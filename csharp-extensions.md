# Extension Methods in Unity

Extension methods allow you to add new methods to existing types without modifying their structure. This makes your code more reusable and easier to maintain. For example, when you write an `int` and use `.ToString()`, that’s an extension method. They're especially useful when you find yourself writing similar logic across different places.

## When Should You Use Extension Methods?

You should use them when:
- You frequently use the same logic for a specific type.
- You want to reduce repetitive code.
- You want to maintain a clean and reusable codebase.

You can even bundle your extension methods into a utility library and use them across multiple projects.

---

## Example 1: Object Spawner with Parenting

Let’s say we have an `EnemySpawner` in our game that spawns enemies and sets them as a child of the spawner object:

```csharp
public class EnemySpawner : MonoBehaviour 
{
    [SerializeField] private GameObject goPrefab;

    void Start()
    {
        var go = Instantiate(goPrefab, transform.position, Quaternion.identity);
        go.transform.SetParent(transform);
    }
}
```

Now, you also have an ObstacleSpawner doing the same logic. Instead of repeating the same code, create an extension method.

```csharp
public static class ExtensionMethods
{
    public static void CreateObjectAndSetParent(this Transform trans, GameObject go, Vector3 pos, Quaternion rot)
    {
        GameObject temp = Object.Instantiate(go, pos, rot);
        temp.transform.SetParent(trans);
    }
}
```

Usage in another script:

`transform.CreateObjectAndSetParent(prefab, position, rotation);`


## Example 2: Reset Transform
Often you may need to reset an object’s transform.

### Old way:

```csharp
public void ResetTransformation()
{
    transform.position = Vector3.zero;
    transform.rotation = Quaternion.identity;
    transform.localScale = Vector3.one;
}
```

### Extension Method

```csharp
public static void ResetTransformation(this Transform trans)
{
trans.position = Vector3.zero;
trans.rotation = Quaternion.identity;
trans.localScale = Vector3.one;
}
```

Now you can call it directly like: `transform.ResetTransformation();`

Here is an Extension method library for popular actions, like shuffling etc.

```csharp
using UnityEngine;
using System;
using System.Collections.Generic;

public static class UnityExtensions
{
    // 1. Destroy GameObject safely (if not null)
    public static void SafeDestroy(this GameObject obj)
    {
        if (obj != null)
        {
#if UNITY_EDITOR
            if (!Application.isPlaying)
                UnityEngine.Object.DestroyImmediate(obj);
            else
#endif
                UnityEngine.Object.Destroy(obj);
        }
    }

    // 2. Set active safely (check if value differs)
    public static void SetActiveIfChanged(this GameObject obj, bool isActive)
    {
        if (obj != null && obj.activeSelf != isActive)
            obj.SetActive(isActive);
    }

    // 3. Reset transform position, rotation, scale
    public static void ResetTransform(this Transform t)
    {
        t.localPosition = Vector3.zero;
        t.localRotation = Quaternion.identity;
        t.localScale = Vector3.one;
    }

    // 4. Get or Add a component if not present
    public static T GetOrAddComponent<T>(this GameObject obj) where T : Component
    {
        return obj.TryGetComponent<T>(out var comp) ? comp : obj.AddComponent<T>();
    }

    // 5. Shuffle a list randomly
    public static void Shuffle<T>(this IList<T> list)
    {
        for (int i = list.Count - 1; i > 0; i--)
        {
            int rand = UnityEngine.Random.Range(0, i + 1);
            (list[i], list[rand]) = (list[rand], list[i]);
        }
    }

    // 6. Convert Vector3 to Vector2 (XZ plane)
    public static Vector2 ToXZ(this Vector3 v) => new Vector2(v.x, v.z);

    // 7. Set layer recursively
    public static void SetLayerRecursively(this GameObject obj, int layer)
    {
        obj.layer = layer;
        foreach (Transform t in obj.transform.GetComponentsInChildren<Transform>(true))
        {
            t.gameObject.layer = layer;
        }
    }

    // 8. Invoke action after delay using coroutine
    public static void InvokeDelayed(this MonoBehaviour mb, Action action, float delay)
    {
        mb.StartCoroutine(InvokeCoroutine(action, delay));
    }

    private static System.Collections.IEnumerator InvokeCoroutine(Action action, float delay)
    {
        yield return new WaitForSeconds(delay);
        action?.Invoke();
    }

    // 9. Clamp Vector3 between two values
    public static Vector3 Clamp(this Vector3 v, Vector3 min, Vector3 max)
    {
        return new Vector3(
            Mathf.Clamp(v.x, min.x, max.x),
            Mathf.Clamp(v.y, min.y, max.y),
            Mathf.Clamp(v.z, min.z, max.z)
        );
    }

    // 10. Lerp Color alpha
    public static Color WithAlpha(this Color c, float alpha)
    {
        c.a = alpha;
        return c;
    }

    // 11. Check if layer is in LayerMask
    public static bool IsInLayerMask(this GameObject obj, LayerMask mask)
    {
        return (mask.value & (1 << obj.layer)) != 0;
    }

    // 12. Smoothly look at a direction
    public static void SmoothLookAt(this Transform t, Vector3 targetPosition, float speed)
    {
        Vector3 direction = targetPosition - t.position;
        if (direction != Vector3.zero)
        {
            Quaternion targetRotation = Quaternion.LookRotation(direction);
            t.rotation = Quaternion.Slerp(t.rotation, targetRotation, Time.deltaTime * speed);
        }
    }

    // 13. Check distance within a threshold
    public static bool IsWithinDistance(this Vector3 pos, Vector3 other, float threshold)
    {
        return Vector3.SqrMagnitude(pos - other) < threshold * threshold;
    }

    // 14. Enable/Disable a CanvasGroup
    public static void SetCanvasGroupActive(this CanvasGroup cg, bool isActive)
    {
        cg.alpha = isActive ? 1 : 0;
        cg.blocksRaycasts = isActive;
        cg.interactable = isActive;
    }

    // 15. Get world bounds of renderer
    public static Bounds GetRendererBounds(this GameObject obj)
    {
        var renderers = obj.GetComponentsInChildren<Renderer>();
        if (renderers.Length == 0) return new Bounds(obj.transform.position, Vector3.zero);

        Bounds bounds = renderers[0].bounds;
        for (int i = 1; i < renderers.Length; i++)
            bounds.Encapsulate(renderers[i].bounds);

        return bounds;
    }
}
```



## Final Thoughts
Extension methods are extremely useful for common and repetitive tasks. By organizing them into a library, you can boost your development speed and maintain cleaner code.



