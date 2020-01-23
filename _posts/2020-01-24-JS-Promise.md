---
layout: post
title:  "callback 지옥 탈출법 : Promise"
date:   2020-01-24 01:12:14 +0900
categories: [web]
tags: [JS]
---

# 오늘 배운 거 : callback 지옥을 해결하기 위한 방법 - Promise

https://ko.javascript.info/promise-basics#ref-59

```js
let promise = new Promise(function(resolve, reject) {
    // executor
    var r = do_something(args)
	if (r){
    	resolve(r);
	}
  	else{
        reject(r);
  	}
});
```

- executor는 promise 생성과 함께 실행된다.
- executor 에서 보통 시간이 걸리는 일을 수행하고 일이 끝나면 resolve나 reject함수를 호출한다.
- resolve나 reject를 호출하면 promise 객체의 상태가 변하고, 이는 바뀌지 않는다.
- reject에서는 Error객체를 보통 호출한다.

```js
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

// resolve 함수는 .then의 첫 번째 함수(인수)를 실행합니다.
promise.then(
  result => alert(result), // 1초 후 "done!"을 출력
  error => alert(error) // 실행되지 않음
);
```

- then의 첫번째 인수는 promise가 이행되었을 때(resolved) 실행되는 함수이다. 여기서는 result => alert(result)
- 두번째 인수는 reject되었을 때 실행된다.
- 에러가 발생한 경우만 다루기 위해서 catch를 사용함
  - `.catch(f)` 는 `.then(null,f)`과 동일
- finally
  - 항상 실행함
  -  다음 핸들러에 결과(result)와 에러(error)를 전달
  -  `.finally(f)` 호출은 `.then(f, f)`와 유사하나 이행/거부 여부를 모른다는 점이 다름

