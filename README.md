# JavaScript_CodingTest

## 레벨0

https://velog.io/@tjdgur/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-Lv.0-%ED%86%B5%ED%95%A9%EC%A0%95%EB%A6%AC

## 레벨 0 정답률 60% 이하 문제
---
[분수의 덧셈] <br>
![image](https://user-images.githubusercontent.com/38232501/233602930-216e64e0-c259-4e41-bb3a-09d72e2bd8e8.png)

```
function solution(numer1, denom1, numer2, denom2) {
   // // 최소 공배수 구하기
   // lcm = 1;
   // while(true) {
   //     if ( (lcm % denom1 === 0 ) && (lcm % denom2 === 0 )) break;
   //     else lcm++
   // }
   
   // 분모는 분모끼리의 곱
   y = denom1 * denom2
   // 분자는 대각선의 곱
   x = numer1*denom2 + numer2*denom1
	 
  
   // 기약분수로 만들기 위해 최대 공약수를 찾아줌
   maxNum = 0;
   for(i=1; i<=y;i++) {
       if(x%i === 0 && y%i ===0)
           maxNum = i
   }
	    return [x/maxNum, y/maxNum]
}
```
<br>

[다항식 더하기]

```
function solution(polynomial) {
    const arr = polynomial.split(" + ");
    
    
    const xNum = arr
                .filter(n => n.includes("x"))
                // ["3x","x"]
                // 만약 첫 번째 인수로 전달된 문자열이 없다면, 즉 "x"가 없다면 replace 메서드는 빈 문자열을 반환합니다.
                // 따라서 "3x" 문자열에서 "x"를 제거하면 "3"이 반환되며, "x" 문자열에서 "x"를 제거하면 빈 문자열("")이 반                 환됩니다. 이때 빈 문자열은 JavaScript에서 Falsy 값이므로 || 연산자의 오른쪽 피연산자로 간주되어 "1"
                // (or 연산자는 한 개가 false이면 나머지 한 개 true인 값을 찾아서 리턴하니까.)
                .map(n => n.replace('x', '') || '1')
                .reduce((acc, cur) => acc + parseInt(cur, 10), 0);
    const num = arr
                .filter(n => !isNaN(n))
                .reduce((acc, cur) => acc + parseInt(cur, 10), 0);

    let answer = [];
    // xNum이 1일 경우를 대비하여 공백으로 바꾸어줌
    if(xNum) answer.push(`${xNum === 1 ? "" : xNum}x`);
    if(num) answer.push(num);

    return answer.join(' + ')
}
```

|| or연산자에서
map을 통해 공백으로 다 바뀌었을 때, 공백값은 false라고 취급 되므로
or의 특성인 둘 중 한 개에 true인 값으로 return하기 때문에 '1'이라는 true값이 바뀌어 들어감

3x 같이 계수가 있는 경우에는 x가 지워진다하더라도 공백이 되지 않으므로 맞는 말

계수가 1일 때
게수가 1인 경우를 대비하여서 1일 땐 공백으로 바꾸어줌

parseInt
parseInt( ,10)을 통한 십진수 변환

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
