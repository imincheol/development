JavaScript Array Functions 

## 자바스크립트 배열 함수 정리 기준
---
자바스크립트 배열에는 다양한 함수들이 들어 있습니다.
최근에는 이러한 함수를 사용하는 기법들이 많이 늘어나고 있는데요..

이 글에서는 자바스크립트 배열에 있는 함수들을 살펴보고 구분을 해보았습니다.

구분 기준은 크게 두가지로 "원본 배열 수정 여부"와 "반환값"이 무엇인가에 대해서 입니다.

1. 원본 배열 수정 
1.1 반환값이 없다 
1.2 원본 배열 반환 
2. 원본 배열을 수정하지 않음 
2.1 새로운 배열 반환 
2.2 하나의 값 반환 

위의 구분을 사용해서 자바스크립트 배열을 카테고리화 한 것을 살펴보시죠. 

- 아래의 예시에서 인자로 사용하는 함수 fn_xx 는 맨 아래에 설명해두었습니다. 

## 구분 
---
1. 원본 배열 수정 
   1. 반환값이 없다 
      - forEach( fn_i , thisValue ) 
      - reduce( fn_reduce, initValue ) 
      - reduceRight( fn_reduce, initValue )
   1. 원본 배열 반환 
      - fill( value, startIndex, endIndex )
1. 원본 배열을 수정하지 않음 
   1. 새로운 배열 반환 
      - map( fn_v , thisValue ) 
      - filter(fn_tf, thisValue) 
   1. 하나의 값 반환 
      - every( fn_tf, thisValue )  
      - find( fn_tf, thisValue ) 
      - findIndex( fn_tf, thisValue )

## 내용
---
1.1   원본 배열을 수정하지만 값을 반환하지는 않는다 


forEach( fn_i , thisValue ) 

- for 대신 forEach를 사용해서 각 요소를 순회할 수 있다. 
  하지만 continue 또는 break 를 사용하려고 하면 어떻게 해야할까? 
  그때는 아래에 나오는 every 함수를 사용하면 된다.

- 수행 : 배열의 각 요소를 돌면서 함수 fn 을 수행한다 
- return : 없음 

```js
var result = 0;
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.forEach( currentValue=> { result += currentValue; } );

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // undefined
result // "0abc0123"
```
---
 
reduce( fn_reduce, initValue ) 
-  수행 : 왼쪽에서 오른쪽으로 순회하면서 fn_reduce 함수를 통해 모든 값을 누적하여 계산한다 
- 인자 : initValue 초기값으로 설정하는 값. 없으면 0 
-  return : 없음 
```javascript
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.reduce( (total, currentValue)=>{ return total + currentValue} );

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // "abc0123"
```
---
 
reduceRight( fn_reduce, initValue )
- 수행 : 오른쪽에서 왼쪽으로 순회하면서 fn_reduce 함수를 통해 모든 값을 누적하여 계산한다 
- 인자 : initValue 초기값으로 설정하는 값. 없으면 0 
-  return : 없음 
```javascript
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.reduceRight( (total, currentValue)=>{ total + currentValue} );

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // "6cba"
```
---
 

#### 1.2 원본 배열 반환 

fill( value, startIndex, endIndex )
- 수행 : 원본 배열을 value 값으로 채워넣는다.
- 인자 : startIndex 이상 endIndex 미만까지 변경한다. 없을 경우 모든 요소를 변경한다. 
-  return : 원본 배열 Source Array
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.fill( "xx", 2, 5 );

aa // (8) ["a", "b", "xx", "xx", "xx", 1, 2, 3]
bb // (8) ["a", "b", "xx", "xx", "xx", 1, 2, 3]
```
---
 
### 2. 원본 배열을 수정하지 않음 
#### 2.1 새로운 배열 반환 
map( fn_v , thisValue ) 
-  수행 : 배열의 각 요소를 돌면서 함수 fn 을 수행하여 return 되는 결과들의 모음을 새로운 배열로 반환한다 
-  return : 새로운 배열 New Array
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.map( currentValue => { return currentValue + 9 });

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // (8) ["a9", "b9", "c9", "9", 9, 10, 11, 12]
```
---
 
filter(fn_tf, thisValue) 
- 수행 : 배열의 각 요소를 돌면서 함수 fn_tf 의 결과가 true 인 배열을 모아 반환한다 
- return : 새로운 배열 New Array
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.filter( currentValue => { return typeof currentValue == "string" });

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // (4) ["a", "b", "c", ""]
```
---
 
2.2 하나의 값 반환 
every( fn_tf, thisValue )  
-  처음부터 끝까지 모든 요소에 대해서 fn_tf 함수를 수행하지만 
  중간에 결과가 false 가 나온다면 그 시점에서 멈추게 된다. 
  따라서 forEach로는 구현하지 못하는 continue(true) 또는 break(false)를 사용한 것처럼 사용이 가능하다 
-  수행 : 모든 배열의 요소에 대하여 함수 fn_tf  의 결과가 모두 true 이면 true 값을 반환한다 
-  return : Boolean 
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.every( currentValue => { return typeof currentValue == "string" });

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // false
```
---
 
find( fn_tf, thisValue ) 
-  수행 : 함수 fn 의 결과가 true가 나오는 첫번째 요소의 value 반환
-  의미 : 배열에서 조건에 맞는 요소의 값을 찾으려고 할때 사용 
-  return : Value
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.find( currentValue => { return typeof currentValue != "string" });

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // 0
```
---
 
findIndex( fn_tf, thisValue )
-  수행 : 함수 fn 의 결과가 true가 나오는 첫번째 요소의 index 반환
-  의미 : f배열에서 조건에 맞는 요소의 인덱스를 찾으려고 할때 사용 
-  return : index
```js
var aa = ["a", "b", "c", "", 0, 1, 2, 3];
var bb = aa.findIndex( currentValue => { return typeof currentValue != "string" });

aa // (8) ["a", "b", "c", "", 0, 1, 2, 3]
bb // 4
```
---
 
## fn 함수 

함수들을 카테고리화하여서 사용할때 인자로 사용한 fn_xx 함수들에 대해서 정리 및 요약 

### fn_i( currentValue, index, arr ) { }
---
- 입력 
  -  currentValue 현재 순회하는 요소의 값 
   - index 현재 순회하는 요소의 인덱스 
  - arr 원본 배열 참조 
- 출력
   - `없음` 
 
### fn_tf( currentValue, index, arr ){ return Boolean; }
---
- 입력 
  - currentValue 현재 순회하는 요소의 값 
  - index 현재 순회하는 요소의 인덱스 
  - arr 원본 배열 참조 
- 출력 
  - `Boolean 반환  `
 
### fn_v( currentValue, index, arr ){ return value; }
---
- 입력 
  - currentValue 현재 순회하는 요소의 값 
  - index 현재 순회하는 요소의 인덱스 
  - arr 원본 배열 참조 
- 출력 
  - `값 반환`
---
