# 데이터 최대 값 또는 최소 값 가져오기

    SELECT MAX(컬럼) FROM 테이블;
    SELECT MIN(컬럼) FROM 테이블;

# 데이터의 갯수 구하기

    SELECT count(animal_id) from animal_ins

# 중복된 데이터 없이 조회하기

    SELECT distinct 컬럼 FROM 테이블

# max, min값을 가진 row의 다른 컬럼 값까지 출력하기

    SELECT * FROM 테이블 WHERE 컬럼 = (SELECT MAX(컬럼) FROM 테이블);
