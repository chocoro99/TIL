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
