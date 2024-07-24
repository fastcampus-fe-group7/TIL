# GitHub Rulesets

## 사전 지식

- GitHub Rulesets을 통해 원격 저장소(Repository) 단위로 규칙을 설정할 수 있으며, 설정된 규칙을 통해 해당 레파지토리 내의 브랜치, 태그, 커밋, 푸시 등의 대상과 동작에 제한을 둘 수 있다.

## 사용방법

- GitHub의 특정 원격 저장소(Repository)에 들어와 Settings - Rules - Rulesets을 통해 진입함

  ![image](https://github.com/user-attachments/assets/6fbd22c4-d527-49ff-81ef-7e2ecc5a69d0)

- Ruleset Name을 통해 해당 규칙의 이름을 설정하고, Enforcement status를 통해 활성화 상태 변경 가능함

  ![image](https://github.com/user-attachments/assets/7599dbe8-8d6f-43a1-b378-0e7df51dc9dd)

- Bypass list를 통해 규칙과 상관 없이 레파지토리를 이용할 수 있는 예외 대상을 설정함

  ![image](https://github.com/user-attachments/assets/c3ea6d95-4ee8-4d7a-a1f9-69e7b42a8d50)

- Targets를 통해 규칙의 대상이 될 브랜치를 설정함

  ![image](https://github.com/user-attachments/assets/93a874c6-0953-48a5-ab87-e5bee91c4906)

- Rules의 옵션을 통해 Target으로 설정한 브랜치에 규칙을 설정할 수 있음
- Restrict creations, updates, deletions : 브랜치의 생성, 수정, 삭제를 제한함

  ![image](https://github.com/user-attachments/assets/8ab34d62-f73c-49c1-b6e9-29b1e391fe8e)

- Require linear history : 병합 커밋 푸시를 방지(rebase 사용하도록 함)함
- Require merge queue : 병합 큐를 통해서만 병합이 진행되도록 순서를 관리할 수 있도록 해줌
- Require deployments to succeed : 성공적으로 배포가 진행됐을 경우에만 push할 수 있도록 함

  ![image](https://github.com/user-attachments/assets/f7c38892-bd91-4f37-9287-dd4a3fac26c3)

- Require signed commits : 인증된 서명을 가진 커밋만 push되도록 함
- Require a Pull Request Before Merging : 대상 브랜치로 병합되기 전에 Pull Request를 거쳐야만 하도록 설정할 수 있음
- Require Status Checks to Pass : 상태 검사를 진행한 뒤 통과되는 커밋만이 push되도록 함

  ![image](https://github.com/user-attachments/assets/b3ed424c-3a00-47ca-9a11-bbf9ae52703c)

- Block force pushes : 설정된 대상 브랜치로 직접 강제 push되는 것을 방지함
- Require Code Scanning Results : 브랜치에 특정 커밋을 업데이트하기 전에 정적 분석 도구를 통해 검사되도록 함

  ![image](https://github.com/user-attachments/assets/36f916d0-23d7-4d60-84ef-9ae153f943d4)

- Restrictions의 옵션을 통해 제한 사항을 설정할 수 있음
- Restrict Commit Metadata : 커밋 작성자의 이메일 주소, 커밋 메시지 내용 등을 제한 할 수 있음
- Restrict Branch Names : 브랜치 이름 명명 규칙을 강제해 일관성 있는 브랜치 네이밍을 하도록 할 수 있음

  ![image](https://github.com/user-attachments/assets/e94fe755-0bb0-4676-a8b6-801643f20024)
