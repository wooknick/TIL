# 알고리즘 문제풀이에 도움되는 javascript 함수 모음

- [permutation](https://levelup.gitconnected.com/find-all-permutations-of-a-string-in-javascript-af41bfe072d2)

```javascript
const findPermutations = (string) => {
  if (!string || typeof string !== "string") {
    return "Please enter a string";
  } else if (string.length < 2) {
    return string;
  }

  let permutationsArray = [];

  for (let i = 0; i < string.length; i++) {
    let char = string[i];

    let remainingChars =
      string.slice(0, i) + string.slice(i + 1, string.length);

    for (let permutation of findPermutations(remainingChars)) {
      permutationsArray.push(char + permutation);
    }
  }
  return permutationsArray;
};
```

- combinations

```javascript
const combinations = (str) => {
  const fn = (active, rest, a) => {
    if (!active && !rest) return;
    if (!rest) {
      a.push(active);
    } else {
      fn(active + rest[0], rest.slice(1), a);
      fn(active, rest.slice(1), a);
    }
    return a;
  };
  return fn("", str, []);
};
```
