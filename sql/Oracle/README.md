# Oracle SQL 실습 쿼리

## 2장 19p.
```
select name, tel, substr(tel, 1, instr(tel, ')')-1) as "지역번호"
from student
where deptno1 = 101;
```

## 2장 29p.
```
select name, jumin, replace(jumin, substr(jumin,7,7), '*******') as "주민"
from student
where deptno1 =101;
```

## 2장 30p.
```
select name, tel, replace(tel, substr(tel, 5, 3), '###') as "REPLACE"
from student
where deptno1 = 102;
```

## 2장 103p.
```
select name, birthday
from student
where to_char(birthday, 'mm') = '03';
```

## 2장 108p.
```
select name, to_char(hiredate,'yyyy-mm-dd') 입사일, to_char(pay*12, '9,999') as "연봉",
to_char((pay*12)*1.1,'9,999') as "인상후"
from professor
```

## 3장 37p.
```
select max(pay+nvl(bonus,0)) MAX, 
min(pay+nvl(bonus,0)) MIN, trunc(avg(pay+nvl(bonus,0)),1) AVG
from professor
```

## 3장 38p.
```
select max(nvl2(bonus,pay+bonus,0)) MAX, 
min(nvl2(bonus, pay+bonus,0)) MIN,
trunc(avg(nvl2(bonus, pay+bonus,0)),1) AVG
from professor
```

## 4장 37p.
```
select a.profno 교수번호, a.name 이름, a.hiredate 입사일, count(b.hiredate) "입사일 빠른수"
from professor a, professor b
where a.hiredate > b.hiredate
group by a.profno, a.name, a.hiredate
order by count(b.hiredate) asc;
```
