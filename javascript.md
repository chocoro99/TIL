# 템플릿 문자열

    var string1 = '안녕하세요';   
    var string2 = '반갑습니다';   
    console.log(string1 + ' '+ string2)   
    console.log(`${string1} ${string2}`)   

    var product = { name: '도서', price: "3000원" }
    console.log('제품 '+product.name+'의 가격은 '+product.price+'입니다')
    console.log(`제품 ${product.name}의 가격은 ${product.price}입니다`)

    var value1 = 1
    var value2 = 2
    console.log(`두 값을 더한 값은 ${value1+value2}입니다`)

# 전개 연산자
    var array1 = ['one', 'two']
    var array2 = ['three', 'four']
    var array3 = array1.concat(array2)
    console.log(array3)
    var array4 = [...array1, ...array2]
    console.log(array4)

    const(변수), let(상수)

# if. 조건문
    const a = 3;
    if(a + 1 == 2){
    console.log("True")
    }
    else if(a == 3){
    console.log("T")
    }
    else{
    console.log("False")
    }

# switch. 조건문
    const device = 'iphone'

     switch(device){
    case 'lgphone':
     console.log("LG")
     break;
     case 'iphone':
     console.log("아이폰")
     break;
    default:
    console.log("?")
    break;
    }

# for. 반복문
    for(let i=0; i<5; i++){
    console.log(i)
    }

    let i = 0;
    while (i < 5) {
    console.log(i);
        i++;
    }


    let numbers = [10, 20, 30, 40, 50];
    for (let number of numbers) {
    console.log(number)
    }

    const dog = {
    name: '멍개',
    sound: "멍멍",
    age: 5,
    }
    console.log(Object.entries(dog)) // 배열 변환
    console.log(Object.keys(dog)) // 키의 값을 배열로 가져옴
    console.log(Object.values(dog)) // 값을 배열로 가져옴

    for (let key in dog) {
    console.log(`${key}: ${dog[key]}`)
    }

# 클래스
    function Animal(type, name, sound){
        this.type = type;
        this.name = name;
        this.sound = sound;
        this.say = function(){
            console.log(this.sound)
        }
    }

    class Animal {
    constructor(type, name, sound) {
        this.type = type;
        this.name = name;
        this.sound = sound;
    }
    say() {
        console.log(this.sound)
    }
    }

    const cat = new Animal('고양이', '야옹', '냐웅')
    cat.say()

# 화살표 함수
    function add1(a, b) {
    return a + b;
    }

    const add2 = function(a, b) {
    return a + b;
    }
    console.log(add1)
    console.log(add2)

    const add3 = (a, b) => a + b;
    console.log(add1(2,3));
    console.log(add2(2,3));
    console.log(add3(2,3));

# 라이브러리 의존성 관리
HTML에 script 태그를 사용 -> import Module from ./module로 변함

# 배열 내장함수
    const hero = ['엔트맨', '닥터 스트레인지', '아이언맨']
    for(let i of hero){
      console.log(i)
    }
    hero.forEach(one => {
      console.log(one)
    })

    const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    const result_array = []
    array.forEach((a) => {
      result_array.push(a*a)
    })
    console.log(result_array)

    const result_map = array.map(n => n * n);
    console.log(result_map)

    let j = 0
    for (let i of array) {
    j = j + i
    }
    console.log(j)

    const result_reduce = array.reduce((total, num) => total + num, 0)
    console.log(result_reduce)

# 비동기 함수
    function work() {
    const start = Date.now()
    for (let i = 0; i < 10000000; i++) { }
    const end = Date.now()
    console.log(`${end - start}ms`)
    }

    function work2() {
    setTimeout(() => {
        const start = Date.now()
        for (let i = 0; i < 10000000; i++) { }
        const end = Date.now()
        console.log(`${end - start}ms`)
    }, 0)
    }

    function work3(callback) {
    setTimeout(() => {
        const start = Date.now()
        for (let i = 0; i < 10000000; i++) { }
        const end = Date.now()
        console.log(`${end - start}ms`)
        callback();
    }, 0)
    }

    console.log("시작")
    work3(() => {console.log("작업 끝")});
    console.log("끝")


    function todo1(onDone){
      setTimeout(() => onDone("작업1 끝"), 100);
    }
    function todo2(onDone){
      setTimeout(() => onDone("작업2 끝"), 200);
    }
    function todo3(onDone){
      setTimeout(() => onDone("작업3 끝"), 300);
    }

    todo1(function(message1){
      console.log(message1);
      todo2(function(message2){
        console.log(message2);
        todo3(function(message3){
          console.log(message3);
        })
      })
    })

    const todo1 = () => new Promise(resolve => {
    setTimeout(() => resolve("작업1 끝"), 100)
    })
    const todo2 = () => new Promise(resolve => {
    setTimeout(() => resolve("작업2 끝"), 200);
    })
    const todo3 = () => new Promise(resolve => {
    setTimeout(() => resolve("작업3 끝"), 300);
    })
    todo1().then(message1 => {
    console.log(message1)
    return todo2()
    })
    .then(message2 => {
        console.log(message2)
        return todo3()
    }).then(message3 => {
        console.log(message3)
    })
    
# 배열 추가, 삭제 함수
배열 추가 함수 - Array.push(), Array.unshift(), Array.splice()

Array.push()

    let arr = ['a', 'b', 'c'];
    arr.push('d');
    // arr = ['a', 'b', 'c', 'd'] 배열의 끝에 요소를 추가

Array.unshift()

    let arr = ['a', 'b', 'c'];
    arr.unshift('d');
    // arr = ['d', 'a', 'b', 'c'] 배열의 가장 앞에 요소를 추가

Array.splice(start, deleteCount, el)

    let arr = ['a', 'b', 'c'];
    arr.splice(2, 0, 'd');
    // arr = ['a', 'b', 'd', 'c']

배열 삭제 함수 - Array.pop(), Array.shift(), Array.splice()

Array.pop()

    let arr = ['a', 'b', 'c', 'e'];
    arr.pop();
    // arr = ['a', 'b', 'c']; 배열의 마지막 요소를 제거

Array.shift()

    let arr = ['a', 'b', 'c', 'd'];
    arr.shift();
    // arr = ['b', 'c', 'd'] 배열의 가장 앞에 있는 요소를 제거

Array.splice()

    let arr = ['a', 'b', 'c', 'd'];
    arr.splice(2, 1);
    // arr = ['a', 'b', 'd'] 인덱스 2부터 1개의 요소를 제거