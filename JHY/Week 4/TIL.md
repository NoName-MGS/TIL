# 2023-08-04 Week 4 배운 점 정리

## MOCA 운영체 학습모듈_Process termination 수강
  
# process

+ fork()
    + 프로세스를 새로 만들기 위한 시스템 call
    + 자신과 완전히 동일한 값을 만드는 자식(process)을 생성(현재 process 복제)
    + 복사본을 만드는 것이지 둘이 변경사항을 공유하지 않음.
    + 누가 부모고 누가 자식인지 구별 할 수 없음(pid로는 구별 가능)

+ exec()
    + 프로세스의 이미지를 완전 새로운 call로 변경
    + 현재돌리고 있던 모든 내용이 다 날아가고 처음부터 다시 만듦
    + execl(), execlp(), execle(), execv(), execvp(), execvpe()
        + l→내가 무엇으로 변신할지 arguments를 콤마로 구별
        + v→string의 array 형태
        + p→ 경로
        + e→specify environment variables

+ wait()
    + 부모가 wait()를 통해 자식의 return code를 알 수 있다.
    + pid = waitpid(-1, &status, 0);
    + pid = waitpid(childpid, &status, 0);

+ zombie process
    + 프로세스는 죽었지만 부모가 exit(return code)를 회수하지 않은 프로세스.

+ orphan process
    + 부모 프로세스가 자식보다 먼저 죽었을 경우.(child가 살아있는데 parent가 죽음)
    + zombie process를 많이 만들 수 있음
    + 많이 복잡해짐 → 해결방법
        + parent가 죽으면 child도 죽임(cascading termination 방법)
        + child들을 다른 process 밑으로 붙여줌(process hierarchy 방법)
            + 리눅스는 parent가 죽으면 init에 붙여줌.