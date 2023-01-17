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

# typescript 다형성

        // 아래와 그 아래는 같은 내용
        type plusType = (a:number, b:number) => number;
        type plushType = {
                (a:number, b:number) : number
        }

### 다형성

        // (a:number, b:number) : number와 (a:number, b:string) : number의
        // 두 타입을 가질 수 있다
        type plusType = {
                (a:number, b:number) : number,
                (a:number, b:string) : number
        }

        const plus:plusType = (a, b) => {
                // b의 type이 number일 때 a+b를 리턴
                if(typeof b === "number") return a+b;

                // 아닐 땐 a만 리턴
                return a;
        }

### 받은 파라미터 개수에 따른 타입

        // a와 b 타입과 a, b, c 타입을 가지고 있을 때
        type addType = {
                (a:number, b:number) : number,
                (a:number, b:number, c:number) : number
        }

        // c를 받아도 안받아도 상관 없다면 c?:number를 사용
        const add:addType = (a, b, c?:number) => {
                // 이렇게도 가능하지만
                // if(typeof c === "undefined") return a+b;
                // return a+b+c

                // 간결하게 이렇게도 가능
                if(c) return a + b + c
                return a + b
        }
        // 실행
        add(1, 2)
        add(1, 2, 3)

### 제네릭

- 실행 시 타입을 지정한다

        type arrType = {
                // 둘 다 같은 내용이다
                // <T>(a:T[]) : void,
                <T>(a: Array<T>) : void
        }

        const arr:arrType = (a) => {
        console.log(a[0], a[1], a[2])
        }

        // 실행하여 숫자 배열이면 number[] 타입이 문자 배열이면 string[] 타입을
        // 불린 배열이면 boolean[] 타입이 지정된다
        arr([1, 2, 3])
        arr(['a', 'b', 'c'])
        arr([true, false, true])

        // 배열이 아닌 숫자나 문자, 불린의 경우
        type tempType = {
                // 이렇게 사용한다
                <T>(a: T) : void
        }
        const temp = (a) => {
                console.log(a)
        }

# 클래스

- 클래스

        class play{
                // this.a = a처럼 지정을 위해 타입 지정
                a: string;
                b: string;
                c: string;
                constructor(
                        a: string,
                        b: string,
                        c: string
                ){
                        this.a = a
                        this.b = b
                        this.c = c
                }
                say(){
                        console.log(this.a, this.b, this.c)
                }
        }
        const Play = new play("A", "B", "C")
        Play.say() // "A", "B", "C"

- 추상 클래스/ 추상 메소드와 접근 제어

        // 추상 클래스는 추상 메소드를 가지고 있어야함
        abstract class play{
                constructor(
                        // public 내부, 외부에서 접근 가능
                        public a: string,

                        // protected 내부, 자식까지만 허용 외부는 접근 불가능
                        protected b: string,

                        // private 내부에서만 접근 가능 자식, 외부는 접근 불가능
                        private c: string
                ) {}

                // 추상 메소드
                abstract sayHello(): string
        }

        class work extends play {
                sayHello() {
                return `${this.a}, ${this.b}`
                }
        }
        const Play = new work("A", "B", "C");
        console.log(Play.a); // "A"
        console.log(Play.sayHello()); // "A", "B"

# 인터페이스

        interface play {
        a: string;
        b: string;
        c: string;
        sayHello(): string;
        }

        // 인터페이스 사용 시 implements 써야 함
        class work implements play {
        constructor(
                public a: string,
                public b: string,
        ) {}
        sayHello() {
                return `${this.a}, ${this.b}`
        }
        }

        const Play = new work("a", "b")
        console.log(Play.a); // "a"
        console.log(Play.sayHello()) // "a", "b"
