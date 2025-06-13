# Unity ScriptableObjects – Improved Data Management

In game development, we often encounter situations where similar objects require different data. For example, three different enemies might each have unique movement speeds, attack ranges, and other stats. ScriptableObjects are an excellent solution in such scenarios.

ScriptableObjects exist as assets in your project and consume very little memory. They are generally used to store and manage data. Their advantages include:

- Independent of scene and Play Mode (runtime changes are saved).
- Easy to use with drag-and-drop.
- Easily testable.
- Reduce dependencies between scripts.

---

## Why Not Just Duplicate Prefabs?

Duplicating a prefab copies its data as an instance. But duplicating data is unnecessary—multiple objects can reference shared data instead. Although this might not seem like a big deal, avoiding repetition is a key principle in programming.

Using shared data via ScriptableObjects makes things cleaner and more efficient. You can reuse existing data when creating a new enemy and make quick assignments from the editor.

---

## Creating a ScriptableObject

To create a ScriptableObject, your class must inherit from `ScriptableObject`, and you can use the `[CreateAssetMenu]` attribute to make it show up in Unity’s asset menu.

```csharp
[CreateAssetMenu(menuName = "Stats/EnemyStats")]
public class EnemyStats : ScriptableObject
{
}
```

This creates an asset menu item at Stats → EnemyStats. When you right-click in the Project window, you can now create this object.


<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://www.sdedeakay.com/wp-content/uploads/2022/06/so-1024x867.png" style="width: 55%;" alt="Gameplay Screenshot">
<img src="https://www.sdedeakay.com/wp-content/uploads/2022/06/so1.png" style="width: 40%;" alt="Gameplay Screenshot">
</div>




At first, the object is empty. Let’s define some variables inside:

```csharp
[CreateAssetMenu(menuName = "Stats/EnemyStats")]
public class EnemyStats : ScriptableObject
{
    public string enemyName;
    public int health;
    public int mana;
    public float moveSpeed;
    public float attackSpeed;
}
```

Now you’ll see these fields in the inspector and can edit them directly. The variables are public so they can be used in other scripts.


<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://www.sdedeakay.com/wp-content/uploads/2022/06/image-1.png" style="width: 75%;" alt="Gameplay Screenshot">
</div>

## Using the ScriptableObject in a MonoBehaviour
To apply this data to an enemy, add a field in the enemy script:

```csharp
public class Enemy : MonoBehaviour
{
[SerializeField] private EnemyStats stats;
}
```
This lets you assign the ScriptableObject from the Unity Inspector.

<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://www.sdedeakay.com/wp-content/uploads/2022/06/image-2.png" style="width: 75%;" alt="Gameplay Screenshot">
</div>


Let’s test it by adding a method inside EnemyStats that logs the stat values:

```csharp
public void PrintStats()
{
Debug.Log($"My name is {enemyName}, my health is: {health}, my mana is {mana}, my move speed is {moveSpeed} & my attack speed is {attackSpeed}");
}
```

Now call that method from the enemy script:

```csharp
private void Start()
{
    stats.PrintStats();
}
```

Run the game, and you'll see your enemy’s data printed in the console. You can assign another ScriptableObject to test different values. The change is immediate.

<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://www.sdedeakay.com/wp-content/uploads/2022/06/image-3.png" style="width: 75%;" alt="Gameplay Screenshot">
</div>


## Conclusion
With ScriptableObjects, you can assign and reuse data easily between multiple objects. Creating new enemies or updating stats becomes faster and more manageable. You can even change data during runtime, and it persists without requiring Play Mode restarts.

This is one of the cleanest and most efficient ways to manage game data in Unity. In future articles, we’ll explore how ScriptableObjects can also help simplify game architecture and reduce code coupling.