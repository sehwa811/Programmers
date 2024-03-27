```javascript
function solution(citations) {
  citations = citations.sort((a, b) => b - a);
  let i = 0;
  while (i + 1 <= citations[i]) {
    i++;
  }
  return i;
}
```
- 인덱스를 하나씩 증가시키면서 오른쪽으로 순회하다가, 지금까지의 개수(인덱스 + 1)가 현재 요소의 값보다 큰 순간 멈춘다.

```javascript
const solution = (citations) =>
  citations.sort((a, b) => b - a).filter((el, idx) => el >= idx + 1).length;
```
