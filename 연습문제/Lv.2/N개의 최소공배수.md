## ✅

```javascript
function solution(arr) {
    const m = Math.max(...arr);
    let k = 2;
    while (1) {
        if (arr.filter((e)=> (m * k) % e === 0).length === arr.length) return m * k;
        k++;
    }
}
```

### 헷갈렸던 부분
- `Math.max()`를 쓸 때 괄호 안에 배열을 바로 집어넣으면 안되고 스프레드 연산자로 풀어준 후 넣어야 한다
```
console.log(Math.max(1, 3, 2));
// Expected output: 3

console.log(Math.max(-1, -3, -2));
// Expected output: -1

const array1 = [1, 3, 2];

console.log(Math.max(...array1));
// Expected output: 3
```
- `filter` 메소드 쓸 때 처음에 `=== 0`을 안썼다

<br>

### 다른 사람의 풀이
```javascript
function nlcm(num) {
 return num.reduce((a,b) => a*b / gcd(a,b))  
}

function gcd(a, b) {
  return a % b ? gcd(b, a%b) : b
}
```
- 