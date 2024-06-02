# Github Actions를 활용한 README.md 업데이트 자동화

## Github Actions란?
Github에서 제공하는 CI/CD툴이다. 자세한 내용은 다른 문서를 참고하길 바란다.

## 개요
- Github Actions를 어떤식으로 활용하는것이 좋을까 고민을 하다가, 현 단계에서 사용할 수 있는 활용법으로 현재 Repository에 추가되는 md파일들을 자동으로 README.md에 정리해주는 기능을 적용시켜 볼까 해서 해당 내용을 따라할 수 있도록 작성하고자 한다.
- 아이디어: git push, PR시에 master branch에 추가될 파일들을 repository를 순회하며 README.md 파일에 작성.

## 따라하기
1. .github\workflows\generate-readme.yml 파일을 만든다.
2. generate-readme.yml 내용작성
```yml
name: Generate README

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.7]

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v1
      with:
        python-version: ${{ matrix.python-version }}
    - name: Update README.md
      run: |
        python update.py
    - name: Push the change
      run: |
          git config --global user.name 'kimisadev27'
          git config --global user.email 'kimisadev27@gmail.com'
          git commit -am "Automated update of README.md" || true
          git push
```
- 설명: main branch에 push, pull_request가 실행될 때, update.py를 실행한다.
3. update.py 작성
```python
#!/usr/bin/env python

import os
from urllib import parse


HEADER="""# TIL

> Today I Learned Wiki

---

"""


def main():
    content = ""
    content += HEADER

    for root, dirs, files in os.walk("."):
        dirs.sort()
        if root == '.':
            for dir in ('.git', '.github'):
                try:
                    dirs.remove(dir)
                except ValueError:
                    pass
            continue

        category = os.path.basename(root)

        content += "### {}\n\n".format(category)

        for file in files:
            name = os.path.basename(file).split('.')[0]
            name = " ".join(word.capitalize() for word in name.split('-'))
            content += "- [{}]({})\n".format(name, parse.quote(os.path.join(category, file)))
        content += "\n"

    with open("README.md", "w") as fd:
        fd.write(content)


if __name__ == "__main__":
    main()
```
- 설명: repository를 순회하며 폴더/파일명을 readme에 추가하고, 링크를 건다.
- 대표 텍스트는 md파일의 첫번째 라인이다.


## 테스트 중 발생한 문제
generate-readme.yml내용 중 - name: Push the change 를 실행중에 아래 에러메세지가 발생했다.
```
remote: Permission to '<github-repository 주소>' denied to github-actions[bot].
fatal: unable to access '<github-repository 주소>': The requested URL returned error: 403
Error: Process completed with exit code 128.
```
### 해결방법
![image](https://github.com/fastcampus-fe-group7/TIL/assets/34756233/62a6307b-f61a-42d2-b80a-f6bffff1c0ac)<br>
위 이미지에서 기본으로 지정된 `Read repository contents and packages permissions` 옵션을<br>
`Read and write permissions` 으로 변경해주고 저장해 접근권한을 변경해서 해결한다.


## 결과
업로드 후 이미지 추가


## 마치며
Github Actions을 활용해 README.md 파일을 업데이트 하는 기능을 추가해봤다.
팀단위 협업할때 이런 기능을 활용해 생산성을 높여보도록 하자.




## 참고자료
[Github Actions docs](https://docs.github.com/ko/actions)
[TIL Auto-Format README](https://github.com/marketplace/actions/til-auto-format-readme)
[github-actions generate-readme](https://github.com/aicioara/til/blob/master/github/github-actions.md)