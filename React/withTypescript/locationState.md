# location

react router의 history 객체를 활용하면, 컴포넌트를 마운트시킬 때 필요한 데이터를 함께 보낼 수 있다.

```javascript
history.push({
  pathname: "/to",
  state: {
    // state에 담아 보낸다!
    id,
    name,
  },
});
```

이 변수는 location 객체 내부 state에 담겨서 전달되므로 아래와 같이 확인할 수 있다.

```typescript
const myComponent: React.FunctionComponent<RouteComponentProps> = ({
  location,
}: RouteComponentProps) => {
  //
  useState(() => {
    const { state } = location;
    console.log(state.id);
    console.log(state.name);
  });
  //
};
```

그런데 타입스크립트에서 위와 같이 사용하려고 하면 다음과 에러가 난다.

> Property 'id' does not exist on type '{}'.

location 내의 state의 디폴트 타입이 {}이기 때문이다. 우리가 원하는 타입을 선언해 덮어씌워주는 방식으로 해결 가능하다. RouteComponentProps가 인자로 받는 세번째 제네릭 타입에 우리가 정의한 타입을 넣어주면 된다.

```typescript
import { StaticContext } from "react-router";

// 타입 정의
type LocationState = {
  id: string;
  name: string;
};

const myComponent: React.FunctionComponent<RouteComponentProps<
  {},
  StaticContext,
  LocationState
>> = ({ location }: RouteComponentProps<{}, StaticContext, LocationState>) => {
  //
  useState(() => {
    const { state } = location;
    console.log(state.id);
    console.log(state.name);
  });
  //
};
```

---
