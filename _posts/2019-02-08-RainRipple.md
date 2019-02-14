---
layout: post
title: "빗물 효과"
description: 빗물 효과
image: '\images\bg.jpg'
category: 'Unity3D'
tag:
 - Unity3D
introduction: 빗물 효과

---


```c++
Shader "Custom/Rain" {
	Properties {
		_Color ("Color", Color) = (1,1,1,1)
		_MainTex ("Albedo (RGB)", 2D) = "white" {}
		_RainBaseColor("RainBaseColor", 2D) = "white" {}
		_RainNormal("RainNormal", 2D) = "white" {}
		_Glossiness ("Smoothness", Range(0,1)) = 0.5
		_Metallic ("Metallic", Range(0,1)) = 0.0
		_RainSpeed ("RainSpeed", Range(0, 1)) = 0.0
	}
	SubShader {
		Tags { "RenderType"="Opaque" }
		LOD 200

		CGPROGRAM
		// Physically based Standard lighting model, and enable shadows on all light types
		#pragma surface surf Standard fullforwardshadows

		// Use shader model 3.0 target, to get nicer looking lighting
		#pragma target 3.0

		sampler2D _MainTex;
		sampler2D _RainBaseColor;
		sampler2D _RainNormal;

		struct Input {
			float2 uv_MainTex;
			float2 uv_RainBaseColor;
			float2 uv_RainNormal;
		};

		float _RainSpeed;
		half _Glossiness;
		half _Metallic;
		fixed4 _Color;

		UNITY_INSTANCING_BUFFER_START(Props)
			// put more per-instance properties here
		UNITY_INSTANCING_BUFFER_END(Props)

		void surf (Input IN, inout SurfaceOutputStandard o) {
			
			fixed4 c = tex2D (_MainTex, IN.uv_MainTex) * _Color;
			fixed4 rainBaseColor = tex2D(_RainBaseColor, IN.uv_RainBaseColor);

			//============================================================
			//                     rain 
			//============================================================
			fixed4 rainNormal = tex2D(_RainNormal, IN.uv_RainNormal);
			fixed4 rainNormal2 = tex2D(_RainNormal, IN.uv_RainNormal.xy + 0.5);
			
			
			//rian ripple
			fixed4 resultRain;
			fixed4 rain = tex2D(_RainBaseColor, IN.uv_RainBaseColor).x - (1.0 - frac(_Time.y * _RainSpeed));
			fixed4 rain2 = tex2D(_RainBaseColor, IN.uv_RainBaseColor.xy + 0.5).x - (1.0 - frac(_Time.y  * _RainSpeed));

			rain = (1 - smoothstep(step(distance(rain, 0.05), 0.05), 0.00001, 1));
			rain2 = (1 - smoothstep(step(distance(rain2, 0.05), 0.05), 0.00001, 1));

			fixed rippleFade = abs(sin((_Time.y* _RainSpeed) * 0.05));
			fixed InterpolationTime = clamp(rippleFade, 0, 1);

			rain = rain * rippleFade;
			rain2 = rain2 * rippleFade;

			resultRain = lerp(rain, rain2, InterpolationTime);
			//=============================================================
			rainNormal = lerp(rainNormal, rainNormal2, resultRain);

			o.Albedo = c.rgb;
			o.Normal = UnpackNormal(rainNormal.rgba);
			//o.Emission = rainNormal.rgb;
			o.Alpha = 1;
		}
		ENDCG
	}
	FallBack "Diffuse"
}

```



![rain](\images\rain.png)

![rain2](\images\rain2.png)

