![React with TypeScript](https://user-images.githubusercontent.com/31315644/77824045-edd28b00-7142-11ea-83d8-b88e7cb6c97d.png)

------------

# React에서 TypeScript 사용하기 

## 목차

- [JavaScript의 단점](#a1)
  1. [JS 편집기의 자동완성의 불편함](#b1)
  2. [함수 파라미터 타입 체킹을 안해줌](#b2)
  3. [리덕스를 사용할 때 불편함](#b3)
  4. [리액트 컴포넌트 쓸 떄 어떤 props를 넣어야하는지 에디터에서 알 방법이 없다.](#b4)
- [TypeScript를 써야 하는 이유](#a2)


<br/>

----------

### JavaScript의 단점 <a id="a1"></a>

1. [JS 편집기의 자동완성의 불편함](#b1)
2. [함수 파라미터 타입 체킹을 안해줌](#b2)
3. [리덕스를 사용할 때 불편함](#b3)
4. [리액트 컴포넌트 쓸 떄 어떤 props를 넣어야하는지 에디터에서 알 방법이 없다.](#b4)

<br/>

#### JS 편집기의 자동완성의 불편함 <a id="b1"></a>

VS Code를 사용할 경우 간단한 자동완성은 가능하다. 

![JS 편집기의 자동완성의 불편함01](https://media.vlpt.us/post-images/velopert/1ead1cd0-df9a-11e9-a678-e775d1643dee/image.png)

다만, 파라미터가 배열이고 그 배열에 대한 자동완성은 함수내부에서 안될 경우가 존재한다.

![JS 편집기의 자동완성의 불편함02](https://media.vlpt.us/post-images/velopert/37020e30-df9a-11e9-a678-e775d1643dee/image.png)

<br/>

#### 함수 파라미터 타입 체킹을 안해줌 <a id="b2"></a>

가정을 해보자.

아래와 같이 문자열을 인자로 받고 문자열의 길이를 반환해주는 함수가 있다고 가정하자.

개발자라면 당연하게도 이 함수에 들어갈 변수의 타입은 문자열이라고 이해를 할 수 있다.

왜냐하면 변수명을 명백하게도 문자열(str)이라고 적어놨기 때문이다.

```js
function getLength(str) {
  return str.length;
}
```

<br/>

**문제는 저 함수에 숫자를 넣든 배열을 넣는 문제가 안된다는 것이다.** 

```js
getLength(3); // undefined
getLength([1,2,3,4,5]); // 5
```

이는 곧 큰 문제를 야기할 수 있다. 왜냐하면 `getLength(str)`를 만든 개발자의 의도는 문자열을 받는 함수였기 때문이다. 

그런데 엉뚱한 숫자 혹은 배열이 해당 함수에 들어갈 경우 의도와는 다른 결과를 내면서 심지어 오류처리조차 해주지 않는다.

즉, 자바스크립트 환경에서는 실행해볼때까지 해당 코드에 오류가 있는지 없는지 알 방법이 없다.

<br/>

#### 리덕스를 사용할 때 불편함 <a id="b3"></a>

종종 리덕스를 사용하다보면 특정 상태를 가지고는 왔는데 해당 상태 내부를 조회할 경우 불편함을 느낀적이 꽤 있다.

예를들면, 아래와 같은 경우이다.

```jsx
const feed = useSelector(state => state.feed.feeds)
```

`useSelector`를 이용해 리덕스 스토어 안에 있는 상태를 조회하였다. 

`JS`만을 이용할 경우, 여기서 `state.feed.feeds`에 `.`을 붙인다고 안에 있는 상태가 나열되지 않는다. 

**즉, 상태안에 어떤값이 들어가 있는지 알아보려면 에디터 단에서는 알 수 가 없다.**

따라서, Redux DevTools로 확인 하거나, 리듀서 관련 코드가 들어가 있는 파일을 열어서 확인해봐야 한다.

<br/>

#### 리액트 컴포넌트 쓸 떄 어떤 props를 넣어야하는지 에디터에서 알 방법이 없다. <a id="b4"></a>

- 리액트 컴포넌트에서는 `propTypes` 라는 것을 사용하면 특정 컴포넌트에서 필요한 `props` 를 지정해서 컴포넌트에서 필요한 `props` 가 없다면 콘솔에 경고를 출력하도록 할 수 있다.
- 문제는 `propTypes` 쓰는 과정이 너무나도 번거롭다. 특히 `props` 로 배열이나 객체 가져와야 하는경우엔  `arrayOf`, `shape` 같은 함수를 이용해야 할 때도 있고 여러 타입인 경우엔 `oneOfType` 란걸 써야 하기 때문에 불편하다.
- `propTypes` 를 설정해도 `props` 빠뜨리면 브라우저 단에서만 경고를 보여줄 뿐 에디터에서는 아무 경고도 보여주지 않기 때문에 실제로 코드를 실행해봐야만 실수를 했는지 안했는지 알 수가 있다.

<br/>

### TypeScript를 써야 하는 이유 <a id="a2"></a>

1. **IDE 를 더욱 적극적으로 활용 할 수 있다.**
   - 자동완성 및 타입 체킹이 되기 떄문에 개발 생산성 상승. 
   - 어떤 컴포넌트를 사용하거나, 함수를 사용 할 때 해당 파일을 직접 얼여보지 않고도 어떤 props 또는 파라미터를 넣어줘야 하는지 알 수 있다. 
   - 리덕스를 사용하게 될 때에도, 리듀서 관련 코드를 열지 않고도 상태 객체가 어떤 구조로 이루어졌는지 확인 가능.
2. **실수를 줄 일 수 있다.**
   - 대부분의 실수들은 타입 체킹(특히 null)에서 많이 나오게 되는데 TypeScript를 이용할 경우 에디터 단에서 타입 체킹이 바로바로 가능해져 이러한 실수를 많이 줄일 수 있다.
3. **협업 시 유용**
   - IDE에서 컴포넌트, 함수 등을 사용 할 때 어떤 값을 어떤 타입으로 넣어야 하는지 바로 IDE상에서 확인 할 수 있기 때문에 굳이 주석으로 작성하거나, 코드를 읽어보거나, 협업하는 사람에게 물어보지 않아도 쉽게 사용 할 수 있다.

<br/>

-----------

### Reference

- [velopert.log : 리액트 프로젝트에서 타입스크립트 사용하기](https://velog.io/@velopert/using-react-with-typescript)