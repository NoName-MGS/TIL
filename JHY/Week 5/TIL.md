# 2023-08-22 Week 5 배운 점 정리

## MOCA 운영체 학습모듈_Process 수강
  
# process

+ Implementin Processes
    + process control block - 프로세스에 대응되는 abstract data type
        + long state;                             /*state of the prcess*/
        + pid_t pid; pid_t tgid;            /*process identifier*/
        + struct task_struct *parent;*   /*this process”s parent*/
        + struct list_head children;    /*list of my children*/
        + struct mm_struct *mm;      /*adress space of this process*/

+ Process가 만들어지는 5가지 state
    + new : 프로세스 생성
    + running : 명령이 실행되고 있다.
    + waiting : 어떤 이벤트가 발생해서 프로세스가 대기함.
    + ready : 프로세스가 프로세서에 승인되기를 기다림
    + terminated : 프로세스 실행 종료

+ Inter-Process Communications Models(다른 프로세스들과 소통하는 여러가지 메커니즘)
    1. Shared memory
        1. 운영체제가 system call에 의해 shared memory를 만들어줌
        2. 프로세스들을 join시켜줌
        3. 판을 깔아주고 연결해줌. 운영체제는 관여하지 않음
        + 단점) implementation overhead가 크다.
        + 장점) 프로토콜 자체는 복잡하지만 성능이 좋음. (운영체제의 관여가 최소화)
    2. Message passing
        1. 운영체제가 메세지 전체를 전달해주는 형태
        + 단점) user와 kernel끼리의 switch가 많이 발생
        + 장점) 운영체제에게 한번 보내주면 끝

+ Signals
    + 여러개의 프로세스에게 나 이런 일이 있어라고 알려주는 형태의 메커니즘
    + 내가 너한테 시그널을 보냄. 너가 읽씹하거나 받아서 핸들링하거나
    + 처리를 하다가 문제가 발생하면 운영체제가 시그널을 보냄.