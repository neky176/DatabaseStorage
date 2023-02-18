

<br/>

# 소계/총계 함수
 ## [1) ROLLUP](#1-rollup-1)
 ## [2) CUBE](#2-cube-1)
 ## [3) GROUPING SETS](#3-grouping-sets-1)
 ## [4) GROUPING](#4-grouping-1)

<br/>
<br/>

---------------

<br/>

### 1) ROLLUP
 - ROLL_UP(A) : A 그룹핑 -> 합계
 - ROLL_UP(A, B) : A, B 그룹핑 -> A소계 / 합계
 - ROLL_UP(A, B, C) : A, B, C 그룹핑 -> (A소계, B소계) / 합계

<br/>
<br/>

```
SELECT ORDER_DT
     , MENU_NAME
     , SELLER
     , COUNT(*)
  FROM CAFE
--GROUP BY ROLLUP (ORDER_DT) 
--GROUP BY ROLLUP (ORDER_DT, MENU_NAME)
GROUP BY ROLLUP (ORDER_DT, MENU_NAME, SELLER)
;
```

<br/>

![rollup01](https://user-images.githubusercontent.com/80929909/219847909-682d7b02-beb5-4f92-80af-1e3a0836c1c7.png)

<span style='background-color:#548235'>`주문날짜에 대한 메뉴별 판매한 음료의 소계`</sapn>
`주문날짜에 대한 판매한 음료의 소계`

`총 판매한 음료의 합계`

</br>
</br>

---------------

</br>

### 1) CUBE
 - CUBE(A) : A 그룹핑 -> 합계
 - CUBE(A, B) : A, B 그룹핑 / A 그룹핑 / B 그룹핑 -> A소계, B소계 / 합계 
 - CUBE(A, B, C) : A, B, C 그룹핑 / A, B 그룹핑 / A, C 그룹핑 / B, C 그룹핑 -> (A소계, B소계), (A소계), (B소계) / 합계

<br/>
<br/>

```
SELECT ORDER_DT
     , MENU_NAME
     , SELLER
     , COUNT(*)
  FROM CAFE
--GROUP BY CUBE (ORDER_DT)
--GROUP BY CUBE (ORDER_DT, MENU_NAME)
GROUP BY CUBE (ORDER_DT, MENU_NAME, SELLER)
ORDER BY ORDER_DT
;
```
<br/>

![cube01](https://user-images.githubusercontent.com/80929909/219849664-593b6635-a0ab-40aa-bf80-a0090fdb19b7.PNG)

`주문날짜에 대한 메뉴별 판매한 음료의 소계`
`주문날짜에 대한 판매한 음료의 소계`

`메뉴별 판매한 음료의 소계`

`총 판매한 음료의 합계`

</br>

---------------

</br>

### 3) GROUPING SETS
 - GROUPING SETS(A, ()) : A 그룹핑 -> 합계
 - GROUPING SETS(A, B, ()) : A 그룹핑 / B 그룹핑 ->  합계 

<br/>
<br/>

```
SELECT ORDER_DT
     , MENU_NAME
     , SELLER
     , COUNT(*)
  FROM CAFE
--GROUP BY GROUPING SETS (ORDER_DT, ())
--GROUP BY GROUPING SETS (ORDER_DT, MENU_NAME, ())
GROUP BY GROUPING SETS (ORDER_DT, MENU_NAME, SELLER, ())
ORDER BY ORDER_DT, MENU_NAME, SELLER
;
```

<br/>

![groupingsets01](https://user-images.githubusercontent.com/80929909/219857435-0900330a-e7ef-4fae-b13c-01af40d88024.PNG)

`주문날짜별 판매한 음료 수`
`메뉴별 판매한 음료 수`
`판매자별 판매한 음료 수`
`총 판매한 음료의 합계`

</br>
</br>

### 4) GROUPING
 - ROLLUP, CUBE, GROUPING SETS 함수를 사용할 때 소계 자리에 NULL 대신에 텍스트를 쓸 수 있게 해주는 함수이다.

<br/>
<br/>

```
SELECT ORDER_DT
     , MENU_NAME
     , DECODE(GROUPING(SELLER), 1, 'TOTAL', SELLER) ASSELLER
     , COUNT(*)
  FROM CAFE
GROUP BY GROUPING SETS (ORDER_DT, ROLLUP(MENU_NAME, SELLER))
ORDER BY ORDER_DT, MENU_NAME, SELLER
;
```

<br/>

![grouping01](https://user-images.githubusercontent.com/80929909/219858081-c9df8716-450b-4ea4-9fdd-f6d5f14bd552.PNG)

`GROUPING을 이용하여  SELLER 컬럼부분에 NULL 대신 'TOTAL'이 출력됨을 확인 할 수 있다.`

</br>