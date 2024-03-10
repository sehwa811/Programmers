### 첫 시도

```javascript
function solution(s) {
  var answer = "";
  const arr = s.split(" ");
  const u = arr.map((e) => e[0].toUpperCase());

  return answer;
}
```
- map 메소드 잘못 사용
  - map을 이렇게 쓰면 그냥 첫글자들만 남음

### 두 번째 시도

```javascript
function solution(s) {
  const arr = s.split(" ");
  const u = arr.map((e) => e[0].toUpperCase() + e.slice(1).toLowerCase());
  return u.join(" ");
}
```

- 런타임 에러
  - 원인: 공백이 연속해서 나올 경우 e[0]가 undefined일 수 있다. 그때 `toUpperCase()` 메소드를 쓰면 런타임 에러가 난다
- 문제 잘못읽음
  - 뒤에 문자들 소문자로 바꾸는 거 고려 안함

### 해결

```javascript
function solution(s) {
  const arr = s.split(" ");
  const u = arr.map(
    (e) => e.charAt(0).toUpperCase() + e.slice(1).toLowerCase()
  );
  return u.join(" ");
}
```

### 주의할 점
- __`chartAt()`__
  - 문자열에서 특정 문자를 추출할 때, `chartAt`과 숫자 인덱싱 사이에는 결과에 차이가 있다!
  - 만약 e가 공백(' ')일 경우, e[0]은 undefined 이지만 `e.chartAt(0)`은 '' 이다.

