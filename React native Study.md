리액트 네이티브(React Native) 스터디 내용


#   리액트 네이티브란 ?
리액트 + 네이티브
리액트를 이용해 모바일 네이티브 어플리케이션을 개발하는 기술
어플리케이션의 UI를 개발한다는게 좀 더 정확한 정의 인듯.

먼저 리액트가 무엇인지 알아야한다.

리액트 = 페이스북이 웹 개발을 쉽게 하기 위해 만든 기술이다. 커스텀 컴포넌트를 만들고 쉽게 조합해서 뷰를 쉽게 만들 수 있다.
Java Script를 이용해 개발한다.

리액티브는 리액트의 접근법을 네이티브 앱을 개발하기 위해 사용하는 것으로 자바스크립트로 구현하지만 크로스 플랫폼(ios,Android)을 동시게 개발 가능하게 한 오픈소스 프로젝트이다. (네이티브 위젯을 표시하지만 작업은 js로)

가장큰 장점은 개발 생산성이 좋다.
코드 작성이 쉽다(js를 모른느 나에겐 해당 안된다)
라이브 리로드.  - 수정사항을 빠르게 확인하기 쉽다 - 컴파일에 소요되는 시간이 적다.

단점으로는 비즈니스 로직이 복잡해지거나 액티비티 갯수가 많아지게 되면
네이티브 어플리케이션에 비해 속도가 느려진다 - 라이프 사이클과 관련한 기능 사용이 어렵다
vs 네이티브와 비교해서
네이티비는 액티비티 단위로 화면을 관리하며 적정 시점에 메모리를 비워주지만
리액트 네이티브는 전체 앱 단위로 화면이 중첩되면 모든 뷰를 들고있어 느려짐


※ios 커버를 위해서는 OS X가 필수적이지만 난 맥북이 없으므로 일단 윈도우에서 안드로이드 시험부터 해본다!


# 윈도우에 리액티브 설치하기

필요한 패키지 몇개가 있다.
jdk(오라클)
android sdk
(안드로이드 스튜디오 sdk manager이용 및 환경변수 설정)
npm(node.js 홈페이지에서 받는다)
다있겠지뭐

콘솔창에서 cmd 로 리액티브 설치
```
npm install -g react-native-cli
```

프로젝트 생성
```
react-native init 프로젝트이름
```
프로젝트 실행
```
프로젝트가 위치한 폴더로 이동
react-natvie run-android
```
디버깅
```
크롬 창에서 http://10.0.2.2:8081/debugger-ui 주소를 http://localhost:8081/debugger-ui 로 변경하고, 디바이스의 앱을 완전종료 시킨 뒤 앱을 재실행하면 정상적으로 나오게 됩니다.
(오른쪽 아래 사각형 버튼을 누르면 실행중인 앱이 나오는데 이곳에서 종료시켜줍니다.)
```


# Native(Java, Swift)로 개발한 컴포넌트 추가하기.

1. Github에 새로운 repo 생성 및 해당 repo 클론
2. 배포자 정보 설정 계정 추가
3. login
4. 생성한 repo 초기화
해당 repo 폴더 이동후
npm init

5. index.js 파일 생성 및 푸쉬

```
var { NativeModules } = require('react-native');
module.exports = NativeModules.RNAudioPlayer;
위의 코드는 RNAudioPlayer라는 이름으로 네이티브 모듈을 만들어서 RN의 패키지 리스트에 등록할 것이고 이를 JS쪽에 export한다는 의미입니다.
```
6. 안드로이드 네이티브 모듈 작성

7. npm publish로 모듈 배포

8. 사용할 프로젝트에서 install 및 링크
npm install --save react-native-sample-module
react-native link



# React의 Component 와 Props
Component = 단순하게 생각하면 하나의 UI 요소 ,UI를 독립적 재사용 가능하도록 각 부분을 분리한 요소
Props라는 형태를 이용해 입력을 받고 이 Props를 이용해 View를 구성하고  
화면에 나타나야하는 요소를 설명해놓은 React 요소를 Render에서 반환
js에서의 함수와같다

Component를 만드는 방법 2가지
JS function을 만들고 return으로 정의
ex)
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

ES6 클래스를 만들고 exntend로 React.Component후 render부분에서 정의  
ex)
```
export default class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

```
https://reactjs.org/docs/components-and-props.html#composing-components
컴포넌트 구성 및 추출 링크

* React의 모든 컴포넌트는 Props의 값을 수정하지 않는 순수한 함수여야 한다.
네트워크 응답 및 기타 다른 요소에 대한 응답으로 시간 경과에 따라 출력을 변경할 수있게합니다.
State는 React 구성 요소가 규칙을 위반하지 않고 사용자 동작,

#State
Props와 비슷하지만 Private하며 컴포넌트에 의해 완전히 제어되는것.
Classes로 정의되는 컴포넌트의 추가적인 특성중 하나이다.

EX)
RandomNumber.js
```
import React from 'react';
import ReactDOM from 'react-dom';


class RandomNumber extends React.Component {
    updateNumber(){
        let value = Math.round(Math.random()*100);
        this.props.onUpdate(value);
    }
    constructor(props){
        super(props);
        this.updateNumber = this.updateNumber.bind(this);
    }
    updateNumber 메소드가 state에 접근할수 있도록 바인딩

    render(){
        return (
            <div>
                <h1>RANDOM NUMBER: { this.props.number }</h1>
                <button onClick={this.updateNumber}>Randomize</button> //버튼 클릭시 updateNumber수행
            </div>
        );
    }

}

export default RandomNumber;
```
버튼 클릭시 updateNumber실행으로
랜덤 변수 생성
이후 해당값을 파라미터로 functio 형태의  prop실행하여 ,  parent 컴포넌트의 onUpdateㅇ실행

onUpdate: function 형태의 prop 으로서, parent 컴포넌트에 정의된 메소드를 실행 할 수 있게 합니다.

App.js
```
import React from 'react';
import ReactDOM from 'react-dom';
import Header from './Header';
import Content from './Content';
import RandomNumber from './RandomNumber';

class App extends React.Component {

    constructor(props){
        super(props);

        this.state = {
            value: Math.round(Math.random()*100)
        };       //value값을 state로 지정 및 default값 지정

        this.updateValue = this.updateValue.bind(this); / /updateValue에서 state 접근할수 있도록 바인딩
    }

    updateValue(randomValue){    //randomValue를 value 값에 세팅해줌
        this.setState({
            value: randomValue
        });
    }   //하위 컴포넌트에서 넘겨운 randomValue로 setState로 value값을 없데이트


    render(){
        return  (
            <div>
                <Header title={ this.props.headerTitle }/>
                <Content title={ this.props.contentTitle }
                          body={ this.props.contentBody }/>
                      <RandomNumber number={this.state.value} //number에 state값인 value값 세팅
                                  onUpdate={this.updateValue} />  //onUpdate라는 prop에 updateValue라는 function형태의 prop 넘겨줌
            </div>
        );
    }
}

App.defaultProps = {
    headerTitle: 'Default header',
    contentTitle: 'Default contentTitle',
    contentBody: 'Default contentBody'
}; //default props값 세팅

export default App;
```
state 사용시 주의사항

바로 값을 ㅆ쓰지마라
// Wrong


```
this.state.comment = 'Hello';
```

setState사용
```
this.setState({comment: 'Hello'});
```

this.props 및 this.state가 비동기 적으로 업데이트 될 수 있으므로 다음 상태를 계산할 때 해당 값을 신뢰해서는 안됩니다.
//Wrong
```
this.setState({
  counter: this.state.counter + this.props.increment,
}); //이때 counter 값과 increment값이 연산중에 변할수도 잇다.
```
//Correct
```
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
or
```
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```
객체가 아닌 함수를 받아들이는 두 번째 형식의 setState ()를 사용하십시오.  
 이 함수는 이전 state를 첫 번째 인수로 받고, 두 번째 인수로 적용될 때의 props을받습니다.

setState는 모든 state를 한번에 merge시킨다.
따라서 개별로 setState하기 위해서는 setState call을 분리시킬 수도 있다.

ex)
```
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });

  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
```


#Component Life  ecycle

```
componentDidMount() {
  this.timerID = setInterval(
        () => this.tick(),
        1000
      );
} //컴포넌트의 출력이 DOM에 렌더링 된 후 실행.
//출력이 완료 된후 1초후 tick funcion 실행

componentWillUnmount() {
  clearInterval(this.timerID);
} //

```

# 웹에서 데이터 가져오기
Fetch API
Promise기반의 문법
ex)
```
fetch('http://url')
.then((respones) => respone.text())
.then((responseText) => {
  console.log(responseText)
  });
```


# JS 두꺼운 화살표 함수
화살표 함수는 익명 함수이기 때문에, 메소드가 아닌 함수에 사용하는 것이 적절합니다. 또한 익명 함수이기 때문에 생성자로 사용할 수 없습니다.

출처: http://beomy.tistory.com/19 [beomy]

함수 실행 콘텍스트 명확히 하기위해 bind 명력어 이용 특히 Callback시에
ex)
```
var callback = funcion(val){
  console.log('~~);
}.bind(this);

```
두꺼운 화살표 함수로 자동 바인딩
ex)
```
var callback  = (val) => {
  console.log('do somoe~~');
}
```
JS의 this 문법자바스크립트에는 4가지의 함수 실행 타입이 있기 때문이다.

js의 4가지 함수 실행방법

함수 실행: alert('Hello World!')  
메소드 실행: console.log('Hello World!')
생성자 실행: new RegExp('\d')
간접 실행: alert.call(undefined, 'Hello World!')

함수와 메소드의 차이는 객체의 멤버 객체의 여부
따라서 this사용시에 참조되는 객체가 전역 객체이냐 메소드를 가지고있는 객체이냐 차이
메소드를 파라미터로 사용할때는 this가 전역 객체를 가르킨다
but .bind로 this의 참조를 강제 시킬 수 있다.


# Promise 문법
https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
## Promise ?
js 비동기 처리에 사용되는 객체.

## Promise의 3가지 상태
1. Pending (대기)
비동기 처리 로직 아직 완료하지 않은 상태
```
new Promise();
대기상태
new Promise(function(resolve, reject){

});
```
2. Fulfilled (이행)
비동기 처리 로직 성공적으로 되어 결과 값 반환

```
new Promise(function(resolve, reject){
   resolve(data); > 성공했을때 실행  
});

getData.then({
  //성공했을때 수행
  });
```

3. Rejected (실패)
비동기 처리 로직 실패 or 오류

```
new Promise(function(resolve, reject){
   resolve(data); > 성공했을때 실행  
   reject(new Error("Request is failed"));  > 실패했을때.

});

getData.then().catch(funtion (err){
  //에러 수행
});

```


Promise없는 비동기 처리의 예
```
$.get('url', function (response) {
	parseValue(response, function (id) {
		auth(id, function (result) {
			display(result, function (text) {
				console.log(text);
			});
		});
	});
});
```
콜백지옥에 빠질수있다.

이를 위해 .then() 사용
ex)
```
function getData(callback) {
  // new Promise() 추가
  return new Promise(function (resolve, reject) {
    $.get('url 주소/products/1', function (response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function (tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
```
여러개 프로미스 연결하기
```
getData(userInfo)
  .then(parseValue)
  .then(auth)
  .then(diaplay);



  var userInfo = {
    id: 'test@abc.com',
    pw: '****'
  };

  function parseValue() {
    return new Promise({
      // ...
    });
  }
  function auth() {
    return new Promise({
      // ...
    });
  }
  function display() {
    return new Promise({
      // ...
    });
  }
```
#모바일 컴포넌트
HTML 기본 컴포넌트가아닌 React Native에서 제공하는 네이티브 ui엘리먼트를 기반으로 구성된 웹과는 다른 컴포넌트로 구성

컴포넌트의 color는 배경색이아니다
배경색을 사용하기 위해서는 backgroundColor사용
텍스트에서 color는 글씨색

flex, width, height로 크기조절
flex -  부모 컴포넌트에서의 상대적 비율을 정수로
width,height - 절대 크기, 상대크기 둘다 가능
 '숫자' or 'n%' 가능


## View

backgroundColor사용해 색상지정
색상값에 'rgba(52,52,52,0.8)'로 투명도도같이 설정가능
## Image

기본 사용방법
```
<Image source = {require("./ImagefileName.jpg")} />
//로컬에 저장된 이미지
<Image source = {require("./ImagefileName.jpg")}
        style =  {{width:400, height:400}}/>
        웹에서 불러올 경우 이미지 크기 선언필수
//웹이 있는 이미지
```
resizeMode속성으로 프레임안에 어떻게 렌더링 시킬지 결정가능
contain = 비율 유지 프레임 넘어가지 않게
cover = 비율 유지 꽉차게
stretch = 비율 무시 꽉차게


이미지이름.android.확장자
이미지이름.ios.확장자
이렇게 사용할 경우 플랫폼 별 이미지 로딩 가능
파일명 @2x, @3x 로 해상도별 이미지 렌더링도 가능
이미지의 스타일 속성


리액트 네이티브 5.0부터는 이미지 컴포넌트 하위에 자식 컴포넌트 추가 불가

따라서 배경으로 사용할 경우
<ImageBackground> 컴포넌트 사용



##TouchableHighlight

### What is ?
버튼이나 컨트롤 요소같이 사용자의 터치에 반응하는 엘리먼트는 보통 TouchableHighlight컴포넌트로 감싸져 있음
사용자에게 클릭시에 시각적 피드백을 준다.
### How To
사용자에게 클릭 시에 피드백을 주고싶은 컴포넌트를 TouchableHighlight로 감싸준다.
ex)
```
<TouchableHighlight
  onPressIn={this._onPressIn}
  onPressOut={this._onPressOut}
  accessibilityLabel={'PUSH ME'}
  style = {styles.touchable}>
  ///감쌀 뷰
  <Text styles={styles.buttonText}>
    {this.state.buttonState}
  </Text>
</TouchableHighlight>
```


TouchableOpacity이것도 많이 사용한다.
TouchableOpacity 클릭시 투명해지는 버튼
버튼도 Customize 위해서 기본 버튼컴포넌트의 속성일부를 덮어써 커스터마이징 가능하다.




## Text
일반 적인 TextBox
HTML처럼 em , strong등의 하위태그는사용 할수 없다.
대신 StyleSheet.create({
  // 해당 부분에 스타일을 기입해서 글자 마다 다른 스타일 기입가능
  });
가장 상위 텍스트 컴포넌트에 BaseText 스타일을 만들고 정의해줌으로써
한가지 폰트를 사용하는 것도 가능
```
import React, { Component } from 'react';
import { AppRegistry, Text, StyleSheet } from 'react-native';

export default class TextInANest extends Component {
  constructor(props) {``
    super(props);
    this.state = {
      titleText: "Bird's Nest",
      bodyText: 'This is not really a bird nest.'
    };
  }

  render() {
    return (
      <Text style={styles.baseText}>
        <Text style={styles.titleText} onPress={this.onPressTitle}>
          {this.state.titleText}{'\n'}{'\n'}
        </Text>
        <Text numberOfLines={5}>
          {this.state.bodyText}
        </Text>
      </Text>
    );
  }
}

const styles = StyleSheet.create({
  baseText: {
    fontFamily: 'Cochin',
  },
  titleText: {
    fontSize: 20,
    fontWeight: 'bold',
  },
});

// skip this line if using Create React Native App

AppRegistry.registerComponent('TextInANest', () => TextInANest);
```

fontweight, fondStyle 등의 속성 사용


재사용 가능한 이탤릭체 스타일과 컴포넌트 예시
```
class em extends Component{
  render(){
    return(
      <Text style= {styles.italic}>
        {this.props.Children} //컴포넌트의 하위 정보 참조
      </Text>
      );
  }
}
const styles = StyleSheet.create({
  italic:{
    fondStyle:"italic",
  }
});

```
이를 이용한 텍스트 입력 예시
```
<Text>
  React <Em>Natvie</Em>
</Text>
```
React Native는 트리에 속한 모든 텍스트 노드에 적용되는 기본 폰트 사용 X

이를 위해 스타일이 적용된 컴포넌트 사용 권장
처음에 기본적인 스타일을 가지고 선언을 한 후 재사용을 해야한다.
ex)
```
class MyApptext extends Component{
  render(){
    return(
      <Text style={styles.myapptextstyle}>
        {this.prop.Children}
      </Text>
      );
  }
}

const styles = StyleSheet.create({
    myapptextstyle :{
      fontFamily : 'fontname',
    }
  });
```

해당 컴포넌트 생성 후 Text 생성 사용시에 항상
가장 상위 노드에 해당 컴포넌트 적용

기본 폰트에서 변형된 스타일 적용시에는
해당 컴포넌트로 감싼 Text를 이용한 컴포넌트 생성

```
class HeaderText extends Component{
  render(){
    return(
      <MyApptext>
        <Text style = {{fontSize:20}>
        {this.prop.Children}
        </Text>
      </MyApptext>
      );
  }
}

const styles = StyleSheet.create({
    myapptextstyle :{
      fontFamily : 'fontname',
    }
  });
```

Text 내부의 모든 요소는 flexbox 레이아웃을 사용하지 않고 텍스트 레이아웃을 사용.
즉, <Text> 내부의 요소는 더 이상 직사각형이 아니며 줄의 끝을 볼 때 줄 바꿈됩니다.
View로 감쌀경우 텍스트가 줄의 끝부분일때 , 다음 컨테이너로 넘어갈때 두가지 모두
줄바꿈 but Text로 감쌀경우 줄의 끝부분에서만 줄바꿈 실행

### Text 컴포넌트의 속성
fontSize: 20,
fontWeight: 'bold',
fondtFamily: 'Cochin',
fontWeight: 'Bold',
color: 'red',
selectable : bool 타입 사용자가 텍스트를 선택하고 기본 복사본을 사용하고 기능을 붙여 넣을 수있게합니다.
accessibilityHint : ?  string 타입
accessibilityLabel : ? node 타입
accessible : bool타입
ellipsizeMode
nativeID
numberOfLines
onLayout
onLongPress
onPress
pressRetentionOffset
allowFontScaling
style
testID
disabled
selectionColor
textBreakStrategy
adjustsFontSizeToFit
minimumFontScale
suppressHighlighting

https://facebook.github.io/react-native/docs/text



##FlatList

##TextInput

##ScrollView


## Button



# 터치및 제스처 구성

## PanResponder
### What is
컴포넌트X
리액트 네이티브에서 제공하는 클래스
PanResponder gesture State를 통해 현재 제스처의 속도, 누적거리등 터치에 관한 정보 획득 가능.
### How to
객체 생성 + render 함수 결합
ex)
```
<View {...this._panResponder.panHandlers}>

</View>

//컴포넌트 생성시 실행  , panResponder 리스너 달아주기
componentWillUnmount(){
  this._panResponder = PanResponder.create({
    onStartShouldSetPanResponder :  this._handleStartShouldSetResponder// 리스너 달아줘서 해당 이벤트 발생시에 정의해놓은 함수 실행
    onMoveShouldSetPanResponder  : this._handleMoveShouldSetPanResponder//
    });
}
```
onStartShouldSetPanResponder
onMoveShouldSetPanResponder
onPanResponderGrant
onPanResponderMove
onPanResponderRelease
onPanResponderTerminate
6개이벤트 존재


# CSS flex
https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Flexbox%EC%9D%98_%EA%B8%B0%EB%B3%B8_%EA%B0%9C%EB%85%90
##flexbox란 ?
CSS 디자인 요소(컴포넌트)배치를 위한 인터페이스
flexbox를 1차원이라 칭하는 것은, 레이아웃을 다룰 때 한 번에 하나의 차원(행이나 열)만을 다룬다는 뜻입니다.

## flex의 주축과 교차축
flexbox에는 두개의 축이 있다 (교차축 , 주축)
주축 설정은 flex-direction 이며
- row
- row-reverse
- column
- column-reverse

row or row-reverse 는 주축은 인라인 방향 행을따른다.

column 과 column-reverse의 주축은 페이지 상단에서 하단으로 블록방향

교차축
주축에 수직

flex 요소를 정렬 끝을 맞추기 위해선 축 방향에 대한 이해 필요
주축, 교차축에 따라 항목 정렬, 끝을 맞주츤 속성 적용으로 레이아웃 구성

## flex 시작선과 끝선

쓰기방법을 가정하지 않는다. 과거 css처럼 왼쪽에서 오른쪽 , 위에서 아래로
가정하지 않는다.

축에 따라 바뀐다

주축이 row고 영어라면 주축시작선은 왼쪽끝 끝선은 올ㄴ쪽끝
아랍어라면 반대
둘다 가로쓰기이므로 교차축의 시작선은 위끝 끝선은 아래끝

##flex 컨테이너

flex박스가 놓여있는 영역을flex 박스라고 한다.
flex 컨테이너를 생성하려면 영역내의 컨테이너 요소의 display값을 flex혹은 inline-flex로 지정
 - 이건 web에서 사용할때

## 모바일에서 flexbox

기본적으로 웹과 다른점은 default flexdirection이 row가 아님 column으로 설정된다.
또한 flex의 파라미터는 single number만 지원한다,

flex의 요소들

1. flex-direction
가로축 세로축 방향
'column' , 'row'
default  = column

2. Justify Content
주축에 따른 Children 컴포넌트들의 배치 결정
주축의 시작 or 끝, 균등 한 간격 배부 결정
'felx-start' , 'center', 'flex-end' , 'space-around','space-between', 'space-evenly'
flex-start = 끝선 시작
center = 컴포넌트를 가운데 배치
flex-end = 끝선 기준
space-between = 양쪽정렬
ex) 3등분 시에 화면의 개체들간의 공백 똑같이

space-around = 공백있는 양쪽 정렬
ex) 3등분시에 화면을 3등분 한 후 각 부분에 가운데 정렬

space-evenly  =

3. Align Items
보조축에 따른 Component들의 배열 결정하는 요소
'flex-start','flex-end','center' , 'strech',baseLinie 으로 구성
flex-start =  좌측 시작점
center = 가운데
flex-end 우측끝점
stretch = 정렬방향의 크기지정 X시에 flex-start,부터 flex-end까지 쭉 늘리는 속성

http://yuddomack.tistory.com/entry/5React-Native-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-%EB%94%94%EC%9E%90%EC%9D%B8-2%EB%B6%80-%EB%B0%B0%EC%B9%98Flex-Direction%EC%99%80-%EC%A0%95%EB%A0%ACjustify-content-align-items?category=754156
//Align 가장 잘 적리함

//https://facebook.github.io/react-native/docs/layout-props
여기에 모든 컴포넌트 요소가 있다.
