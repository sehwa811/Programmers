## ✅

### 첫 번째 시도

```javascript
function solution(n, k) {
  const v = n.toString(k);
  return v.split("0").filter((item) => item !== "1" && item !== "").length;
}
```

### 두 번째 시도

```javascript
function solution(n, k) {
  const v = n.toString(k);
  return v.split("0").filter((item) => {
    if (item == "1" || item == "") return false;
    if (item !== "2" && item % 2 === 0) return false;
    else return true;
  }).length;
}
```

### 세 번째 시도(정답)

```javascript
function chkPrime(num) {
  if (num < 2) return false;
  if (num === 2) return true;
  for (var i = 2; i <= Math.sqrt(num); i++) {
    if (num % i === 0) return false;
  }
  return true;
}

function solution(n, k) {
  const v = n.toString(k);
  const filtered = v.split("0").filter((item) => {
    if (item == "") return false;
    if (chkPrime(parseInt(item))) return true;
  });
  return filtered.length;
}
```

- 소수인지 판별해주는 함수를 별도로 작성했다 : 제곱근 값 전까지만 계속 숫자를 증가하며 나눠보고 나머지가 0이 되면 소수가 아니므로 false 리턴하며 종료
- `숫자.toString(원하는 진수)` : 숫자를 특정 진수로 변환 + 문자열로 변환
- 테스트 케이스 1번이 9ms로 유독 매우 느리다
  <br>

### 다른 사람 풀이

```javascript
function isPrime(num) {
  if (!num || num === 1) return false;
  for (let i = 2; i <= +Math.sqrt(num); i++) {
    if (num % i === 0) return false;
  }
  return true;
}

function solution(n, k) {
  const candidates = n.toString(k).split("0");
  return candidates.filter((v) => isPrime(+v)).length;
}
```
- __문자열 앞에 +를 붙여주면 숫자가 된다! `parseInt`를 쓸 필요 없어진다__
