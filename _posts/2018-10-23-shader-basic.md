---
layout: post
title: "Shader"
description: 쉐이더 함수정리
image: '\images\bg.jpg'
category: 'Shader'
tag:
 - Shader
 - Unity3D
 - HLSL
introduction: 쉐이더 기초테크닉
---



#  Step 1 : 색상

```c
struct VertexInput{
    float4 vertex : POSITION;
    float2 uv : TEXCOORD;
}

struct FragmentInput{
    float4 vertex : POSITION;
    float2 uv : TEXCOORD;
}

void vertex(VertexInput i){
	FragmentInput o;
    o.vertex = i.vertex;
    o.uv = i.uv;
}
```



# Step 2 : 텍스쳐

