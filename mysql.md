# 데이터 최대 값 또는 최소 값 가져오기

    SELECT MAX(컬럼) FROM 테이블;
    SELECT MIN(컬럼) FROM 테이블;

# 데이터의 갯수 구하기

    SELECT count(animal_id) from animal_ins

# 중복된 데이터 없이 조회하기

    SELECT distinct 컬럼 FROM 테이블

# max, min값을 가진 row의 다른 컬럼 값까지 출력하기

    SELECT * FROM 테이블 WHERE 컬럼 = (SELECT MAX(컬럼) FROM 테이블);

# 테이블 조회 정렬 ORDER BY

    오름차순
    SELECT * FROM 테이블 ORDER BY 컬럼 ASC(생략 가능);

    내림차순
    SELECT * FROM 테이블 ORDER BY 컬럼1 DESC;

# 특정 문자포함 검색 Like

    특정 문자로 시작하는 데이터 검색
    SELECT 컬럼 FROM 테이블 WHERE 컬럼 LIKE '특정 문자열%';

    특정 문자로 끝나는 데이터 검색
    SELECT 컬럼 FROM 테이블 WHERE 컬럼 LIKE '%특정 문자열';

    특정 문자를 포함하는 데이터 검색
    SELECT 컬럼 FROM 테이블 WHERE 컬럼 LIKE '%특정 문자열%';

# NULL 값을 다른 값으로 변환 IFNULL

    SELECT IFNULL(컬럼,'값') FROM 테이블;
