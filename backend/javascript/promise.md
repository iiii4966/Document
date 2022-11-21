# Promise

- blocking 되지 않아도 되는 promise 함수 실행 시 반드시 catch chaning 을 걸고 에러를 로깅한다.
- 결괏값이 필요한 blocking promise 함수의 실행은 await 을 사용하고 try, except 를 사용하여 에러를 로깅한다.

```jsx
// not blocking function
async function foo(){
  return fetch(...);
}

function main(){
  foo().then(result => logger.info(result)).catch(err => logger.error(err));
}
```


```jsx
// blocking function
async function foo(){
  return fetch(...);
}

function main(){
	try {
		  const result = await foo();
	} catch (err) {
		logger.error(err);
		rethrow(err);
	}
}
```