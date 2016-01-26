---
layout: post
title: Simple Functions Composing in C#
---

```csharp
public static class Ext
    {
        public static Func<T1, T3> Compose<T1, T2, T3>(this Func<T1, T2> func,
            Func<T2, T3> funcToCompose)
        {
            return (x => funcToCompose(func(x)));
        }
    }
```
