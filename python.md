# sys.stdin.readline() 개행 문자 제거
strip()으로 개행 문자 제거  

    a = sys.stdin.readline().strip()

# 리스트 정렬 sort
기본 값은 오름차순 정렬, reverse 사용으로 내림차순 정렬  
   
    n = [1, 2, 5, 3, 4]  
    n.sort()  
    print(n) -> [1, 2, 3, 4, 5]  

    n.sort(reverse=True)  
    print(n) -> [5, 4, 3, 2, 1]

key값으로 정렬도 가능  
  
    s = ["생각한다", "나", "그리고", "너는"]  
    s.sort(key=len) -> 문자 길이로 정렬  
    print(s) -> ["나", "너는", "그리고", "생각한다"]

# List
append : 리스트에 추가 

    a = [1,2,3,4,5]  
    a.append(6)  
    print(a) -> [1,2,3,4,5,6]

del : 키워드로 삭제

    a = [1,2,3,4,5,6]  
    del a[1]  
    print(a) -> [1,3,4,5,6]

remove
 
    a = [1,2,3,4,5]  
    a.remove(5)  
    print(a) -> [1,2,3,4]

# print f"{}"
    a = 10
    print(f"오늘은 {a}일이다.") -> 오늘은 10일이다.

# join
"".join(리스트)를 하게 될 경우 리스트 내용물만 출력한다  

    a = [1,2,3,4,5]  

    result = ",".join(map(str,(a)))  
    print(result) -> 1,2,3,4,5

    b = ["b","c","a","d"]  

    result2 = "-".join(b)  
    print(result2) -> b-c-a-d

# find, index
공통점 : 찾는 문자의 위치를 찾아낸다.

.find( ) :

찾는 문자가 없는 경우에 -1을 출력한다.

문자열을 찾을 수 있는 변수는 문자열만 사용이 가능하다.  
리스트, 튜플, 딕셔너리 자료형에서는 find 함수를 사용할 수 없다.   
사용하게 되면 AttributeError 에러가 발생한다.

.index( ) : 

찾는 문자가 없는 경우에 ValueError 에러가 발생한다.

문자열, 리스트, 튜플 자료형에서 사용 가능하고 딕셔너리 자료형에는 사용할 수 없어 AttributeError 에러가 발생한다.

# 삼항 연산자
    a if a>b else b -> [on_true] if [expression] else [on_false]  
a가 b보다 클 때 a,  
b가 a보다 클 때 b

# count
    str = "Hello, Wordl"  
    str_count = str.count("o") -> str에서 문자 "o"의 개수를 셉니다  
    print(str_count) -> 2

# 대문자 소문자

string.upper() : 모든 문자를 대문자로 변환  

    str = "hi, python"  
    str_up = str.upper()  
    print(str_up) -> HI, PYTHON

string.lower() : 모든 문자를 소문자로 변환  

    str2 = "BYE, PythoN"  
    str2_low = str2.lower()  
    print(str2_low) -> bye, python

# round, ceil, floor, trunc
round(number[,ndigits]) : 반올림  

    round(1234.56) -> 1234  
    rount(1234.567, 2) -> 1234.57

ceil() : math 라이브러리를 사용하며 양의 정수 방향으로 올림한다.  

    import math  
    math.ceil(1.5) -> 2  
    math.ceil(-1.5) -> -1

floor() : math 라이브러리를 사용하고 ceil()과 반대로 음의 정수 방향으로 내림한다  

    math.floor(1.5) -> 1  
    math.floor(-1.5) -> -2

trunc() : math 라이브러리를 사용하고 소수점 아래는 다 버린다.  

    math.trunc(1.5) -> 1  
    math.trunc(-1.5) -> -1