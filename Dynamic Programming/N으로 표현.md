- DP는 메모이제이션을 사용하는 기법이다
  - 이때 어떤 것을 메모할 것이냐 가 중요!

```javascript
const calculateFuncs = [(a, b) => a + b, (a, b) => a * b, (a, b) => a - b, (a, b) => Math.floor(a / b)];

function getCalculationResults(nth, dp, N) {
    let nthResults = new Set();
    nthResults.add(Number(String(N).repeat(nth)));
    
    for (let i = 1; i < nth; i++) {
        for (const calculateFunc of calculateFuncs) {
            for (const item1 of dp[i].values()) {
                for (const item2 of dp[nth - i].values()) {
                    const result = calculateFunc(item1, item2);
                    nthResults.add(result);    
                }
            }
        }
    }
    
    return nthResults;
}

function solution(N, number) {
    if (N === number) {
        return 1;
    }
    
    const dp = [];
    dp[1] = new Set([N]);
    
    for (let i = 2; i <= 8; i++) {
        dp[i] = getCalculationResults(i, dp, N);
                
        if (dp[i].has(number)) {
            return i;
        }
    }
    
    return -1;
}
```
- DP[k] = N의 숫자를 k번 연산해서 나온 결과값


### 몰랐던 메소드
- `String.repeat(n)` : String을 n번 반복하여 만든 새 문자열을 반환한다
  - 0을 넣으면 빈 문자열 ''을 반환한다



```javascript
function solution(N, number) {
    var answer = 0;
    var use = Array.from(new Array(9), () => new Set());
    if(N==number) return 1;
    else {
        use.forEach((element, index) => {
            if (index !== 0) element.add(Number(String(N).repeat(index)));
        });
        for(var i=1 ; i<=8 ; ++i) {
            for(var j=1 ; j<i ; ++j) {
                for(var first of use[j]) {
                    for(var second of use[i-j]) {
                        use[i].add(first+second);
                        use[i].add(first-second);
                        use[i].add(first*second);
                        use[i].add(first/second);
                    }
                } 
            }
            if(use[i].has(number)) return i;
        }
        return -1;
    }
    return answer;
}
```