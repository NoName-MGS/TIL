# 2023-07-03 Week 1 배운 점 정리

## 운영체제(안정섭 교수님) 과제 PA_0 해결하기

+ Linked List 
    + 어떤 데이터를 저장할 때 그 다음 순서의 자료가 있는 위치를 데이터에 포함시키는 방식으로 자료를 저장
+ push_stack()함수 구현함.
    +  linked list head를 이용하여 stack을 구현함.
  
```c
void push_stack(char* string)
{
    struct entry* new_stack = (struct entry*) malloc(sizeof (struct entry));
    new_stack->string=(char *) malloc(sizeof char*100);
    INIT_LIST_HEAD(&new_stack->list);
    list_add_tail(&new_stack->list, &stack);
}
```

