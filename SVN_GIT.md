# 형상관리툴

+ 소프트웨어 버전 관리 툴
+ 형상관리는 소스의 변화를 끊임없이 관리하는 것을 말한다.
+ 소스를 버전 별로 관리할 수 있어서 개발할 때 실수로 소스를 삭제하거나, 수정하기 이전으로 돌아가야되는 경우 유용하게 사용되는 툴
+ 팀 프로젝트에서도 누가 무엇을 어떻게 수정했는지도 알 수 있기 때문에 코드를 병합하거나 수정된 소스를 추적하는 데에도 쓰인다.

+ 종류
  + Client/Server 타입 : Subversion(SVN), CVS, Perforce, ClearCase, TFS
  + 분산저장소 타입 : Git, Mercurial, Bitkeeper, SVK, Darcs
  + Folder 공유 타입 : RCS, SCCS
  
  1. CVS
  - 1980년대에 만들어진 형상관리 툴이지만 파일 관리나 커밋 중 오류 시 롤백이 되지 않는 등 불편한 문제점이 있어 이후 SVN으로 대체됨
  
  2. SVN
  - 2000년에 CVS를 대체하기 위해 만들어졌으며 현재까지 두루 사용되는 형상관리 툴
  
  - trunk
    + 프로젝트에서 가장 중심이 되는 디렉터리
  
  - branches
    + trunk에서 뻗어져 나온 나뭇가지. 프로젝트 내의 작은 프로젝트
    
  - tags
    + 버전 별로 소스코드를 따로 관리하는 공간(버전 별로 태그를 붙여서 tag 디렉터리 안에 보관한다고 생각하면 됨)
    
   3. GIT
   - 매우 빠른 속도와 분산형 저장소. SVN보다 많은 기능을 지원하는 대신 당연히 익숙해지기에 더 많은 시간이 필요함.
   
   4. SVN vs GIT 비교
    1) SVN
      - SVN은 보통 대부분의 기능을 완성해놓고 소스를 중앙 저장소에 commit
      - commit의 의미 자체가 중앙 저장소에 해당 기능을 공개한다는 의미.
      - 개발자가 자신만의 version history를 가질 수 없다. (그렇기 때문에 local History를 이용해야하긴 하지만, 일시적이다. 내가 며칠 전까지에 한하여 작업했던 내역을 확인 가능하지만 버전 관리가 되진 않는다.
      - commit한 내용에 실수가 있을 시에 다른 개발자에게 바로 영향을 미치게 되는 단점도 있다.
      
    2) GIT
      - 반면, git은 개발자가 자신만의 commit history를 가질 수 있고, 개발자와 서버의 저장소는 독립적으로 관리가 가능.
      - commit한 내용에 실수가 있더라도 바로 서버에 영향을 미치지 않는다.
      - 개발자는 마음대로 commit(push)하다가 자신이 원하는 순간에 서버에 변경 내역(commit history)을 보낼 수 있으며, 서버의 통합 관리자는 관리자가 원하는 순간에 각 개발자의 commit history를 가져올 수 있음.
      
 ### 이렇게 git은 서버 저장소와 개발자 저장소가 독립적으로 commit history를 가져갈 수 있기 때문에 매우 유연한 방식으로 소스를 운영할 수 있으며, 이러한 유연성이 git의 가장 큰 장점이다.
 ### 출처 : goddaehee.tistory.com/158
 
      
    
   
