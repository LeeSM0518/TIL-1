# Transaction

<img src="https://user-images.githubusercontent.com/42791260/44822818-1b3e1680-ac38-11e8-9ba2-fb12d86a3f15.png" width="50%">

[![npm](https://camo.githubusercontent.com/f9423913a0a2104581c00dbe8067aeb6d18d0010/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f76657273696f6e2d323031382e33352d627269676874677265656e2e737667)](https://github.com/CheolhoJeon/TIL/blob/master)



## Intro

**트랜잭션(Transaction)**이란, 하나의 논리적인 작업 단위를 구성하는 연산들의 집합을 말합니다. 즉, 데이터베이스의 상태를 변화시키기 위해 수행하는 **작업의 단위**를 뜻합니다.

착각하지 말아야 할 것은, 작업의 단위는 질의어(SQL) 한문장이 아니라는 점입니다. 질의어 한문장은 트랜잭션을 구성하는 하나의 연산이 될 것이며 이러한 질의문들이 모여 트랜잭션을 구성합니다.



## Example

위의 설명으로 이해되지 않는다면 예를 한번 들어봅시다. 은행 업무에 관련된 데이터베이스 응용 프로그램에서 계좌이체를 위해 여러 데이터베이스 연산(검색, 삽입, 삭제, 수정)이 필요로 합니다. 여기서 계좌이체라는 논리적인 작업 단위는 트랜잭션이 될 것이며 계좌이체 트랜잭션은 여러 질의문으로 구성됩니다.