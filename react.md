# React.createElement

    const 이름 = React.createElement(html태그, 태그의 속성, 내용)

    const span = React.createElement(
      "span",
      {
        onMouseEnter: () => console.log("mouse enter"),
      },
      "Total clicks: 0"
    );
    ReactDom.render(span, 위치(root));

# JSX

- JavaScript를 확장한 문법
- 브라우저에서 실행하기 전에 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환된다.

      // JSX로 작성
      const div = () => {
       <div>hi, jsx</div>
      }

      // JSX로 작성한 코드가 아래처럼 변환
      const div = () => {
      React.createElement("div", null, "hi, jsx");
      };

- 반드시 부모 요소 하나가 감싸는 형태여야 한다.

      // 올바르지 않은 코드
      function App(){
        return(
          <div>hi</div>
          <div>JSX</div>
        )
      }

      // 올바른 코드
      function App(){
        return(
          <div>
            <div>hi</div>
            <div>JSX</div>
          </div>
        )
      }

- 자바스크립트 표현식이 사용 가능하다 -> { }

      function App(){
        const message = "hi, JSX";
        return(
          <div>
            <div>{message}</div>
          </div>
        )
      }

# React State

- 컴포넌트 내부의 변경 가능한 데이터를 관리할 때 사용한다

      // message의 내용은 변하지만 화면은 변하지 않음
      function App(){
        let message = "hi, JSX";
        const bye = () => {
          message = "bye, JSX";
        };
        return(
          <div>
            <div>{message}</div>
            <button onClick={bye}>button</button>
          </div>
        )
      }

      // state 사용으로 화면까지 변함
      import {useState} from "react";
      function App(){
        const [message, setMessage] = useState("hi, JSX")
        const bye = () =>{
          setMessage("bye, JSX");
        }
        return(
          <div>
            <div>{message}</div>
            <button onClick={bye}>button</button>
          </div>
        )
      }

# React props

- 부모 컴포넌트가 자식 컴포넌트에게 값을 전달할 때 사용한다

      // props를 사용하여 <span>의 내용을 지정 가능
      const Hello = ({text}) => {
        <span{text}</span>
      }

      function App(){
        return(
          <Hello text="hi, props"/>
        )
      }

# React PropTypes

- 부모 컴포넌트에게 전달 받은 값의 데이터 type을 검사한다

      import PropTypes from "prop-types";

      const Hello = ({text}) => {
        <span>{text}</span>
      }

      // text의 type이 string 아닐 시 console에서 에러 메세지
      Hello.propTypes = {
        text : PropTypes.string
      }

      // 숫자 1을 넘겨서 console에서 에러 발생
      function App(){
        return(
          <Hello text={1}/>
        )
      }

# React Memo

    // 버튼을 누르면 내용이 변하는 코드로 렌더링이 몇 번 실행하는지 확인
    import {useState} from "react";

    const Btn = () => {
      console.log("렌더링")
      <button
      style={{
        background : color,
        color : "white",
      }}>
      {text}
      </button>
    }

    function App(){
      const [text, setText] = useState("hi, React")
      const bye = () => {
        setText("bye, React");
      }
      return(
        <Btn text={text} color="skyblue" click={bye}/>
        <Btn text="React.memo" color="pink"/>
      )
    }
    // 버튼을 누르기 전 console에서 확인한 렌더링 횟수는 2번
    // 버튼을 누른 후 렌더링 횟수도 2번으로 나온다

    // memo를 사용하여 렌더링을 내용이 바뀐 Btn만 실행하게 한다
    const Btn = () => {
      console.log("렌더링")
      <button
      style={{
        background : color,
        color : "white",
      }}>
      {text}
      </button>
    }

    const MemoBtn = React.memo(Btn)

    function App(){
      const [text, setText] = useState("hi, React")
      const bye = () => {
        setText("bye, React");
      }
      return(
        <MemoBtn text={text} color="skyblue" click={bye}/>
        <MemoBtn text="React.memo" color="pink"/>
      )
    }
    // 이렇게 되면 실행 시 렌더링 횟수가 3번으로 변한다

# React useEffect

- 리액트 컴포넌트가 렌더링마다 특정 작업을 실행하는 Hook이다
- 첫 인자는 함수, 그 다음은 배열이 들어간다 ( useEffect(함수, 배열) )

      import { useEffect, useState } from "react";

      function App(){
        const [message, setMessage] = useState("hi, JSX")
        const bye = () =>{
          setMessage("bye, JSX");
        }

        // 렌더링 마다 "useEffect 실행"이 console에 뜬다
        const check = () => {
          console.log("useEffect 실행")
        }
        useEffect(check, [])

        return(
          <div>
            <div>{message}</div>
            <button onClick={bye}>button</button>
          </div>
        )
      }

- 컴포넌트의 destroy 상황

      import { useEffect, useState } from "react";

      function Hello() {
        useEffect(() => {
          console.log("created :)");
          // Hello 컴포넌트가 사라지면서 발생
          return () => {
            console.log("bye :(");
          };
        }, []);
        return <h1>Hello</h1>;
      }

      function App() {
        const [bool, setBool] = useState(false);
        const btn = () => {
          setBool(!bool);
        };

        return (
          <div>
          // bool이 true일 때만 <Hello/>가 실행되고, false일 경우 null로 사라진다
            {bool ? <Hello /> : null}
            <button onClick={btn}>{bool ? "Hide" : "Show"}</button>
          </div>
        );
      }

# styled-components

- CSS in JS 기술을 사용하는 라이브러리로, CSS 파일을 따로 생성해 관리하던 것을 JS에서 CSS 코드를 작성한다

      import styled from "styled-conmponents";

      // <div>생성
      const Wrapper = styled.div`
        // css 코드
        width: 100vw;
        height: 100vh;
        background-color: black;
      `;
      const Title = styled.h1`
        color: blue;
      `;

      const App = () => {
        return(
          <Wrapper>
            <Title>styled-components</Title>
          </Wrapper>
        );
      };

# styled-components props 사용

    const Wrapper = styled.div``;

    // 아래와 같은 style이 겹치는 코드에 props를 사용한다
    const Box1 = styled.div`
      background-color: blue;
      width : 100px;
      height: 100px;
    `;
    const Box2 = styled.div`
      background-color: green;
      width : 100px;
      height: 100px;
    `;
    const App = () => {
      return(
        <Wrapper>
          <Box1 />
          <Box2 />
        </Wrapper>
      );
    };

    const Box = styled.div`
      background-color: ${(props) => props.color};
      width : 100px;
      height: 100px;
    `;

    const App = () => {
      return(
        <Wrapper>
          <Box color="blue" />
          <Box color="green" />
        </Wrapper>
      );
    };

# styled-components 상속

    const Wrapper = styled.div``;

    // 컴포넌트 상속 받기
    const Box = styled.div`
      background-color: blue;
      width : 100px;
      height: 100px;
    `;
    const Circle = styled(Box)`
      // Box의 스타일을 받고 추가적인 스타일 추가 가능
      border-radius: 50%;
    `;
    const App = () => {
      return(
        <Wrapper>
          <Box />
          <Circle />
        </Wrapper>
      );
    };

# styled-components as

    // Box 컴포넌트의 스타일을 사용하고 싶지만 다른 태그로 쓰고 싶을 때 as 사용
    const Wrapper = styled.div``;
    const Box = styled.div`;
      background-color: blue;
      width : 100px;
      height: 100px;

     const App = () => {
      return(
        <Wrapper>
          <Box as="input" />
        </Wrapper>
      );
    };

# styled-components attrs

- 컴포넌트에 attributes를 지정한다

      const Wrapper = styled.div``;

      // 이 컴포넌트를 쓰면 required:true가 적용된 상태로 사용된다
      const Input = styled.input.attrs({ required: true })`
        background-color: skyblue;
      `;

      const App = () => {
      return(
        <Wrapper>
        // 몇 개를 사용하든 똑같이 required: true가 적용
          <Input />
          <Input />
          <Input />
        </Wrapper>
      );

  };

# styled-components 자식 컴포넌트와 애니메이션

    const Wrapper = styled.div`
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    `;

    // styled-components에서 애니메이션을 사용할 땐 "keyframes"를 사용한다
    const rotationAnimation = keyframes`
      0% {
        transform: rotate(0deg);
        border-radius: 0px;
      }
      50% {
        transform: rotate(360deg);
        border-radius: 100px;
      }
      100% {
        transform: rotate(0deg);
        border-radius: 0px;
      }
    `;

    const Text = styled.span``;

    // 애니메이션이 적용 될 컴포넌트
    const Box = styled.div`
      width: 200px;
      height: 200px;

      // props로 background-color 받음
      background-color: ${(props) => props.color};
      display: flex;
      justify-content: center;
      align-items: center;

      // 위에서 생성한 애니메이션 적용
      animation: ${rotationAnimation} 5s linear infinite;

      // 부모 컴포넌트에서 자식 컴포넌트에게 적용시킬 style 작성
      ${Text} {
        color: white;

        // 자식 컴포넌트에게 hover 적용
        &:hover {
          color: yellow;
          font-size: 80px;
        }
      }
    `;

    const App = () => {
      return (
        <Wrapper>
          // props로 {color : green}을 보냄
          <Box color="green">
            // Text는 span 태그지만 as를 사용해 p태그로 사용 중
            <Text as="p">Hello</Text>
          </Box>
        </Wrapper>
      );
    };

# styled-components ThemeProvider

- Theme의 정보를 props 형태로 넘길 수가 있다 => 그로인해 공통적인 style 적용이 쉽다

      // index.js
      import { ThemeProvider } from "styled-components";

      // 두 가지의 Theme
      const darkTheme = {
        textColor: "whitesmoke",
        backgroundColor: "#111",
      };
      const lightTheme = {
        textColor: "#111",
        backgroundColor: "whitesmoke",
      };

      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(

        // props 형태로 theme를 보낸다
        <ThemeProvider theme={lightTheme}>
          <App />
        </ThemeProvider>
      );


      // App.js
      import styled from "styled-components";

      const Title = styled.h1`

        // 전달 받은 theme에서 textColor(#111)를 사용
        color: ${(props) => props.theme.textColor};
      `;

      const Wrapper = styled.div`
        display: flex;
        height: 100vh;
        width: 100vw;
        justify-content: center;
        align-items: center;

        // 전달 받은 theme의 backgroundColor(whitesmoke)를 사용
        background-color: ${(props) => props.theme.backgroundColor};
      `;

      const App = () => {
        return (
          <Wrapper>
            <Title>Hello</Title>
          </Wrapper>
        );
      };
