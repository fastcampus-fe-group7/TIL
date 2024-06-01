# Git Branch 전략

## 사전 지식

- Git은 버전 관리 시스템으로 프로젝트의 소스 코드를 관리하기 위해 사용된다.
- Branch는 git의 핵심 기능 중 하나다. 특정 시점의 코드를 기준으로 새로운 분기를 나눠 다양한 테스트나 기능 개발, 버그 수정 등을 독립적으로 진행할 수 있는 환경을 제공한다.
- 다양한 깃 브랜치 전략이 존재하기 때문에 프로젝트의 특성이나 개발 환경에 맞게 적절한 전략을 선택하는 것이 중요하다.

## Git Flow 전략

![image](https://velog.velcdn.com/images/jseo9732/post/a0cfc196-623e-4a27-98d1-a9a8b3d93d17/image.png)

### 브랜치 구성

- main(master)
  - 프로젝트의 기준이 되는 브랜치
  - 실제 배포 진행
- develop
  - 개발자들이 실제로 개발을 진행하는 브랜치
- feature
  - 새로운 기능의 개발을 진행하는 브랜치
  - 개발이 완료되면 develop 브랜치에 merge
- release
  - 배포를 위해 main 브랜치로 보내기 전, 테스트를 위한 브랜치
  - 테스트를 통과하면 main과 develop 브랜치에 merge
- hotfix
  - main 브랜치 배포 이후 문제(버그)가 발생했을 때 긴급 수정을 위한 브랜치

### 특징

- 각 기능별, 배포 환경, 버그 수정 등의 과정을 명확하게 구분하기 때문에 복잡한 개발 프로젝트에서 버전 관리를 체계적이고 효과적으로 할 수 있음
- 대규모 프로젝트 혹은 여러 팀이 협업할 때 사용하기 좋음

## GitHub Flow 전략

![image](https://velog.velcdn.com/images/jseo9732/post/58fdd4a6-f985-455b-a554-bb3d9fb9a545/image.png)

### 브랜치 구성

- main(master)
  - 프로젝트의 기준이 되는 브랜치
  - 실제 배포 진행
- feature
  - 특정 기능이나 버그 수정을 위한 브랜치
  - 작업이 완료되면 main 브랜치에 merge

### 특징

- 비교적 간단하고 직관적인 형태의 브랜치 모델로 지속적 통합 및 배포(CI/CD)에 적합하며 빠른 피드백과 배포가 가능함
- 항상 배포 가능한 상태를 유지할 수 있기 때문에 신속한 개발과 배포가 중요한 프로젝트나 작은 팀, 단기 프로젝트에 사용하기 좋음

## GitLab Flow 전략

![image](https://velog.velcdn.com/images/jseo9732/post/5dfa5aaa-a941-402f-8d67-4dff3fc436b9/image.png)

### 브랜치 구성

- main(master)
  - 프로젝트의 기본 브랜치
  - 최신 개발 상태 반영
  - 안정적인 코드를 production 브랜치로 merge
- production
  - 실제 운영 환경에 배포하기 위한 브랜치
- environment-specific
  - 개발, 테스트, 스테이징 등의 다양한 배포 환경을 위한 브랜치
  - 특정한 환경의 테스트를 위해 사용
- feature
  - 특정 기능이나 버그 수정을 위한 브랜치
  - 작업이 완료되면 main 브랜치에 merge

### 특징

- Git Flow와 GitHub Flow의 장점을 결합한 형태의 브랜치 모델로 다양한 배포 환경을 고려함
- 복잡한 여러 배포 환경을 가진 프로젝트에 사용하기 좋음

## 출처

- https://www.youtube.com/watch?v=w2r0oLFtXAw
