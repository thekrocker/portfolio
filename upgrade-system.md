
# Upgrade System

This upgrade system allows for flexible, scalable, and clean implementation of in-game upgrade mechanics. It supports multiple upgrade types (like stack size or movement speed), runtime logic, saving/loading, and a well-separated architecture using interfaces and DI (Dependency Injection).

---

## 💡 Key Concepts

### `IUpgrade`
Defines the upgrade logic and properties for a single upgrade (e.g., level, cost, values).

```csharp
public interface IUpgrade
{
    string Id { get; }
    int CurrentLevel { get; }
    int MaxLevel { get; }
    bool CanUpgrade { get; }
    int GetCost();
    void ApplyUpgrade();
    UpgradeData GetUpgradeData();
}
```

### `IUpgradeService`
Global interface to manage and retrieve upgrades. Used for systems/UI to upgrade or query values.

```csharp
public interface IUpgradeService
{
    UpgradeData GetUpgradeData(string upgradeId);
    IEnumerable<string> GetAllUpgradeIds();
    bool CanUpgrade(string upgradeId);
    int GetCurrentLevel(string upgradeId);
    int GetCost(string upgradeId);
    bool BuyUpgrade(string upgradeId);
    float GetCurrentValue(string upgradeId);
}
```

### `UpgradeManager`
- Injects necessary systems (currency, sound, movement, stack).
- Registers upgrades on `Awake()`.
- Supports saving/loading using a key `"Upgrades"`.

### `Upgrade`
Base class for specific upgrades. Uses `UpgradeData` ScriptableObject.

```csharp
public class MoveSpeedUpgrade : Upgrade
{
    protected override void OnApply() { /* logic */ }
}
```

---

## 🧪 Use Cases

### 🏃 Move Speed Upgrade
- Increases character movement speed each level.
- Uses `IMovementUpgradeSource` to adjust runtime value.

### 📦 Stack Size Upgrade
- Increases how many items the player can stack.
- Uses `IStackUpgradeSource` to reflect stack behavior.

---

## 🧱 Data Driven

### `UpgradeData`
Holds upgrade configuration and display info.

```csharp
[CreateAssetMenu(menuName = "Data/PPigeon/Upgrade/Upgrade Data")]
public class UpgradeData : ScriptableObject
{
    public string Id;
    public string DisplayName;
    public Sprite Icon;
    public int BaseCost;
    public int MaxLevel;
}
```

---

## 💾 Save & Load

The manager serializes upgrades by their `id` and `level` to restore them across sessions.

---

## 🧩 DI Friendly

All services and upgrades are registered using `Reflex`:

```csharp
public class UpgradeInstaller : MonoBehaviour, IInstaller
{
    public void InstallBindings(ContainerBuilder containerBuilder)
    {
        containerBuilder.AddSingleton(upgradeManager, typeof(IUpgradeService));
    }
}
```

---

## 🕹️ Example Usage

```csharp
[Inject] private IUpgradeService _upgradeService;

void UpgradeButtonClicked(string upgradeId)
{
    if (_upgradeService.BuyUpgrade(upgradeId))
    {
        Debug.Log("Upgrade successful!");
    }
}
```

---

## ✅ Summary

This system is highly modular, extendable, testable, and ready for production. New upgrades only require a new derived class + data config.

