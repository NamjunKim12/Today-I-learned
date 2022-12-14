## Git 브랜치 전략
  - 여러 개발자가 하나의 저장소를 사용하는 환경에서 저장소를 효과적으로 활용하기 위한 work-flow이다.
  - 거의 모든 기업들이 자신들의 상황에 맞는 전략을 사용하고 있다.
  - 효과적으로 버전 컨트롤 시스템을 사용하기 위해서는, 프로젝트 여건에 어울리는 브랜치 전략을 세워야한다.
  - 따라서 대표적인 브랜치 전략을 비교해보고 올바른 브런치 전략을 세우는 것이 필요하다.
  
### Git-flow 전략

![스크린샷 2022-10-19 오전 2 16 07](https://user-images.githubusercontent.com/69416561/196500112-60fe7e74-b0b8-40e5-b48b-a57758553d6b.png)


- 크게 다섯개의 브런치를 운영하며 관리한다. 메인브랜치인 main, develop와 보조 브랜치인 feature, release, hotfix로 구성된다. 
- 소프트웨어 버전 관리가 필요한 앱이나 솔루션, 혹은 publicAPI에 적합하다.
- 따라서 웹 애플리케이션에서 Git-flow는 적합한 전략이 아니다.
- 웹 애플리케이션은 일반적으로 롤백되지 않으며, 지속적으로 서비스를 제공하기에 소프트웨어를 다양한 버전으로 지원할 필요가 없기 때문이다.

### Github-flow 전략

![image](http://cdn-ak.f.st-hatena.com/images/fotolife/s/shoma2da/20151104/20151104223339.png)

- 깃허브에서 만든 단순한 구조의 브랜치 전략이다.
- main브랜치를 중심으로 운영되며, 기능개발 버그 수정등의 작업용 브랜치를 구분하지 않는 단순한 구조이다.
- main은 언제나 배포가 가능하다.
- 새로운 프로젝트는 main을 기반으로 별도 브랜치를 생성하여 작업을 진행한다.
- 브랜치는 local에 커밋하고, 머지가 준비됐다면 pull request를 만든다.
- 다른 사람이 변경된 코드를 검토한 뒤 승인하면 master에 병합한다.
- 병합된 master는 즉시 배포할 수 있으며, 배포 해야만 한다.
- 상시-배포가 일어나는 프로젝트에 유용하다.
  
### gitLab-flow 전략

- Github-flow 전략을 기반으로 상황에 따라 워크플로우를 활용하는 방법에 대해 추가적 가이드를 제공함.


## 참고자료

- [Git flow, GitHub flow, GitLab flow](https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/)

- [브랜치 전략 수립을 위한 전문가의 조언들](http://blog.hwahae.co.kr/all/tech/tech-tech/9507/)
