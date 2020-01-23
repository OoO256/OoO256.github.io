---
layout: post
title:  "JS Promise"
date:   2020-01-24 01:12:14 +0900
categories: [web]
tags: [JS]
---

# 오늘 배운 거 : JS Promise, 패스워드 저장법

1. 안전한 패스워드 저장방법

https://d2.naver.com/helloworld/318732?fbclid=IwAR109JZd7jNeGH8ltl7zEQRSZpILvZ8IwztNtwb9DxSyeZGEx2jdE4zEsRA



- 멋진 말을 배웠다 

  "보안 시스템은 가장 약한 연결 고리만큼만 강하다."

- 비밀번호를 평문으로 저장하면 안된다.

- digest : hash function의 결과를 의미한다

- avalanche : 입력 값의 일부가 변경되어도 다이제스트가 완전히 달라지는 hash 함수의 성질을 말한다.

- salting : 

  원본 메세지에 임의의 문자열(salt)을 추가하여 hashing하는것. Salt도 같이 DB에 저장한다. 패스워드가 고유의 솔트를 갖고 솔트의 길이는 32바이트 이상이어야 솔트와 다이제스트를 추측하기 어렵다.

- key stretching

  - brute-force attack으로 패스워드를 추측하는 데 많은 시간이 소요되도록
  - hashing을 많이 하는것
  - hash한 결과를 다시 hashing한다
  - ![password2](https://d2.naver.com/content/images/2015/06/helloworld-318732-2.png)



2. callback 지옥을 해결하기 위한 방법 : Promise

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

