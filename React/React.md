# React 기초
---
## 목차
- [React 기초](#react-%EA%B8%B0%EC%B4%88)
  - [리액트의 특징](#%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%9D%98-%ED%8A%B9%EC%A7%95)
    - [JSX 문법](#jsx-%EB%AC%B8%EB%B2%95)
    - [Component 기반](#component-%EA%B8%B0%EB%B0%98)
    - [Virtual DOM](#virtual-dom)
  - [리액트 처음이시라구요? React JS로 웹 서비스 만들기! 정리](#%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%B2%98%EC%9D%8C%EC%9D%B4%EC%8B%9C%EB%9D%BC%EA%B5%AC%EC%9A%94-react-js%EB%A1%9C-%EC%9B%B9-%EC%84%9C%EB%B9%84%EC%8A%A4-%EB%A7%8C%EB%93%A4%EA%B8%B0-%EC%A0%95%EB%A6%AC)
    - [data flow with Props](#data-flow-with-props)
    - [Lists with .maps](#lists-with-maps)
    - [Validating Props with Prop Types](#validating-props-with-prop-types)
    - [Component Lifecycle](#component-lifecycle)
    - [Practicing this setState](#practicing-this-setstate)
    - [Loading states](#loading-states)

---

## 리액트의 특징

### JSX 문법

JSX는 자바스크립트 안에서 HTML 문법을 사용해서 view를 구성할 수 있게 도와주는 자바스크립트 문법으로, 리액트 개발에 엄청난 도움을 준다.
```js
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}
```
코드안에 html 태그를 볼 수 있는데 이게 바로 JSX 이다. JSX없이도 리액트 개발을 할 수 있지만 마크업 개발은 하나의 div만 있는 것도 아니고 복잡할텐데, JSX 없이 사용하게 되면 개발자는 매우 힘들 것이다. 하지만 JSX의 사용으로, 리액트의 사용성은 굉장히 증가했다고 할 수 있겠고 대표적인 특징이 되었다.
### Component 기반

리액트는 컴포넌트 기반 라이브러리 이다.
컴포넌트 기반이라 함은 기존의 웹 페이지를 작성할 때 처럼 하나의 HTML 코드를 집어넣고 하는 것이 아닌, 여러 부분을 분할 해서 코드의 재사용성과 유지보수성을 증가시켜 준다.
### Virtual DOM

브라우저는 html를 읽어서 DOM 트리, CSS 트리를 만들고 DOM이 화면에 있어야할 위치를 잡고 거기에 그리고 색을 채운다.
여기 까지는 전혀 문제가 없다. DOM이 아무리 많던, 복잡하던 상관 없다. 브라우저는 위와 같은 일을 위해 만들어 졌기 때문이다.

하지만 여기 브라우저를 위협하는 요소가 생겼다. 예전과 같이 그냥 단순히 HTML을 서버에서 받아서 한번에 그리고 땡 하는것이 아니라. SPA(Single page application) 같은 것들이 생겨나면서, DOM을 수시로 변경해달라고 브라우저에게 요청한다.

노드가 1000개쯤(예를들어)있는 DOM 트리를 뒤져서 특정 노드를 찾아 width를 조금 넓혀주고 다시 CSS트리를 만들고 합치고, 화면에 스케치하고 색을 채운다. DOM 수정요청이 100번 온다면 브라우저는 위와 같은 일을 100번 한다.

즉 브라우저는 실시간 DOM 수정요청으로 그림을 다시 그리는데 효율적이지 못하다.

이런 브라우저의 단점을 도와주는 녀석이 가상돔(Virtual DOM)이다. 만약 100번의 DOM 수정 요청이 오면, 가상돔은 브라우저 대신 DOM 변경을 인지하고 그 내용을 가상돔에 반영한다.(아직 화면에 그리지 않음) 이 변화를 반영한 가상돔의 내용을 브라우저에게 전달하여 그리게 한다.(100번 그리던 것을 1번만 그린다.)

사실 가상돔(Virtual DOM)이라는 말이 어려워서 그렇지, 그냥 브라우저의 DOM과 렌더링을 위한 버퍼역할을 하는 것이다.

## 리액트 처음이시라구요? React JS로 웹 서비스 만들기! 정리
>[리액트 처음이시라구요? React JS로 웹 서비스 만들기!](https://www.inflearn.com/course/reactjs-web/dashboard) -인프런 강의를 보고 작성하였습니다.
>[소스코드](https://github.com/doohong/react_tutorial)
### create react app
페이스북이 제공하는 create react app을 이용하면 웹팩과 같은 툴을 사용할 필요 없이 손쉽게 리액트 앱을 만들어 준다.
create react app을 npm 이나 yarn 을 이용하여 설치하고 실행 시켜주면 아무런 설정 필요 없이 react app이 만들어지고 실행 시킬수 있다.
### Component
component는 각기 다른 function들과 method를 갖고 있다. 처음 생성된 앱의 흐름을 보면 index.js 에서 App이라는 컴포넌트를 index.html의 root라는 id를 가지고 있는 엘리먼트에 렌더 한다. 
우리는 App 컴포넌트에 다른 컴포넌트를 불러올 수 있으며 마지막엔 결국 ReactDOM을 이용하여 App 컴포넌트를 root에 렌더 한다.
**ReactDOM** 은 리액트를 웹사이트에 출력 하는걸 도와주는 모델이다. 리액트를 이용하여 웹사이트에 올리고 싶을때 ReactDOM을 이용하고 모바일 앱에 올려 놓고 싶을때는 ReactNative를 사용하면 된다.

Component 클래스는 항상 render() 메서드를 가지고 있어야 한다. 
```js
class App extends React.Component {
  render() {
    return (
      <div>
        기본적인 컴포넌트 구조
      </div>
    );
  }
}
export default App
```
return 에 JSX를 이용하여 렌더할 Html 코드를 입력하고 index.js에서 불러올 수 있도록 export를 해주면 된다.
### data flow with Props
리액트에는 2개의 주요 컨셉이 있다. 하나는 state 다른 하나는 props
부모 컴포넌트가 자식 컴포넌트에게 정보를 전달하는것이 props이다.
```js
const movies = [
    "스파이더맨",
    "알라딘"
]
class App extends React.Component {
  render() {
    return (
      <div>
        <Movie title={movies[0]} />
        <Movie title={movies[1]} />
      </div>
    );
  }
}
export default App
```
이렇게 부모 컴포넌트에서 movies라는 배열의 각 요소를 자식 컴포넌트에게 title이라는 키로 전달 할 수 있으며 꼭 {}를 써줘야 한다.
자식 컴포넌트에서는 {this.props.title}을 이용하여 title정보를 받을 수 있다.
```js
class App extends React.Component {
    render(){
        return  (
            <div>
                <Header title={ this.props.headerTitle }/>
                <Content title={ this.props.contentTitle }
                          body={ this.props.contentBody }/>
            </div>
        );
    }
}

App.defaultProps = {
    headerTitle: 'Default header',
    contentTitle: 'Default contentTitle',
    contentBody: 'Default contentBody'
};
```
위와 같이 부모 컴포넌트에서 App.defaultProps를 이용해 기본적으로 props를 설정해줄수있다.

또한 동적으로 값을 변경하고 싶은경우에는 props 대신 state를 사용하면 된다.
setState를 이용하여 기존의 값을 변경 시킬 수 있다.

### Lists with .maps
movies라는 배열의 각 요소를 한개씩 전달하였지만 실제 API를 호출해서 영화 정보를 받아올때는 몇개가 있을지 모르기 때문에 기존 방식으로는 문제가 있다.
해결하기 좋은 방법으로는 JavaScript의 map 메서드를 이용하는 방법이다. 
map은 말 그대로 1:1로 매핑을 시켜주는 메서드라 생각하면 좋다
> 배열.map((요소, 인덱스, 배열) => { return 요소 });
```js
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.map((v) => {
  console.log(v);
  return v;
});
```
위의 결과로는 콘솔에는 1 2 3이 찍히게 되고 result에는 배열이 그대로 나오게 된다.
map은 기존의 array를 변경시키는 것이 아니고 새로운 array를 만드는 것 이다.
```js
const movies = [
  {
    title: "스파이더맨"
  },
  {
    title: "알라딘"
  } 
]
class App extends React.Component {
  render() {
    return (
      <div>
        {movies.map(movie => {
         return <Movie title={movie.title} />
        })}
      </div>
    );
  }
}
export default App
```
위처럼 map을 통해 배열의 각 엘리먼트를 활용해서 새로운 array를 만든다. map 메서드는 (여기)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map]를 통해 확인할 수 있다.

### Validating Props with Prop Types
리액트는 엘리먼트가 많을 경우 Key라는 unique한 값을 부여해야 한다. 위에 예제의 경우는 map의 두번째 매개변수인 index를 이용하여 각각 고유한 키값을 부여할 수 있다.
```js
{movies.map(movie, index => {
         return <Movie title={movie.title} key={index} />
        })}
```
또한 자식 컴포넌트에서 전달받을 props에 원하는 타입을 지정할 수 있다.
위의 예제의 경우 Movie컴포넌트가 자식 컴포넌트이고 자식 컴포넌트에 propTypes를 설정하면 된다. 더이상 React.propTypes는 사용되지 않으므로 이방법을 이용하려면 yarn을 이용해서 prop-types를 설치해야 한다. 추가적으로 isRequired라고 작성하면 해당 prop은 제공하는 것이 필수로 설정된다.
```js
class Movie extends Component{
  static propTypes = {
    title: React.propTypes.string.isRequired
  }
}
```

### Component Lifecycle
컴포넌트는 여러 기능들을 정해진 순서대로 실행하는데 이것이 컴포넌트의 라이프 사이클이다. 
컴포넌트는 componentWillMount() -> render() -> componentDidMount() 이 순서대로 사용자가 원하든 원하지않든 사이클이 발생한다.  
각각의 메서드를 정의해서 console.log를 찍어보면 순서대로 발생하는것을 확인 할 수 있다.

컴포넌트가 처음 실행될 때 그것을 Mount라고 표현한다. 컴포넌트가 시작되면 우선 context, defaultProps와 state를 저장한다. 그 후에 componentWillMount 메소드를 호출한다. 그리고 render로 컴포넌트를 DOM에 부착한 후 Mount가 완료된 후 componentDidMount가 호출된다.

주의할 점은, componentWillMount에서는 props나 state를 바꾸면 안된다. Mount 중이기 때문이다. 그리고 아직 DOM에 render하지 않았기 때문에 DOM에도 접근할 수 없다.

componentDidMount에서는 DOM에 접근할 수 있다. 그래서 여기에서는 주로 AJAX 요청을 하거나, setTimeout, setInterval같은 행동을 한다.

정리하면 다음 순서로 실행된다.

1. state, context, defaultProps 저장
2. componentWillMount
3. render
4. componentDidMount

### Practicing this setState
페이지가 로드되고 난 후 일정시간 뒤에 작업이 일어나도록 하려면 setTimeout 을 이용하면 된다. 
영화가 후에 추가되거나 값이 변경되어 영화를 담고있는 state의 값을 변경시켜주려면 setState를 이용하면 된다.

페이지가 로드 된 후 영화를 한개 추가하고자 하면 setTimeout 안에 setState를 사용하면 된다.
```js
componentDidMount(){
    setTimeout({}=>{
        this.setState({
            movies:[
                ...this.state.movies
                {
                    title: "추가될영화"
                }
            ]
        })
    },1000)
}
```
위에처럼 작성하게 되면 1초뒤에 영화를 한개 생성한다. 만약 ...this.state.movies 이부분이 없다면 기존의 state.movies의 내용이 작성한 내용으로 덮어 씌여진다.

### Loading states
필요한 데이터가 항상 바로 즉시 존재하지는 않을 것이다.
데이터가 존재하지 않을때 데이터를 불러오면 에러가 발생할 것이다. 그런 일을 대비하여 데이터가 존재하지 않는 동안 기다리는 api콜을 타임아웃 기능으로 유사하게 구현 해 볼 것이다. 먼저 state는 비운 채로 시작한다.
```js
componentDidMount(){
    setTimeout({}=>{
        this.setState({
            movies:[
                {
                    title: "추가될영화"
                }
            ]
        })
    },1000)
}
 render(){
    return (
      <div className="App">
        {this.state.movies.map((movie,index) => {
        return <Movie title={movie.title} poster={movie.poster} key={index} />
         })};
      </div>
    );
  }
```
이렇게 되면 state.movies가 render 사이클에서 존재하지 않으므로 에러가 난다.
```js
 _renderMovies = () => {
  const movies =  this.state.movies.map((movie,index) => {
    return <Movie title={movie.title} key={index} />
  });
  return movies;
};
  render(){
    return (
      <div className="App">
        {this.state.movies ? this._renderMovies() : "Lodding"}
      </div>
    );
  }
```
위와 같이 작성하여 state.movies가 존재하는지 확인을 하고 존재할 경우 우리가 만든 _renderMovies()를 이용하여 영화를 화면에 띄워줄 수 있다.
리액트는 자체 기능이 많기 때문에 리액트 자체 기능과 내가 만든 기능을 구별해주기 위해 언더스코프를 메서드 앞에 붙이게 된다.
