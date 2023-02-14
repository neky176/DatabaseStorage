

<br/>

# 윈도우함수_순위함수
 ## [1) RANK](#---RANK)
 ## [2) DENSE_RANK](#---DENSE_RANK)
 ## [3) ROW_NUMBER](#---ROW_NUMBER)

<br/>
<br/>

---------------

<br/>

### 1) RANK
 - 순위가 같으면 같은 수 만큼 다음 순위를 건너뛴다.

<br/>
<br/>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , SUBJECT
     , SCORE
     , RANK()OVER(ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```
<br/>

![RANK01](https://user-images.githubusercontent.com/80929909/218761724-48211eb2-2294-4200-bb8f-3c3d92e882e0.PNG)

`컬럼에 정렬을 지정할 시 해당 컬럼 값에 NULL값이 있는 경우 NULL(무한의값)은 최대값으로 인식한다.`

</br>
</br>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , CLASS
     , SUBJECT
     , SCORE
     , RANK()OVER(PARTITION BY CLASS ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```
<br/>

![RANK02](https://user-images.githubusercontent.com/80929909/218761958-6d01704d-1d4a-4882-a46c-54fbe8ab18f6.PNG)

`CLASS별 점수를 내림차순한 순위를 구했다.`

---------------

</br>

### 2) DENSE_RAVK
 - 순위가 여러개가 같아도 바로 다움 순위의 값을 보여준다.

<br/>
<br/>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , SUBJECT
     , SCORE
     , DENSE_RANK()OVER(ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```
<br/>

![DENSE_RANK01](https://user-images.githubusercontent.com/80929909/218762316-73159a10-b35a-4a5b-9c48-09ce8d3c6e23.PNG)

</br>
</br>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , CLASS
     , SUBJECT
     , SCORE
     , DENSE_RANK()OVER(PARTITION BY CLASS ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```
<br/>

![DENSE_RANK02](https://user-images.githubusercontent.com/80929909/218762620-224733a9-4b12-41b4-bb63-5f0f7da83ede.PNG)

</br>

---------------

</br>

### 3) ROW_NUMBER
 - 같은 순위없이 차례대로 순위를 나열한다.

<br/>
<br/>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , SUBJECT
     , SCORE
     , ROW_NUMBER()OVER(ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```

<br/>

![ROW_NUMBER](https://user-images.githubusercontent.com/80929909/218762947-d42bf240-d883-4cbc-80d7-552dbe901285.PNG)

</br>
</br>

```
SELECT STUDENT_ID
     , STUDENT_NAME
     , CLASS
     , SUBJECT
     , SCORE
     , ROW_NUMBER()OVER(PARTITION BY CLASS ORDER BY SCORE DESC) AS RANK
  FROM SCHOOL
;
```
<br/>

![ROW_NUMBER02](https://user-images.githubusercontent.com/80929909/218763110-36d3cc8c-8192-4245-b0a4-89ffe7e2fea7.PNG)

</br>