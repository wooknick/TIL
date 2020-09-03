# 이항 계수 nCr mod p 구하기

1. O(nlgn) 알고리즘

페르마의 소정리를 이용함

> a^(-1) ≡ a^(p-2) (mod p)

nCr = n! / (n-r)!r! (mod p) 인데, 페르마의 소정리에 의해 아래가 성립함.

((n-r)!r!)^(-1) (mod p) = ((n-r)!r!)^(p-2) (mod p)

코드는 아래와 같음.

```javascript
const [N, R] = data[0].split(" ").map(Number);
const p = 1000000007n;

const fact = new Array(N + 1);
fact[0] = 1n;
fact[1] = 1n;

for (let i = 2; i <= N; i++) {
  fact[i] = (1n * (fact[i - 1] * BigInt(i))) % p;
}

const answer = (fact[N] * pow((fact[N - R] * fact[R]) % p, p - 2n)) % p;
console.log(answer);

function pow(a, b) { // a, b 는 BigInt
  if (b === 0n) {
    return 1n;
  } else if (b % 2n === 0n) {
    const t = BigInt(pow(a, b / 2n)) % p;
    return (t * t) % p;
  } else {
    const t = BigInt(pow(a, b / 2n)) % p;
    return (BigInt(a % p) * (t * t)% p)) % p;
  }
}
```

2. O(n) 알고리즘

> inv(1) = 1
> inv(i) = -(p / i) \* inv(p % i)

정수 i에 대해 i^(-1) mod p 를 구하고, 그 값을 이용해 i!^(-1) mod p를 구하는 전처리를 활용한 방식

[출처](https://lifeignite.tistory.com/43)

```javascript
const [N, R] = data[0].split(" ").map(Number);
const p = 1000000007n;

const fact = new Array(N + 1);
fact[0] = 1n;
fact[1] = 1n;
const invFact = new Array(N + 1);
invFact[0] = 1n;
invFact[1] = 1n;

for (let i = 2; i <= N; i++) {
  fact[i] = (1n * (fact[i - 1] * BigInt(i))) % p;
}
for (let i = 2; i <= N; i++) {
  invFact[i] = (-1n * (p / BigInt(i)) * invFact[p % BigInt(i)]) % p;
}
for (let i = 2; i <= N; i++) {
  invFact[i] = (1n * invFact[i - 1] * ((invFact[i] + mod) % mod)) % mod;
}

const answer = fact[N] * (invFact[N - K] % p) * (invFact[K] % p);
console.log(Number(answer % p));
```
