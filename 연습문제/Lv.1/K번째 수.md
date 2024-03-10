## ✅

### 첫 시도(실패)
```javascript
function solution(array, commands) {
  var answer = [];
  for (c of commands) {
    const sliced = array.slice(c[0] - 1, c[1] - 1);
    sliced.sort();
    answer.push(sliced[c[2] - 1]);
  }
  return answer;
}
```

위 코드를 제출하니 결과값이 [6, null, 3] 으로 출력되어 수정

### 두 번째 시도(통과)
```javascript
function solution(array, commands) {
    var answer = [];
    for (c of commands) {
        const sliced = array.slice(c[0] - 1, c[1]);
        sliced.sort((a, b) => a - b);
        answer.push(sliced[c[2] - 1])
    }
    return answer;
}
```

### 아이디어
- commands 내부를 for loop로 순환하며 각 요소에 대해 검사
- array를 자른다
- 자른 배열을 오름차순으로 정렬
- k번째에 있는 수를 찾아서 answer 배열에 push

### 주의할 점

- **sort()는 내부적으로 숫자를 문자열로 변환한 후 오름차순으로 정렬한다.**
  - [1, 100, 34, 4] 이 배열의 경우 정렬해보면 [1, 100, 34, 4] 라는 엉뚱한 결과를 얻는다.
  - [-3, 2, 0, 1, 3, -2, -1] 는 더 엉뚱하다. 마이너스 기호를 무시한채 [-1, -2, -3, 0, 1, 2, 3] 로 정렬된다.

__따라서 sort() 메소드는 콜백함수를 인자로 넣어주어야 제대로 쓸 수 있다.__

- 첫 번째 인자가 두 번째 인자보다 작으면 음수를 반환 -> 자리 교체 X
- 첫 번째 인자가 두 번째 인자보다 크면 양수를 반환 -> 자리 교체 O
- 첫 번째 인자가 두 번째 인자와 같으면 0을 반환
- 따라서 숫자 배열을 제대로 오름차순 정렬하기 위해서는 첫 번째 인자에서 두 번째 인자를 빼준다.
  `[-3, 2, 0, 1, 3, -2, -1].sort((a, b) => a - b);    // [-3, -2, -1, 0, 1,  2,  3]`
- 반대로 숫자 배열을 내림차순으로 정렬하고 싶다면 피연산자의 순서를 반대로!
  `[-3, 2, 0, 1, 3, -2, -1].sort((a, b) => b - a);    // [3, 2, 1, 0, -1, -2, -3]`

<br>

### 다른 사람 풀이

```javascript
function solution(array, commands) {
  return commands.map((command) => {
    const [sPosition, ePosition, position] = command; //구조분해할당
    const newArray = array
      .filter(
        (value, fIndex) => fIndex >= sPosition - 1 && fIndex <= ePosition - 1
      )
      .sort((a, b) => a - b);

    return newArray[position - 1];
  });
}
```

- 퀵소트 이용한 풀이

```javascript
function solution(array, commands) {
  var answer = [];

  for (var i = 0; i < commands.length; i++) {
    var temp = array.slice(commands[i][0] - 1, commands[i][1]);
    temp = quickSort(temp);
    var ans = temp.length != 1 ? temp[commands[i][2] - 1] : temp[0];
    answer.push(ans);
  }
  return answer;
}
```

```javascript
function quickSort(array) {
  if (array.length < 2) {
    return array;
  }
  const pivot = [array[0]];
  const left = [];
  const right = [];
  for (let i = 1; i < array.length; i++) {
    if (array[i] < pivot) {
      left.push(array[i]);
    } else if (array[i] > pivot) {
      right.push(array[i]);
    } else {
      pivot.push(array[i]);
    }
  }
  return quickSort(left).concat(pivot, quickSort(right));
}
```
