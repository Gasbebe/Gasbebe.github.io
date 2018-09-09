---
layout: post
title: "Seja bem-vindo"
description: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
image: 'http://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_760/v1504807239/morpheus_xdzgg1.jpg'
category: 'blog'
twitter_text: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
introduction: Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
---



# Heading 1

## Heading 2

### Heading 3

#### Heading 4

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

## Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

```cs

using UnityEngine;
using UnityEditor;
using System.Reflection;

[InitializeOnLoad]
public class HierarchyIcon
{
    static HierarchyIcon() { EditorApplication.hierarchyWindowItemOnGUI 							 += EvaluateIcons; }

    private static void EvaluateIcons(int instanceID, Rect 				      										  selectionRect)
    {
        GameObject go = EditorUtility.InstanceIDToObject(instanceID) as 															 GameObject;
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