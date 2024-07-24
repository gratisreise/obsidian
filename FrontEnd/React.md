
### React-Dom

Browser[dom] <---> Elm Runtime[vdom]

### VDOM
--- 
HTML
initial model =>  vdom(코드) =>  dom띄워주기 => 실제돔을 눌렀다(이벤트) => vdom(코드)
=> 프론트 서버에서 => 변화메세지를 준다 => 기능 코드를 다시준다 => 바뀐 부분만 바꿔서 로드 시킨다. => 효율을 위해서 =>

vdom과 dom은 다르다 vdom의 목적은 dom을생성하기 위해서 
메모리를 많이 먹는다?: vue vs react




### SPA(Single Page Application)
---

브라우저를 벗어난 곳에서 자바스크립트를 쓰게 하는 것 : 노드js => 이벤트 그리딩?? => 빠르다?
노드는 빠르다 => 인터프리터 + 싱글스레드 => 빠르다? => 뻗기는 쉽다?
npm 잘 가져다 써야함 잘못 가져다 쓰면 완전 망함


```shell
npx create-react-app
```


cli에서 e(environment): 환경변수  || x(execute) : 실행

