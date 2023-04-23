# JavaScript_CodingTest

## 레벨0

https://velog.io/@tjdgur/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-Lv.0-%ED%86%B5%ED%95%A9%EC%A0%95%EB%A6%AC

## 레벨 0 정답률 60% 이하 문제
---
### [분수의 덧셈] 
<br>
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

### [다항식 더하기]
<br> 
![image](https://user-images.githubusercontent.com/38232501/233769610-78260094-4f69-4761-9cb2-0c2be5883415.png)


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

### [최빈값 구하기]
<br>
![image](https://user-images.githubusercontent.com/38232501/233836847-faa094f6-2298-41ea-9d11-28e6ba9967ab.png)


```
function solution(array) {
    // answer: 최빈값을 저장하는 변수로
    // repeatCnt: 현재까지의 최대 등장 횟수를 저장하는 변수로, 초기값은 0으로 설정합니다.
    // before: 이전 원소의 값입니다. 반복문에서 현재 원소와 비교하기 위해 사용됩니다. 
    // cnt: 현재 원소의 등장 횟수를 저장하는 변수입니다. 초기값은 0으로 설정합니다.
    // isdup: 최빈값이 여러 개인지를 나타내는 플래그 변수입니다. 초기값은 false로 설정합니다.
    
     answer = 0 
     repeatCnt = 0 
     before = 0
     cnt = 0;
     isdup = false
    
    array = array.sort((a,b)=>a-b)

    for( i=0;i<array.length;i++)
    {   
        // 현재 숫자와 이전 숫자가 같지 않다면 cnt = 1
        // 즉, 새로운 숫자 카운트 시작 
        if (before != array[i]) {
            cnt=1
        }
        // 이전 숫자와 현재 숫자가 같으면 cnt+1
        else {
            cnt+=1
        }
        
        // 현재 원소의 등장 횟수가 여태 가장 컸던 반복수 크다면
        if(cnt > repeatCnt){
            // 현재 반복중인 원소의 반복수를 가장 컸던 반복수로 지정
            repeatCnt = cnt
            // 현재 역대급 반복수를 return 값으로 지정 
            answer = array[i]
            
            isdup = false
        }
        
        // 현재 반복하고 있던 수가 여태 가장 컸던 반복수랑 같다는 것은
        // 같은 반복수를 가졌다는 말
        // 그렇기 때문에 isdup을 true로 바꿔 -1을 리턴
        if(cnt==repeatCnt){
            // 현재 반복값이 아까 역대급 반복수랑 같지 않다면
            // 즉, 값은 다른데 반복수는 같은 경우 
            if(answer!==array[i])
                isdup=true
        }
        
        // 인덱스값을 before에 넣어줘서 
        // 다음 차례 때 비교할시 활용
        before = array[i]
    }
    
    if (isdup) {
         return -1
    }
    else {
        return answer; 
    }

}
```

### [OX퀴즈]
<br>
![image](https://user-images.githubusercontent.com/38232501/233836859-8b947def-d94d-4c9c-8d94-e22639a6e0f7.png)

```
function solution(quiz) {
    var answer = [];
    return quiz.map(t => {
        const [calc, result] = t.split(' = ');
        const sign = calc.includes('+') ? 1 : -1
        const [a, b] = calc.split(sign === 1 ? ' + ' : ' - ');

        return +a + (+b * sign) === +result ? 'O' : 'X'
    });
}
```

return 시엔 양수로만 계산하되 사인을 곱해주는 형식으로 하셨다.
split을 할 떄마다 비구조화 할당으로 배열에 넣어주는 것이 참 참신

여기서,
a와 b 그리고 result애 +를 붙여준 것은 문자를 '정수'로 만들기 위해서이다.


[다음에 올 숫자] <br>
![image](https://user-images.githubusercontent.com/38232501/233839857-f82563d5-302b-4a50-b7bf-eb82fc3e3816.png)

```
function solution(common) {
    // 공차수열 인지 공비수열인지를 파악하려면
    // 적어도 3개 이상의 원소가 필요하다.

    // 공차수열은 하나 떨어진 원소간의 차는 전부 같다.
    
    if (common[2] - common[1] === common[1] - common[0]) {
        return common.pop() + common[1] - common[0]
    } else {
        return common.pop() * (common[1] / common[0]);
        
    }
    
}
```












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
