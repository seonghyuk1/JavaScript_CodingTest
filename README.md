# JavaScript_CodingTest

## 레벨0

https://velog.io/@tjdgur/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-Lv.0-%ED%86%B5%ED%95%A9%EC%A0%95%EB%A6%AC

## 레벨 0 정답률 60% 이하 문제

---
## 레벨1

```
[짝수와 홀수]
정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.

function solution (number) {
	return (number % 2 === 0 ? "Even" : "Odd")
}
```
 
 
 --- 
[평균 구하기]
 <br>
![image](https://user-images.githubusercontent.com/38232501/231174791-d3909686-c5e4-48d4-9e3e-7685d3a36809.png)

내 답
처음엔 나도 모르게 reduce의 존재를 떠올리지도 못한 채 for를 적고 있었다.. 뭐였지 하다가 map을 쓰려다가 그냥 reduce를 떠올리고 썼다

```
// reduce를 통해 다 더한 후 길이만큼 나눠주면 예상한 값이 나옴
function solution(arr) {
    return arr.reduce ((acc, cur) => acc + cur) / arr.length 
}
```

reduce 복습은 벨로그 
