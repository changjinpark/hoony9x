## Online Judge 채점 모듈 개발
- 2015.08
- **본 프로젝트는 소스코드가 유실되어서 현재 존재하지 않는 상태입니다.**

학교에서 배웠던 시스템프로그래밍 과목의 지식을 적극 활용하여 개인적으로 진행해 본 프로젝트입니다.

채점모듈은 크게 2가지 부분으로 나눌 수 있습니다. 

1. 채점 대기중인 소스 코드 및 제출 정보를 DB 에서 불러오기 
2. 불러온 소스 코드를 컴파일, 실행, 그리고 출력 결과 검증 

1번은 단순히 MySQL DB 에 접속해서 데이터를 송수신하는 부분입니다. 핵심은 2번에 있습니다. 
2번의 경우 학교 과목 중 시스템프로그래밍에서 배웠던 내용을 기반으로 코드를 작성했습니다. 
- 컴파일 과정: 소스 코드를 가져온 후 Child Process 생성. 컴파일을 Child Process 에서 진행하고 컴파일이 완료될 때 까지 Parent Process 는 대기 
- 실행 과정: 컴파일이 성공적으로 끝났다면 실행 파일이 생성되어 있을 것인데 이를 실행. 이 과정 역시 실행 파일을 Child Process 를 생성 후 여기서 실행하고 종료될때까지 Parent Process 는 대기. 데이터의 입출력은 stdin, stdout 을 이용하도록 했으며 이를 위해 Child Process 에서 실행을 하기 전에 input/output stream redirection 을 진행. 지정된 시간 내에 실행이 끝나지 않을 경우 SIGKILL 을 보내 강제로 종료. 
- 출력 결과 검증 과정: 오류 없이 종료가 되었을 경우 stdout 으로 나온 출력 결과물을 검증. 미리 준비된 파일과 1:1 비교를 할 수도 있고 복수정답 문제의 경우 출력 결과를 검증하는 별도의 코드를 사용하기도 함. 

이 과정을 무한 반복하도록 하여 채점 모듈의 동작을 확인했습니다.