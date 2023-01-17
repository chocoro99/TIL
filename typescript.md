# typescript Type

- 초기 지정된 타입 이외의 값을 넣으면 error가 생김

### 타입이 값에 따라 string으로 지정됨

        let a = "hello"

### 타입을 처음에 지정 가능

        let b : string = "hello"

### string이 아닌 number를 넣으면 에러 발생

        let b : string = "hello"
        b = 10

### 단 타입을 any로 넣으면 상관없음(javascript처럼 상관 x)

        let c : any = "hello";
        c = 10

### 배열도 마찬가지로 다른 타입의 값을 추가하면 에러 발생

        // let d:number[] = [10, 2, 5]
        let d = [10, 2, 5];
        d.push("hi")

### 객체도 타입 지정 가능

        const c :{home:string} = {
            home : "run"
        }

### 따로 타입을 묶어서 지정 가능

        type Home = {
            home : string
        }
        const d : Home = {
            home : "run
        }

### ?를 사용하면 값이 없어도 타입 지정 가능

        type Home = {
            home : string,
            study? : string
        }
        const e : Home = {
            home : "run"
        }

### readonly로 값 수정을 막을 수 있음

        type Home = {
            readonly home : string,
            study? : string
        }
        const f : Home = {
            home : "run"
        }
        f.home = "readonly" 값 수정이 안됨

### 함수도 타입 지정이 가능하다

        function g(value : string) : string{
            retunr value;
        }
        // 화살표 함수는 이렇게
        const g = (value : string) : string => {
            return value;
        }

### undefined로 타입, 값 지정

        let g : undefined = undefined;

### null도 타입, 값 지정

        let h : null = null;

### unknow 타입도 값도 지정 되지 않은 변수

        let i : unknown;

        // 타입이 string일 때 hello 값, number면 10
        if(typeof i === 'string') {
            i = 'hello';
        } else if(typeof i === 'number') {
            i = 10;
        }

### 에러 발생시키는 never 타입

        function j() : never{
            console.log("!.!")
            throw new Error("!.!")
        }
