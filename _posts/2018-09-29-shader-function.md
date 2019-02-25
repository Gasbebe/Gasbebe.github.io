---
layout: post
title: "02. 쉐이더 함수정리"
description: 쉐이더 함수정리
image: '\images\bg.jpg'
category: 'Shader'
tag:
 - Shader
 - Unity3D
 - HLSL
introduction: 쉐이더 함수정리
---



#  shader math function(수학함수)

수학함수

lerp(a,b, t) : 선형보간 함수 t는 0~1사의 값  0의 가까우면 a값에 가까워지고 1의 가까우면 b의 값의 가까워진다

```c++
lerp(1, 5, 0) // 1
lerp(1, 5, 0.5)// 3 
lerp(1, 5, 1)// 5
```

---

radians(x) : x의 라디안 값 반환 (60분법)

```c++
radians(180) // PI
radians(360) // 2PI
radians(1) // PI/180
```

---

saturate : 0 ~ 1 넘는 값을 잘라버리는 함수

```c++
saturate(10) // 1
saturate(0.5) // 0.5
saturate(0) // 0
saturate(-1) // 0
```

---

abs : 절대값을 반환하는 함수

```c++
abs(-10) // 10
abs(10) // 10
```

---

clamp(a, b, c)  : a  =  현재값,  b = 최소값,  c = 최대값, a를 b와 c의 값으로 범위를 제한 시킨다

```c++
clamp(10, 0, 5) //5
clamp(-1, 0, 5) //0
clamp(3, 0, 5) // 3
```

---

max(a,b) :  a와 b중에 큰 값 반환

```c++
max(10, 5)// 5
max(20, 10)// 10
```

---

min(a, b) : a와 b중에 작은 값 반환

```c++
min(-1, -3) // -3
min(-5, -10) // -10
min(5, 10) // 10
```

---

sign(x) : x에 대해 부호를 반환합니다 양수의 경우 1, 0의 경우 0, 음수의 경우 -1을 반환 합니다.

```c++
sign(-3) // -1
sign(0) // 0
sign(10) // 1
```

---

step(x,y) : x <= y 일때 1을 반환 아니면 0을 반환한다

```c++
step(10, 10) // 1
step(10, 9) // 0
step(9, 10) // 1
```

---

acos(x) : 아크 코사인 함수 각도를 구할때 많이씀, cos를 적용했을 때 x가 나오는 라디안 각도 값을 반환 합니다.

```
acos(x)
```

---

asin(x) : 아크 사인 함수 각도를 구할때 많이씀, sin을 적용했을 때 x가 나오는 라디안 각도 값을 반환 합니다.

```
asin(x)
```

---

atan(x) : 아크 탄젠트 함수 각도를 구할때 많이씀, tan을 적용했을 때 x가 나오는 라디안 각도 값을 반환합니다.

```
atan(x)
```

---

atan2 :  tan을 적용했을 때(x,y)가 나오는 라디란 각도 값을 반환합니다.

```
atan2(y, x)
```

---

ceil : 무조건 올림함수

```c++
ceil(10.1) // 11
ceil(10.6) // 11
ceil(10) // 10
```

---

cos : 코사인 값 반환

```
cos(x)
```

---

cosh : 라디안 x의 하이퍼볼릭 cos값을 반환합니다.

```
 cosh(x)
```

---

exp : x를 인수로 하는 e^x 값을 반환합니다.  e(오일러 상수,  자연상수)

```c#
console.log(Math.exp(0));
// expected output: 1

console.log(Math.exp(1));
// expected output: 2.718281828459 (approximately)

console.log(Math.exp(-1));
// expected output: 0.36787944117144233

console.log(Math.exp(2));
// expected output: 7.38905609893065
```

---

degress(x) : 라디안 값을 각도로 반환

```c++
degress(PI) // 180
degress(2*PI) // 360
degress(PI/180) // 1
```

---

exp2(x) : 밑수가  2인 지수  2^x

```c++
exp2(1.0) // 2.000000
exp2(1.2) // 2.297397
exp2(1.4) // 2.639016
exp2(1.6) // 3.031433
exp2(1.8) // 3.482202
exp2(2.0) // 4.000000
exp2(2.2) // 4.594793
exp2(2.4) // 5.278032
exp2(2.6) // 6.062866
exp2(2.8) // 6.964405
exp2(3.0) // 8.000000
```

---

floor : 무조건 내림함수

```c++
floor(10.5) // 10
floor(10.9) // 10
floor(10.8) // 10
floor(10) // 10
```

---

fmod(x) : 나눠서 실수부분 반환하는 함수

```c++
fmod() //?
```

---

frac(x) : x의 소숫점 반환하는 함수 

```
frac(x)
```

---

frexp : ??

```

```

---

isfinite(x) : 무한대, 주어진 값이 유한수인지 판별, 인자가 양 또는 음의 [`Infinity`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Infinity)거나 [`NaN`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/NaN)이면 `false`, 아니면 `true`.

```c++
isfinite(Infinity);  // false
isfinite(NaN);       // false
isfinite(-Infinity); // false

isfinite(0);         // true
isfinite(2e64);      // true
isfinite(910);       // true

isfinite(null);      // true, would've been false with the 
                     // more robust Number.isfinite(null)

isfinite('0');       // true, would've been false with the 
                     // more robust Number.isfinite("0")
```

---

isinf(x) : 함수의 *x* 가 무한대 이면, 0이 아닌 값을 반환 한다.

```c++
isinf(0) // 0
isinf(910) //0
isinf(Infinity) //
isinf(-Infinity) //
```

---

isnan(x) : 함수의 *x* 가 `NaN` 이면 `true`, 다른 값이면 `flase`를 반환 한다.

```

```

---

ldexp, log, log2, log10, modf, pow(제곱 함수), round(반올림 함수), rsprt, sin, sincos, sinh, smoothstep, sprt, tan, tanh,



벡터함수

dot : 내적 함수

reflect : 반사벡터를 구하는 함수

all, any, 

cross : 외적함수

faceforward : 표면에서 노말벡터

distance : 거리함수

length : 길이?

 lit, 

normalize : 정규화 함수

refract



행렬함수

mul : 행렬곱셈함수

transpose

determinant : 행렬



텍스쳐함수

tex1D, tex2D(텍스처와 uv값을 넘기면 해당하는 rgba색상을 반환하는 함수), 

tex3D, texCUBE 

tex11 Dproj, tex2Dproj, tex3Dproj, texCUBEproj,

tex1Dbias, tex2Dbias , tex3Dbias, texCUBEbias



기타함수

noise

# 0.Lambert Lighting(확산 조명)

 확산광 = 빛의세기 x 물체의색 X (Normal . LightingDir)

받아올 Sementic(시멘틱) 

POSITION, NORMAL

# 0.1 BlinFong Half Vector(블린퐁 하프벡터)

 hlaf = E + L / |E + L|

반사광 = 빛의세기 x 물체의색 + 빛의세기 x 물체의색 * (Normal . Lighting) + 빛의세기 x 물체의색 + (Normal . half) 제곱 

# 0.2 쿡, 토런스 반사 모델(금속 표면면)

퐁에 의한 반영 반사 모델은 빛의 반사를 간단한 계산으로 표현할 수있는 훌륭한 것이지만.

어차피 퐁의 경험과 직감에 의지한 이론이므로 싸구려 플라스틱 같은 질감이라 현실감이 없습니다

그래서 토런스(Torrance),  스패로우(Sparrow), 블린(Blinn), 쿡(Cock) 등의 선각자들의 표면의 거친 정도를 표현 할수 있는 좀더 좋은 반사 모델을 생각했습니다

![](\images\CookTorrance.png)







