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

radiams, 

saturate : 0 ~ 1 넘는 값을 잘라버리는 함수

abs : 절대값을 반환하는 함수

clamp, max, min, 

sign : ??

step(x,y) : x <= y 일때 1을 반환 아니면 0을 반환한다

acos : 아크 코사인 함수

asin : 아크 사인 함수

atan : 아크 탄젠트 함수

atan2 : ??

ceil : 무조건 올림함수

cos : 코사인 값 반환

cosh, exp, degress, exp2, 

floor : 무조건 내림함수

fmod : 나눠서 실수부분 반환하는 함수

frac(x) : x의 소숫점 반환하는 함수 

frexp : ??

isfinite : ??

isinf : ??

isnan : ??

ldexp, log, log2, log10, modf, pow(제곱 함수), round(반올림 함수), rsprt, sin, sincos, sinh, smoothstep, sprt, tan, tanh,



벡터함수

dot : 내적 함수

reflect : 반사벡터를 구하는 함수

all, any, 

cross : 외적함수

faceforward

distance, length, lit, 

normalize : 정규화 함수

refract



행렬함수

mul, transpose

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

# 1. Water ripple Shader(빗방울 효과)

이 효과를 구현하기 위해서는 water ripple normal 맵이 필요하다

# ETC.



