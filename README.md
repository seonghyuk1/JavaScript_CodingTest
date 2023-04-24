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


### [다음에 올 숫자] 
<br>

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

### [연속된 수의합]
<br>

![image](https://user-images.githubusercontent.com/38232501/233851642-2295cdae-cca8-4477-a1e5-aba7be22371d.png)

총합을 수의 갯수를 나눈 것이 평균임을 활용하여 쉽게 풀었던 문제
평균값을 구해준 다음 공차가 1인 등차수열임을 활용하여 배열에 넣어준 후 return 하였다.

```
function solution(num, total) {
    ans = []; 
    
    num%2 === 0 ? 평균 = Math.floor(total / num)+1 : 평균 = Math.floor(total / num)
    
    for (i=0; i < num; i++) {
        ans.push((평균 - Math.floor(num/2))+i)
    }
    return ans 
}
```



### [겹치는 선분의 길이]
<br>

![image](https://user-images.githubusercontent.com/38232501/233851685-8a4d22cc-078c-4234-bafb-4ab075219c9a.png)

생각했던 풀이방법은 맞았지만 2차원 배열의 값들을 어떻게 선분에 표시하는지가 어려웠던 문제..
최소, 최대를 구하는 것이 아니라 각 속 배열의 좌측값과 우측값을 저장한 후
그 길이에 맞춰 0으로 채워둔 배열에 +1씩을 해주면 됐다..

```
function solution(lines) {
    const ans = new Array(200).fill(0)
    
    
    for (i=0; i<3; i++) {
        left = lines[i][0]
        right = lines[i][1]
        
        for(j=left; j<right; j++) {
            ans[j+100] += 1
        }
        
    }
    return ans.filter(v => v>=2).length
    
}
```

### 옹알이 (1) 

![image](https://user-images.githubusercontent.com/38232501/233972636-46b7320b-eeca-4801-912f-8f4a8b19702f.png)

<br>

내 풀이
처음엔 순열을 사용한 permute로 생각하여 모든 경우의 수를 다 구하려 해보고 거기에 match하는 애들만을 사용하려 했지만 코드를 짤수록 너무 비효율적인 것 같아서 여러 풀이를 찾아보았다.

```
function solution(babbling) {

    var 할줄아는말 = ["aya", "ye", "woo", "ma"];
    var 얘가한말 = "";
    var answer = 0;

    for(var i=0; i<babbling.length; i++) {
        // 애기가 하는 말의 각각을 문자열로 바꿔준 후
        얘가한말 = babbling[i].toString();
        
        for(var j=0; j<할줄아는말.length; j++) {
            // 얘가 하는 말들의 각각 (문자열)을 얘가 할줄아는말들과 같다면 다 공백으로 지워줌
            // 할줄아는 말의 각각을 돌기때문에 조합이 이상하지 않은 이상 조합이 다 공백으로 바뀜
            얘가한말 = 얘가한말.replaceAll(할줄아는말[j], ' ');    
        }
        
        // 그렇게 공백으로 바뀐 얘가 한 말 중에 공백을 다 지운 후 길이가 0인 애들의 갯수만을 return
        if(얘가한말.trim().length == 0) {
            answer++;
        }
    }

    return answer;
}
```

### 평행 
<br>

![image](https://user-images.githubusercontent.com/38232501/233854091-c419f26b-7002-4c16-b48e-23731f88afb4.png)

사실 소팅과는 상관없이 기울기를 구해주면 되는 문제
한참을 고민하다가 드디어 오랜만에 생각이 났는데
기울기는 x변화량과 y변화량으로 구한다

즉, y변화량 / x변화량인데 (다른 선분 변화량이 같는가를 보기위해)

길이가 정해진 dots이기에 함수를 구현해서 차이가 같은 것이 있다면 값을 올려주면 됐었다.
이 부분에선 너무 오랜만이라.. 결국 그래프도 직접 그려보고 하다가 다른 분의 코드를 참고 했다

```
function solution(dots) {
    answer = 0;
    
    // 기울기 y변화랑/x변화량
    sol(dots[0], dots[1], dots[2], dots[3]) 
    sol(dots[0], dots[3], dots[1], dots[2]) 
    sol(dots[0], dots[2], dots[3], dots[1]) 
    
    return answer>0 ? 1 : 0
}

function sol(a, b, c, d) {
    let abDiff, cdDiff;

    abDiff = (b[1] - a[1]) / (b[0] - a[0]);
    cdDiff = (d[1] - c[1]) / (d[0] - c[0]);

    if (abDiff === cdDiff) {
      answer += 1;
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
