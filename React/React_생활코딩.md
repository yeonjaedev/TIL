# React - 생활코딩


## 1. 컴포넌트 : 컴포넌트를(ex topbar, sidebar..) 태그만으로 가져와서 사용
* 1. 가독성
* 2. 재사용성
* 3. 유지보수

cf) npm 과 npx 차이
* npm : nodejs를 이용한 여러 유용한 라이브러리? 등을 설치할 수 있도록 도움 ( 앱스토어와 유사)
* npx : 일회성 ( 설치 후 한 번만 사용)

jsx - javascript언어로 쉽게 컨버팅 해주는
```jsx
class App extends Component {
    render() {
        return ( <
            div className = "App" >
            <
            Subject > < /Subject> <
            /div>
        )
    };
}
```
여기서

원래 태그를 표현하는 부분에 '</div' 이런식으로 따옴표를 잘 써야하는데 저렇게 쓰는게 jsx언어 이고 자동으로 converting해주는게 react-app이다.
## 2. jsx
* javasript XML
* HTML과 유사하게 하게 정의된 구문을 사용

## 2-1. `<div>` wrapper
다음과 같이 div element 를 wrapper 로 사용해야 오류가 발생하지 않는다.
```jsx
    return  (
        <div>
            <h1> Hello World </h1>
            <h2> Welcome </h2>
        </div>
    );
```

## 2-2. 변수 렌더링
javascript 변수 사용 시 {변수명} 를 사용하여 렌더링
```jsx
render(){
        let text = "React"
        return  (
            <div>
                <h1> Hello</h1>
                <h2> Welcome to {text}</h2>
            </div>
        );
    }
```

 var 변수의 scope는 기본적으로 함수 단위인데 let 은 블럭 범위 내에서 변수를 선언한다.

 ## 2-3. method
{this.hello} 를 통해 버튼이 클릭되면 해당 메소드가 실행되게 할 수 있다.  () 가 뒤에 안붙어있다는점을 주의해주세요. `만약에 () 가 붙으면 페이지가 로드 될때도 실행되고, 클릭할때도 실행된다.`
 ```jsx
    hello(){
       alert("helloReact");
    }

    render(){
        return  (
            <div>
                <button onClick={this.hello}>Click Me</button>
            </div>
        );
    }
 ```
## 2-4. if-else 사용불가
```jsx
<p>{1 == 1 ? 'True' : 'False'}</p>
```
if-else문은 로 대체

## 2-5. style - CamelCase
CamelCase로 써야한다.   
ex) 기존 backgrond-color -> backgroundColor 

```jsx
   render(){
        let pStyle = {
            color: 'aqua',
            backgroundColor: 'black'
        };

        return  (
            <div>
                <p style = {pStyle}>{1 == 1 ? 'True' : 'False'}</p>
            </div>
        );
    }
```


## 3. props
React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달합니다. 이 객체를 “props”라고 합니다.  
  
props는 사용자가 제품을 조작하는 장치이다.
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```


##  class 사용
```jsx
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

## state

* state는 props값에 따라 내부의 구현에 필요한 데이터


* 컴포넌트의 동작을 바꾸고 싶을 때 사용자에게 제공하는 게 props (태그의 속성에 해당하는)  
* 사용자는 props를 통해 컴포넌트를 조작가능하게 됨 - 사용자에게 중요한 정보   
* 사용자에게는 알 필요 없는 컴포넌트 내부적으로 사용되는 게 state  
component를 사용하는 외부의 props   
* props에 따라 컴포넌트를 실제로 구현하는 내부의 state정보   
* 이 둘은 철저하게 분리되어 있음( 사용(props)과 구현(state)은 분리 ! )   

컴포넌트가 실행될 때 제일먼저 constructor가 실행 되어 초기화 작업을 해준다.

* 내부적으로 사용하는 것은 state를 사용한다 !
* App을 호출하는 부분에서는 내부에 어떤 값이 있는지 알지 못하도록 철저히 숨기는게 중요하다.


* 상위의 state값을 하위 컴포넌트의 props값으로 전달함 -가능 !

* state의 값이 바끼면 그 state가지고 있는 컴포넌트의 렌더함수가 다시 호출, 그 하위의 컴포넌트의 렌더함수도 같이 호출됨

* -> props나 state의 값이 바끼면 화면이 다시 그려진다.


* 받는거에서는 props? state 다르게 호출!@!!!!!
* 전달과 받을 때 다르게 ! 
* 상위에서 전달 : {this.state.속성명}
* 하위에서 호출 : {this.props.전달해주는명}
```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

## 이벤트

이벤트 생성, 이벤트에 함수 생성
<Subject 
onChangePage = {function(){
    alert('hihihii');
}.bind(this)}>

props 에 전달 된 
