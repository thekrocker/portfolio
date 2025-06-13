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

## Final Thoughts
Extension methods are extremely useful for common and repetitive tasks. By organizing them into a library, you can boost your development speed and maintain cleaner code.



