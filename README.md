# ⛄ 202230133 정지호
## 5월 8일 강의
### 인라인 조건
#### 1. 인라인 if
* if문을 직접 사용하지 앟고, 도일한 효과를 내기 위해 && 논리 연산자를 사용합니다.
* &&은 and 연산자로 모든 조건이 참일 때만 참.
* 첫 조건이 거짓이면 두번째 조건은 판단할 필요가 없습니다.
#### 2. 인라인 if-else
* 삼항 연산자 사용 
```
조건문 ? 참일 경우 : 거짓일 경우
```
### Arguments 전달하기
* 함수를 정의할 때 피라미터 혹은 매개변수, 함수를 사용할 때는 아귀먼트 혹은 인수라고 부릅니다. 
```js
<button onClick={(event) => this.deleteItem(id, event)}>삭제</button>
<button onClick={this.deleteItem.bind(this, id)}>삭제</button>
```
* 위 코드는 모두 동일한 역할을 하지만 하나는 화살표 함수를 , 다른 하나는 bind를 사용함.
* 이벤트 핸들러에 매개변수를 전달해야 하는 경우도 많습니다.
* event라는 매개변수는 리액트의 이벤트 객체를 의미합니다.
* 두 방법 모두 첫 번째 매겨변수는 id이고 두 번째 매개변수로 event가 전달 됩니다.
* 1번 코드, 명시적으로 event를 매개 변수로 넣어주고 2번 코드는 id 이후 두 번째 매개변수로 event가 자동 전달 됩니다.

## 5월 1일 강의
### 이벤트 처리하기
* DOM에서 클릭 이벤트 처리하는 코드
```js
<button onclick="activate()">
  Activate
</button>
```

* React에서 클릭 이벤트 처리하는 예제 코드
```js
<button onClick={activate}>
  Activate
</button>
```

**둘의 차이점** <br>
1) 이벤트 이름이 onclick에서 onClick으로

```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);

    this.state = {isToggleOn: true};

    // callback에서 `this`를 사용하기 위해선 바인딩을 필수적으로 해줘야 함.
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setTate(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isTogggleOn ? '켜짐' :'꺼짐'}
      </button>
      
    )
  }
}
```
* 이벤트 핸들러 추가 방법?
* 버튼을 클릭하면 이벤트 핸들러 함수인 handleClick()함수를 호출하도록 되어 있습니다.
* bind를 사용하지 않으면 this.handleClick은 글롭ㄹ 스코프에서 호출되어, undefined로 사용할 수 없기 때문.
* bind를 사용하지 않으려면 화살표 함수를 사용하는 방법도 있음.
* 하지만 클래스 컴포넌트는 이제 거의 사용하지 않기 때문에 이 내용은 참고만.
### 훅의 규칙
**1. 무조건 최상위 레벨에서만 호출.**
* 따라서 반복문이나 조건문 또는 중첩된 함수들 안에서 훅을 호출하면 안 됨.
* 규칙에 따라 훅은 컴포넌트가 렌더링 될 때마다 같은 순서로 호츌 되어야 함. <br>

**2. 함수형 컴포넌트에서만 훅을 호출해야 함.**
* 따라서 일반 자바스크립트 함수에서 훅을 호출하면 안 됨.
* 훅은 함수형 컴포넌트 혹은 직접 만든 커스텀 훅에서만 호출할 수 있음.

**주의할 점** 
* 일반 컴포넌트와 마찬가지로 다른 훅을 호출하는 것은 무조건 커스텀 훅의 최상위 레벨에서만 해야함.
* 이름은 반드시 use사용.(그렇지 않으면 다른 훅을 불러올 수 없음.)<br>


## 4월 17일 강의
### 훅Hook이란 무엇인가?
* 클래스형 컴포넌트에서는 생성자(constructor)에서 state를 정의하고, **setState() 함수**를 통해 state를 업데이트 합니다.
* 예전에 사용하던 함수형 컴포넌트는 별도로 state를 정의하거나, 컴포넌트의 생명주기에 맞춰서 어떤 코드가 실행되도록 할 수 없었습니다. 
* 함수형 컴포넌트에서도 state나 생명주기 함수의 기능을 사용하게 해주기 위해 추가된 기능이 바로 훅(hook)입니다.
* 함수형 컴포넌트도 훅을 사용하여 클래스형 컴포넌트의 기능을 모두 동일하게 구현할 수 있게 되었습니다. 
* Hook이란 state와 생명주기 기능에 **갈고리를 걸어 원하는 시점**에 정해진 함수를 실행되도록 만든 함수를 의미합니다. 
* 훅의 이름은 모두 **use**로 시작합니다.
* 사용자 정의 훅을 만들 수 있으며, 이 경우에 이름은 자유롭게 할 수 있으나 **use**로 시작할 것을 권장합니다.
* **useState**는 함수형 컴포넌트에서 state를 사용하기 위한 Hook 입니다. 
* 증가 시킬 수는 있으나 증가할 때마다 재 렌더링은 일어나지 않음.

### useEffect
* **useState와 함께 가장 많이 사용하는 Hook**
* 이 함수는 사이드 이펙트를 수행하기 위한 것.
* 영어로 side effect는 부작용을 의미. 일반적으로 프로그래밍에서 사이트 이펙트는 '개발자가 의도하지 않은 코드가 실행되며 버그가 발생하는 것'을 말함.
* 하지만 리액트에선 효과 또는 영향을 뜻하는 effect의 의미에 가까움.
* 예를 들어 서버에서 데이터를 받아오거나 수동으로 DOM을 변경하는 등의 작업을 의미.
* 이 작업을 이펙트라 부르는 이유는 이 작업들이 다른 컴포넌트에 영향을 미칠 수 있으며, 렌더링 중에는 작업이 완료될 수 없기 때문임. 렌더링이 끝난 이후에 실행되어야 하는 작업들임.
* 클래스 컴포넌트의 생명주기 함수와 같은 기능을 하나로 통합한 기능을 제공.
* 저자는 useEffect가 side effect 가 아니라 effect에 가깝다고 설명하고 있으나, 이것은 부작용의 의미를 잘못 해석해 생긴 오해임.
* sideEffect는 렌더링 외에 실행해야 하는 부수적 코드를 말함.
* 예를 들어 네트워크 리퀘스트, DOM 수동 조작, 로깅 등은 정리가 필요 없는 경우.
#### useEffect()함수 사용법
```js
useEffect(이펙트 함수, 의존성 배열);
```
* 첫 번째 파라미터는 이펙트 함수가 들어가고, 두 번째 파라미터로는 의존성 배열이 들어감.
* 의존성 배열은 이펙트가 의존하고 있는 배열로, 배열 안에 있는 변수 중 하나라도 값이 변경되었을 때 이펙트 함수가 실행됨.
* 이펙트 함수는 처음 컨포넌트가 랜더링 이후 재 렌더링 할 때 실행됨.
* 만약 이펙트 함수가 마운트와 언마운트 될 때만 한 번씩 실행되게 하고 싶으면 빈 배열을 넣으면 됨. 이 경우 props나 state에 있는 어떤 값에도 의존하지 않기 때문에 여러 번 실행되지 않음.
#### useMemo()
* useMemo()훅은 Memoized value를 리턴하는 훅임
* 이전 계산값을 갖고있기 때문에 연산량이 많은 작업의 반복을 피할 수 있음.
* 렌더링이 일어나는 동안 실행됨
* 따라서 렌더링 중 실행돼서는 안될 작업을 넣으면 안 됨
* 예를 들어 useEffect에서 실행되어야 할 사이드 이펙트 같은 것임.
```js
  const memoizedValue = useMemo(
    () => {
      //연산량이 높은 작업을 수행하여 결과를 반환
      return computeExpensiveValue(의존성 변수1, 의존성 변수2);
      [의존성 변수1, 의존성 변수2]
    }
  )
```

* 다음 코드와 같이 의존성 배열을 넣지 않을 경우, 렌더링이 일어날 때마다 매번 함수가 실행 됨.
* 따라서 의존성 배열을 넣지 않는 것은 의미가 없음.
* 빈 배열을 넣게 되면 컴포넌트 마운트 시에만 함수가 실행됨.
```js
const memoizedValue = useMemo(
  () => computeExpensiveValue(a,b)
);
```

### useCallback
* useCallback() 혹은 useMemo()와 유사한 역할을 합니다.
* 차이점은값이 아닌 함수를 반환한다는 점.
* 의존성 배열을 파라미터로 받는 것은 useMemo와 동일함.
* 파라미터로 받은 함수를 콜백이라 부름
* useMemo와 마찬가지로 의존성 배열 중 하나라도 변경되면 콜백함수 반환.
```js
const memoizedCallback = useCallback(
    () => {
      doSomething(의존성 변수1, 의존성 변수2);
    },
      [의존성 변수1, 의존성 변수2]
  )
```


### useRef
* useRef() 훅은 레퍼런스를 사용하기 위한 훅임.
* 레퍼런스란 특정 컴포넌트에 접근할 수 있는 객체를 의미
* useRef() 훅은 바로 이 레퍼런스 객체를 반환함.
* 레퍼넌스 객체에는 .current라는 속성이 있는데 이것은 현재 참조하고 있는 엘리먼트를 의미함
```js
const refContainer = useRef(초깃값);
```
* 이렇게 반환된 레퍼런스 객체는 컴포넌트의 라이프타임 전체에 걸쳐 유지됨.
* 즉, 컴포넌트가 마운트 해제 전까지는 계속 유지된다는 의미임.

## 4월 3일 강의
### props 사용법
* JSX에서는 key-value쌍으로 props를 구성
```js
function App(props) {
    return(
        <Profile
            name="지호"
            intro='안녕하세요.'
            viewCount={1500}
        />
    );
}
```
1. Profile 컴포넌트로 name, introductio, viewCount Props를 전달한다.
2. 이때 전달되는 props는 다음과 같은 자바스크립트 객체임
```js
{
    name="지호"
    intro='안녕하세요.'
    viewCount={1500}
}
```
* JSX에서 중괄호를 사용하면 JS코드를 넣을 수 있음.
* props를 통해 value를 할당할 수도 있고, 직접 중괄호를 상요하여 할당할 수도 있음.
```js
function App(props) {
    return(
        <Layout
            width={2500}
            height={1400}
            header={
                <Header title="리액트" />
            }
            footer={
                <Footer />
            }
        />
    );
}
```

* JSX를 사용하지 않는 경우 props의 전달 방법은 createElement()함수 사용

### 컴포넌트 만들기
#### 1.컴포넌트 종류
* 리액트 초기 버전을 사용할 때는 클래스형 컴포넌트를 주로 사용
* 이후 Hook이라는 개념이 나옴녀서 최근에는 함수형 컴포넌트를 주로 사용.
* 예전에 작성된 코드나 문서들이 클래스형 컴포넌트를 사용하고 있기에, <br>
    클래스형 컴포넌트와 컴포넌트의 생명주기에 관해서도 공부해야함. 
#### 2.함수형 컴포넌트
* Welcome 컴포넌트는 props를 받아, 받은 props 중 name키의 값을 "안녕" 뒤에 넣어 반환.

 ```js
        function Welcome(props) {
            return <h1>안녕하세요, {props.name}님</h1>;
        }

 ```

#### 3.클래스형 컴포넌트
* Welcome 컴포넌트는 React.Component class로 부터 상속 받아 선언함.
```js
        class Welcome extends React.Component {
            render() {
                return <h1>안녕하세요, {this.props.name}님</h1>;
            }
        }
```
#### 4.컴포넌트 이름 짓기
* 이름은 항상 대문자 시작 <br>
   &nbsp;&nbsp; -> 리액트는 소문자로 시작하는 컴포넌트를 DOM 태그로 인식하기 때문.
**컴포넌트 파일 이름과 컴포넌트 이름은 같게 함**

#### 5.컴포넌트의 렌더링
```js
function  Welcome(props) {
    return <h1> HI, {props.name}</h1>;
}

const element = <Welcome name="인제" />;
 ReactDOM.render(
    element,
    document.getElementById('root')
 );
```
#### 5.4컴포넌트 합성
* 컴포넌트 합성은 여러 개의 컴포넌트를 합쳐서 하나의 컴포넌트를 만드는 것
* 리액트에서 컴포넌트 안에 또 다른 컴포넌트를 사용할 수 있기 때문에, 복잡한 화면을 러 개의ㅐ 컴포넌트로 나누어 구현 O
* 다음 코드에서 props의 값을 다르게 해 Welcome 컴포넌트 여러번 사용
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App(props) {
  return (
    <div>
      <Welcome name="Mike" />
      <Welcome name="Steve" />
      <Welcome name="Jane" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

#### 5.5 컴포넌트 추출
* 복잡한 컴포넌트를 쪼개서 여러 개의 컴포넌트로 나눌 수도 있음.
* 큰 컴포넌트에서 일부를 추출해서 새로운 컴포넌트를 만드는 것.
* 실무에선 처음부터 1개의 컴포넌트에 하나의 기능만 사용하도록 설계하는 것이 좋음.
<br><br>

```js
function Comment(props) {
  return (
    <div className="Comment">
      <Avatar user={props.author} />
      <div className="user-info">
        <div className="user-info-name">
          {props.author.name}
        </div>
        <div className="user-info-text">
          {props.text}
        </div>
      </div>
    </div>
  );
}
function Avatar(props) {
  return (
    <img className="avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

* Comment는 댓글 표시 컴퍼넌트.
* 내부에서 이미지, 이름, 댓글과 작성일이 포함되어 있음.
* 첫 번째로 이미지 부분을 Avatar 컴포넌트로 출력
* 두 번째로 사용자 정보 부분 추출
* 컴포넌트 이름은 UserInfo. React 컴포넌트 이름은 Camel notation을 사용
* UserInfo 안에 Avatar 컴포넌트를 넣어 완성시킴.

```js
function UserInfo(props) {
  return (
    <div className="userInfo">
      <Avatar user={props.user} />
      <div className="user-info-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

* 추출 후 다시 결합한 UserInfo를 Comment 컴포넌트 반영하면 다음과 같은 모습이 됨.

```js
function Comment(props) {
  return (
    <div className="comment">
      <UserInfo user={props.author} />
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

#### 5.6 댓글 컴포넌트 만들기
```js
function Comment(props) {
  return (
    <div className="comment">
      <UserInfo user={props.author} />
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

### State: 리액트 컴포넌트의 상태
* 상태의 의미는 정산인지 비정상인지가 아니라 컴포넌트 데이터를 의미
* 정확히는 컴포넌트의 변경가능한 데이터를 의미
* state가 변하면 다시 렌더링이 되기 때문에 렌더링과 관련된 값만 state에 포함 시켜야 함.

### state 특징
* 리액트 만의 특별한 형태가 아닌 단지 자바스크립트 객체일 뿐
* constructor은 생성자이고, 그 안에 있는 this.state가 현 컴포넌트의 state임.
* 함수형에서는 useState()라는 함수 사용.
* state는 변경가능하다 했으나 직접 수정해선 안 됨. *(불가능 하다고 생각하는 것이 좋음.)*
* state를 변경하고자 할 땐 **setstate()** 함수 사용

### 생명주기에 대해
* 생명주기는 컴포넌트의 생성 시점, 사용 시점, 종료 시점을 나타냄.
* constructor가 실행되면서 컴포넌트 생성
* 생성 직후 **componentDibMount()** 함수가 호출.
* 컴포넌트가 소멸하기 전까지 여러 번 랜더링 함.
* 랜더링은 **props, setState(), forceUpdate()** 에 의해 생태가 변경되면 이루어짐.
* 렌더링이 끝나면 **componentDinUpdate()** 함수 호출.
* 컴포넌트가 언마운트되면 **compomentWillUnmount()**함수 호출.

## 3월 27일 강의
### **JSX**: JS,XML,HTML을 함께 사용할 수 있는 JS 확장 문법
* JSX는 내부적이로 XML/HTML 코드를 JS로 변환함.
* React 가 createElement 함수를 사용하여 자동으로 JS로 변환해줌.
* 만일 JS로 작업할 경우 직접 createElement함수를 사용해야 함.
* 앞으로 설명하는 코드를 보면 알 수 있지만 결국 JSX는 가독성을 높여 주는 역할.

### 장점
* 코드 간결
* 가독성 향상
* Injection Attack 이라 불리는 해킹 방법을 방어함으로써 보안에 강함.

### JSX 사용법
* 모든 JS 문법을 지원
* JS 문접에 XML과 HTML을 섞어서 사용
* 만일 html이나 xml에 JS코드를 사용하고 싶으면 { } 괄호를 사용합니다.

---
### 엘리먼트: 리액트 앱을 구성하는 요소
* 웹사이트의 경우는 DOM 엘리먼트이며 HTML 요소를 의미함.
### 리액트 엘리먼트 **VS** DOM 엘리먼트
- 리액트 엘리먼트는 Virtual DOM의 형태를 취함.
- DOM 엘리먼트는 페이지의 모든 정보를 갖고 있어 무거움.
- 반면 리액트 엘리먼트는 변화한 부분만 갖고 있어 가벼움.
```
                            |            DOM             |           Virtual DOM
_______________________________________________________________________________________
       업데이트 속도         |           느리다            |             빠르다
---------------------------------------------------------------------------------------
                            |                             |변화부분을 가상 DOM으로 만든 
    element 업데이트 방식    |     DOM 전체를 업데이트      |DOM과 비교하여 다른 부분만  
                            |                             |업데이트
---------------------------------------------------------------------------------------
           메모리            |         낭비 심함           |           효율적
```
### 엘리먼트 생김새
* 리액트 엘리먼트는 JS 객체의 형태로 존재
* 컴포넌트(Button 등), 속성 (color 등) 및 내부의 모든 children을 포함하는 일반 JS 객체
* 마음대로 변경할 수 없는 불변성을 갖음.
* 내부적으로 JS 객체를 만드는 역할 함수 => **createElement()**

**?? 내용이 바뀐다면 ??**
* 컴포넌트를 통해 새로운 엘리먼트 생성
* 그 다음 이전 엘리먼트와 교체를 하여 내용을 변경
* 교체하는 작업을 위해선 **Virtual DOM**을 사용
### 엘리먼트 렌더링 하기
이 div태그 안에 리액트 엘리먼트가 렌더링 되며, 이 것을 Root DOM node라고 함
```js
<div id = "root"></div>
```
엘리먼틀르 렌더링하기 위해선 다음과 같은 코드 필요
```js
const element = <h1>안녕, 리액트!</h1>;
ReactDOM.render(lelment, document.getElementById('root'));
```
render() 함수 사용 <br>
첫 번째 파라메터 출력할 리액트 엘리먼트, 두 번째 파라메터는 출력할 타겟을 나타냄. <br>
리액트 렌더링 = Virtual DOM에서 실제 DOM으로 이동하는 과정<br>
**렌더링된 엘리먼트 업데이트**
**tick()** 함수 정의<br>
    : 현재 시간을 포함한 element를 생성하여 root div에  렌더링.

### 컴포넌트
* 리액트는 컴포넌트 기반의 구조.
* 컴포넌트 구조 : 작은 컴포넌트가 모여 큰 컴포넌트를 구성하고, 다시 이런 컴포넌트들이 모여 전체 페이지 구성.
* 컴포넌트는 재사용이 가능하기 때문에 전체 코드의 양을 줄일 수 있음. <br>
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    => 개발 시간과 유지 보수 비용도 줄일 수 있음.
* 컴포넌트는 JS함수와 입력과 출력이 있다는 면에서 유사함.
* 다만 입력은 **Props**가 담당하고, 출력은 리액트 엘리먼트의 형태로 출력됨.
* 엘리먼트를 필요한 만큼 만들어 사용한다는 면에서 객체 지향의 개념과 비슷.

### Props (property: 속성, 특성)
* 어떤 속성, props 를 넣느냐에 따라 속성이 다른 엘리먼트가 출력됨.
* props는 컴포넌트에 전달 할 다양한 정보를 담고 있는 자바스크립트 객체 <br>
***에어비엔비***


### 특징
* 읽기 전용. 변경 불가능
* 속성이 다른 엘리먼트를 생성하려면 새로운 props를 컴포넌트에 전달하면 됨.

### Pure 함수 VS Impure 함수
* Pure 함수는 인수로 받은 정보가 함수 내부에서도 변하지 않는 함수
* Impure 함수는 인수로 받은 정보가 함수 내부에서 변하는 함수 

## 3월 20일 강의

### 리액트: 사용자 인터페이스를 만들기 위한 js 라이브러리
* 복잡한 사이트를 쉽고 빠르게 만들고, 관리하기 위해 만들어진 것.
* 주로 웹 App의 UI를 개발하는데 사용
* 다른 표현으로 는 SPA를 쉽고 빠르게 만들 수 있도록 해주는 도구

### 장점
1. **빠른 업데이트와 렌더링 속도**
    * Virtual DOM이 가능하게 함.
    * DOM이란 XML, HTML 문서의 각 항목을 계층으로 표현하여 생성, 변형, 삭제할 수 있도록 돕는 인터페이스. (W3C표준)
    * virtual DOM은 DOM 조작이 비효율적인 이유로 속도가 느리기에 고안된 방법
    * DOM: 동기식, Virtual DOM: 비동기식
2. **컴포넌트 기반 구조**
    * 리액트의 모든 페이지는 컴포넌트로 구성
    * 하나의 컴포넌트는 다른 여러 개의 컴포넌트 조합으로 구성
    * 리액트로 개발 하다 보면 레고 블록을 조립하는 것처럼 컴포넌트를 조합해서 웹을 개발하게 됨.

3.  **재사용성**
    * 반복적인 작업을 줄여주어 생산성을 높여줌.
    * 유지보수 용이
    * 재사용이 가능 하려면 해당 모듈의 의존성을 없애야 함.
4. **든든한 지원**
    * 메타에서 오픈소스 프로젝트로 관리하여 계속 발전 중.
5. **활발한 지식 공유 & 커뮤니티**
6. **모바일 앱 개발 가능** 
    * 리액트 네이티브라는 UI프레임워크로 크로스플랫폼 모바일 앱 개발 가능
### 단점
1. 방대한 학습량
2. 높은 상태 관리 복잡도

### 리액트 설치하기
* 노드깔기
    * npm cache clean -force
    * npm install -g node@latest
    * node -v // 확인
* 터미널 열어
    * 설치가 잘 안되는 편 무한시도!!, 다른 파일 만들어서 시도해보면 되는 경우도 있음
    * npm install -g npm@latest // npm 최신버전 다운
    * npm -v // npm 버전확인
    * npm uninstall -g create-react-app // 리액트 지우기(처음에는 안해도 됨)
    * npm install -g create-react-app // 리액트 설치
    * npx create-react-app *파일이름* // npx 이용해서 리액트 설치 시도하는 법
* 리액트 열기
    * npm start

## 3월 13일 강의
자바에서 클래스를 쓰는 케이스 cassAacc = 카멜(낙타)케이스 디비 컴포넌트를 만들 때도 권장.

---
commit할 때 스테이지에 변경 파일 올리고 메시지 적어서 커밋.
* 커밋 메시지는 20자 미만
* 제목 enter*2 + 내용

<br>노드 current보단 **lts**

<br>

## 3월 6일 강의
# h1
# h1
## h2
### h3
#### h4
##### h5
###### h6
 
<br><br>

# 리스트
1. 첫 번째
2. 두 번째 
3. 세 번째
4. 네 번째

- 첫 번째
- 두 번째
- 세 번째
- 네 번째 

<br><br>

*이탈릭체*
**볼드**
***이탈릭볼드*** 

개행은 스페이스 2번 + 엔터 <br><br>
일반 문장을 쓸 때도 마찬가지

```js 코드 입력 시 사용
const p = document.auerySelector("p");
```

[구글 링크](http://google.com)
[페이지 내 링크](#리스트)

![고양이](고양이.jpg)
🎄
🎅
🎁
<br><br>

---
# react1-2
React1 강의 
