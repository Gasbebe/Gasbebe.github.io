---
layout: post
title: "template"
description: base
image: '\images\bg.jpg'
category: 'template'
tag:
 - Android
introduction: 안드로이드
---

```c++
Shader "Tutorial/042_Dithering/DistanceFade"{
	//show values to edit in inspector
	Properties{
		_MainTex ("Texture", 2D) = "white" {}
		_Color ("Tint", Color) = (1,1,1,1)
        _DitherPattern ("Dithering Pattern", 2D) = "white" {}
		_MinDistance ("Minimum Fade Distance", Float) = 0
		_MaxDistance ("Maximum Fade Distance", Float) = 1
	}

	SubShader {
		//the material is completely non-transparent and is rendered at the same time as the other opaque geometry
		Tags{ "RenderType"="Opaque" "Queue"="Geometry"}

		CGPROGRAM

		#pragma surface surf Standard
		#pragma target 3.0

		//texture and tint of color
		sampler2D _MainTex;
		float4 _Color;

		//The dithering pattern
		sampler2D _DitherPattern;
		float4 _DitherPattern_TexelSize;

		//remapping of distance
		float _MinDistance;
		float _MaxDistance;

		//input struct which is automatically filled by unity
		struct Input {
			float2 uv_MainTex;
			float4 screenPos;
		};

		//the surface shader function which sets parameters the lighting function then uses
		void surf (Input i, inout SurfaceOutputStandard o) {
			//read texture and write it to diffuse color
			float3 texColor = tex2D(_MainTex, i.uv_MainTex);
			o.Albedo = texColor.rgb * _Color;

			//value from the dither pattern
			float2 screenPos = i.screenPos.xy / i.screenPos.w;
			float2 ditherCoordinate = screenPos * _ScreenParams.xy * _DitherPattern_TexelSize.xy;
			float ditherValue = tex2D(_DitherPattern, ditherCoordinate).r;

			//get relative distance from the camera
			float relDistance = i.screenPos.w;
			relDistance = relDistance - _MinDistance;
			relDistance = relDistance / (_MaxDistance - _MinDistance);
			//discard pixels accordingly
			clip(relDistance - ditherValue);
		}
		ENDCG
	}
}
```

---

```c++
Shader "Tutorial/042_Dithering/BasicBW"{
	//show values to edit in inspector
	Properties{
		_MainTex ("Texture", 2D) = "white" {}
        _DitherPattern ("Dithering Pattern", 2D) = "white" {}
		_Color1 ("Dither Color 1", Color) = (0, 0, 0, 1)
		_Color2 ("Dither Color 2", Color) = (1, 1, 1, 1)
	}

	SubShader{
		//the material is completely non-transparent and is rendered at the same time as the other opaque geometry
		Tags{ "RenderType"="Opaque" "Queue"="Geometry"}

		Pass{
			CGPROGRAM

			//include useful shader functions
			#include "UnityCG.cginc"

			//define vertex and fragment shader
			#pragma vertex vert
			#pragma fragment frag

			//texture and transforms of the texture
			sampler2D _MainTex;
			float4 _MainTex_ST;

            //The dithering pattern
            sampler2D _DitherPattern;
            float4 _DitherPattern_TexelSize;

			//Dither colors
			float4 _Color1;
			float4 _Color2;

			//the object data that's put into the vertex shader
			struct appdata{
				float4 vertex : POSITION;
				float2 uv : TEXCOORD0;
			};

			//the data that's used to generate fragments and can be read by the fragment shader
			struct v2f{
				float4 position : SV_POSITION;
				float2 uv : TEXCOORD0;
                float4 screenPosition : TEXCOORD1;
			};

			//the vertex shader
			v2f vert(appdata v){
				v2f o;
				//convert the vertex positions from object space to clip space so they can be rendered
				o.position = UnityObjectToClipPos(v.vertex);
				o.uv = TRANSFORM_TEX(v.uv, _MainTex);
                o.screenPosition = ComputeScreenPos(o.position);
				return o;
			}

			//the fragment shader
			fixed4 frag(v2f i) : SV_TARGET{
				//texture value the dithering is based on
				float texColor = tex2D(_MainTex, i.uv).r;

				//value from the dither pattern
				float2 screenPos = i.screenPosition.xy / i.screenPosition.w;
				float2 ditherCoordinate = screenPos * _ScreenParams.xy * _DitherPattern_TexelSize.xy;
				float ditherValue = tex2D(_DitherPattern, ditherCoordinate).r;

				//combine dither pattern with texture value to get final result
				float ditheredValue = step(ditherValue, texColor);
				float4 col = lerp(_Color1, _Color2, ditheredValue);
				return col;
			}

			ENDCG
		}
	}

    Fallback "Standard"
}
```

### Clipping a Model with a Plane

---

```c++
Shader "Tutorial/021_Clipping_Plane"{
	//show values to edit in inspector
	Properties{
		_Color ("Tint", Color) = (0, 0, 0, 1)
		_MainTex ("Texture", 2D) = "white" {}
		_Smoothness ("Smoothness", Range(0, 1)) = 0
		_Metallic ("Metalness", Range(0, 1)) = 0
		[HDR]_Emission ("Emission", color) = (0,0,0)

		[HDR]_CutoffColor("Cutoff Color", Color) = (1,0,0,0)
	}

	SubShader{
		//the material is completely non-transparent and is rendered at the same time as the other opaque geometry
		Tags{ "RenderType"="Opaque" "Queue"="Geometry"}

		// render faces regardless if they point towards the camera or away from it
		Cull Off

		CGPROGRAM
		//the shader is a surface shader, meaning that it will be extended by unity in the background 
		//to have fancy lighting and other features
		//our surface shader function is called surf and we use our custom lighting model
		//fullforwardshadows makes sure unity adds the shadow passes the shader might need
		//vertex:vert makes the shader use vert as a vertex shader function
		#pragma surface surf Standard fullforwardshadows
		#pragma target 3.0

		sampler2D _MainTex;
		fixed4 _Color;

		half _Smoothness;
		half _Metallic;
		half3 _Emission;

		float4 _Plane;

		float4 _CutoffColor;

		//input struct which is automatically filled by unity
		struct Input {
			float2 uv_MainTex;
			float3 worldPos;
			float facing : VFACE;
		};

		//the surface shader function which sets parameters the lighting function then uses
		void surf (Input i, inout SurfaceOutputStandard o) {
			//calculate signed distance to plane
			float distance = dot(i.worldPos, _Plane.xyz);
			distance = distance + _Plane.w;
			//discard surface above plane
			clip(-distance);

			float facing = i.facing * 0.5 + 0.5;
			
			//normal color stuff
			fixed4 col = tex2D(_MainTex, i.uv_MainTex);
			col *= _Color;
			o.Albedo = col.rgb * facing;
			o.Metallic = _Metallic * facing;
			o.Smoothness = _Smoothness * facing;
			o.Emission = lerp(_CutoffColor, _Emission, facing);
		}
		ENDCG
	}
	FallBack "Standard" //fallback adds a shadow pass so we get shadows on other objects
}
```

 https://www.ronja-tutorials.com/ 

```c#
class GridSystem{
	[SrealizeFeild]
    private Tile [] tiles;
}


class Tile{
    private int x;
    private int y;
}
```



### Remind

---

math

- floor() 함수는 올림 함수로서 설정한 구간을 일정한 값으로 설정 할때 많이 쓰임
  - 0 < x <= 1 구간을 floor() 적용 하면  1로 고정
  - (0/10) < x <= (10/10)  floor()를 쓰고 나중에 10을 곱하면 10으로 고정
- 