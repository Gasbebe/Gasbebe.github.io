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



# Step 2 : 트리플래너(TriPlaner)

```c
Shader "Custom/NewSurfaceShader" {
	Properties{
		_MainTex("Albedo (RGB)", 2D) = "white" {}
		_MainTexUV("tileU, tileV, offsetU, offetV", vector) = (1,1,0,0)
		_MainTex2("Side Tex", 2D) = "white" {}
		_MainTex2UV("tileU, tileV, offsetU, offetV", vector) = (1,1,0,0)

	}
	SubShader {
		Tags { "RenderType"="Opaque" }
		LOD 200

		CGPROGRAM

		#pragma surface surf Standard fullforwardshadows
		#pragma target 3.0

		sampler2D _MainTex;
		sampler2D _MainTex2;
		float4 _MainTexUV;
		float4 _MainTex2UV;


		struct Input {
			float3 worldPos;
			float3 worldNormal;
		};

		half _Glossiness;
		half _Metallic;
		fixed4 _Color;

		void surf (Input IN, inout SurfaceOutputStandard o) {
			
			//create triUV
			float2 topUV = float2(IN.worldPos.x, IN.worldPos.z);
			float2 frontUV = float2(IN.worldPos.x, IN.worldPos.y);
			float2 sideUV = float2(IN.worldPos.z, IN.worldPos.y);

			//texture
			float4 topTex = tex2D(_MainTex, topUV * _MainTexUV.xy + _MainTexUV.zw);
			float4 frontTex = tex2D(_MainTex2, frontUV * _MainTex2UV.xy + 		_MainTex2UV.zw);
			float4 sideTex = tex2D(_MainTex2, sideUV * _MainTex2UV.xy + _MainTex2UV.zw);
			
			o.Albedo = lerp(topTex, frontTex, abs(IN.worldNormal.z));
			o.Albedo = lerp(o.Albedo, sideTex, abs(IN.worldNormal.x));

			o.Alpha = 1;
		}
		ENDCG
	}
	FallBack "Diffuse"
}
```

