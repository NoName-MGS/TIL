# 2023-07-12 Week 2 배운 점 정리

## 운영체제(안정섭 교수님) 과제 PA_0 해결하기

+ Linked List 
    + 어떤 데이터를 저장할 때 그 다음 순서의 자료가 있는 위치를 데이터에 포함시키는 방식으로 자료를 저장
+ pop_stack() 함수 구현
+dump_stack() 함수 구현
  
```c
void push_stack(char* string){

    struct entry* new_entry = (struct entry*) malloc(sizeof (struct entry));
    new_entry->string=(char *) malloc(100);
    INIT_LIST_HEAD(&new_entry->list);
    list_add_tail(&new_entry->list, &stack);
}

int pop_stack(char* buffer){
    struct entry *del_entry = list_last_entry(&stack,struct entry,list);

    if(del_entry->string){
        list_del(stack.prev);
        return 0;
    } else{
        return -1;
    }
```