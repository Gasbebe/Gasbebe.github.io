---
layout: post
title: "Shader"
description: 쉐이더 기본동작 원리
image: '\images\bg.jpg'
category: 'blog'
tag:
 - Shader
introduction: 쉐이더 기본동작 원리
---

# 3D Graphics Rendering Pipeline

![pipeline](\images\pipeline.png)

# Vertex Shader(정점 쉐이더)

![vertex-shader-anim](\images\vertex-shader-anim.gif)

**정점 쉐이더는 모델이 가지고 있는 정점에 갯수만큼 실행이 된다**



**출처 : webglfundamentals.org**

# Fragment Shader(프래그멘트 쉐이더)

![fragmentAnim](\images\fragmentAnim.gif)

**정점 쉐이더로 변환된 좌표가 화면상에 잡힌 픽셀만큼 실행이된다**

**출처 : webglfundamentals.org**


```cs

using UnityEngine;
using UnityEditor;
using System.Reflection;

[InitializeOnLoad]
public class HierarchyIcon
{
    static HierarchyIcon() { EditorApplication.hierarchyWindowItemOnGUI += EvaluateIcons; }

    private static void EvaluateIcons(int instanceID, Rect selectionRect)
    {
        GameObject go = EditorUtility.InstanceIDToObject(instanceID) as GameObject;
        if (go == null) return;

        IHierarchyIcon slotCon = go.GetComponent<IHierarchyIcon>();
        if (slotCon != null) 
        {
        	DrawIcon(slotCon.EditorIconPath, selectionRect); 
        }
    }

    private static void DrawIcon(string texName, Rect rect)
    {
        Rect r = new Rect(rect.x + rect.width - 16f, rect.y, 16f, 16f);
        GUI.DrawTexture(r, GetTex(texName));

        Texture2D t = new Texture2D(1, 1);
        Color c = new Color(100, 200, 100, 0.1f);
        t.SetPixel(1, 1, c);
        t.Apply();
        GUI.DrawTexture(rect, t, ScaleMode.StretchToFill);
    }

    private static Texture2D GetTex(string name)
    {
        return (Texture2D)EditorGUIUtility.Load("Icons/" + name);
    }
}

```

## Lists



## Images



# Shader

minimal shader

//==============================================================================

//==============================================================================