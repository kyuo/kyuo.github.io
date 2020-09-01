# for-loop

WHY?

굳이 순수 for-loop를 쓸 이유가 있을까?

-> of, in, 내장함수 활용하기, 써야하면 주의해서 쓰자

## 1. Problem: for [condition] 계속 탐

```
for ([initialization]; [condition]; [final-expression])
   statement
```

다음 소스는 list.length를 계속 탄다

```js
var list = [1,2,3,4,5]
var len = ()=>{
    console.log('n번 참조')
    return list.length
}
for(var idx=0; idx<len(); idx++) {
    //doSomething(idx)
}
```

### 1.1. TODO: 변수 정의

```js
var list = [1,2,3,4,5]
var len = list.length
for(var idx=0; idx<len; idx++) {
    //doSomething(idx)
}
```

### 1.2. TODO: 변수 없애기

순서에 관계없으면 다음과 같이 가능

```js
var list = [1,2,3,4,5]
for(var idx=list.length; idx--; ) {
    //doSomething(idx)
}
```

### 1.3. TODO: of 키워드

```js
var list = [1,2,3,4,5]
for(var item of list ) {
    //doSomething(idx)
    console.log(item)
}
```


## 2 Problem: for 내 함수가 비동기일 경우

```js
var list = [1,2,3,4,5]
var main = function() {
    for(var idx=0; idx<list.length; idx++) {
        // doSomething(idx)
        setTimeout(function(){
            console.log(list[idx])
            console.log(idx)
        },1000*idx)
    }
}
main()

```

### 2.1. TODO: 함수

```js
function doSomething(i) {
    setTimeout(function(){
        console.log(i)
        console.log(list[i])
    },i* 1000)
}
var list = [1,2,3,4,5]
var main = function() {
    for(var idx=0; idx<list.length; idx++) {
        doSomething(idx)
    }
}
main()
```

### 2.2. TODO: 클로저

```js
var list = [1,2,3,4,5]
var main = function() {
    for(var idx=0; idx<list.length; idx++) {
        (function(i){
            setTimeout(function(){
                console.log(i)
                console.log(list[i])
            },i* 1000)
        })(idx)
    }
}
main()
```

### 2.3. TODO: let (Block-scope)

```js
var list = [1,2,3,4,5]
var main = function() {
    for(let idx=0; idx<list.length; idx++) {
        setTimeout(function(){
            console.log(idx)
            console.log(list[idx])
        },idx* 1000)
    }
}
main()
```

## 3. Problem: Array 다루기

```js
var list = [1,2,3,4,5]
for(var idx=0; idx<list.length; idx++) {
    //doSomething(idx)
}
```

### 3.1. TODO: Array 내장 함수

```js
var list = [1,2,3,4,5]
list.forEach((item, idx)=>{
    //doSomething(idx)
})
```

## 4. Problem: 유사배열

유사배열 처리할 때

```js
var nodes = document.querySelectorAll('a')
for(var idx=0; idx<nodes.length; idx++) {
    //doSomething(idx)
}
```

### 4.1. TODO: Array 내장 함수 활용

```js
var nodes = document.querySelectorAll('a')
Array.prototype.forEach.call(nodes, (node, idx)=>{
    //doSomething()
})
```


## Reference: 참고

[2.3. TODO: let (Block-scope)](https://stackoverflow.com/questions/31285911/why-let-and-var-bindings-behave-differently-using-settimeout-function)