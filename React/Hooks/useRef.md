# useRef()
useRef()는 보통 React에서 DOM에 직접 접근할 필요가 있을 때 사용하지만, 클래스형 컴포넌트에서의 인스턴스 변수처럼 사용할 수도 있다.


```javascript
const myComponent = () => {
    const publicVariable = useRef();


    const otherFunction = () => {
        publicVariable.current = "SOMETHING"
    }

}
```
선언만 해두고 나중에 할당할 수도 있고,


```javascript
const myComponent = () => {
    const publicVariable = useRef("SOMETHING");


    const otherFunction = () => {
        console.log(publicVariable.current);
    }

}
```
선언과 동시에 할당할 수도 있다.

[참고](https://ko.reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables)

----

##### 클래스형 컴포넌트 + public 인스턴스 변수 사용하는 예제를 함수형으로 고쳐보려다가 알게된 내용인데, 적절한 활용방식인지 모르겠다. 공식 문서에는 렌더링 중에 refs를 할당하지 말라고 되어 있는데, 이 케이스 말고 다른 안티패턴이 있는지 찾아봐야겠다.
