# Stack System: Flexible, Extendable Stack Handling in Unity

This page showcases how I designed a fully modular and extendable **Stack System** for transferring and managing stacked items with filtering and custom transfer conditions.

---

## 💡 Overview

The Stack System is designed for item transfer logic in games (e.g., factory games, delivery chains, cooking systems). It supports:

- **Filters**: to decide which items to pick
- **Transfer Conditions**: to control when to stop transfers
- **Layout**: for visual positioning of stacked items
- **StackSource**/**StackTarget** interfaces for generalized item movement

---

## 🧰 Filters (`IStackFilter`)

Filters define logic to determine if a stack item matches a condition.

```csharp
public interface IStackFilter
{
    bool IsMatch(IStackItem item);
}
```

### Examples:

```csharp
public class AlwaysMatchFilter : IStackFilter
{
    public bool IsMatch(IStackItem item) => true;
}

public class StackTypeFilter : IStackFilter
{
    public bool IsMatch(IStackItem item) => item.GetItemType() == _type;
}
```

---

## 🛑 Transfer Conditions (`IStackTransferCondition`)

Control when a transfer should **stop**:

```csharp
public interface IStackTransferCondition
{
    string GetConditionDescription();
    bool ShouldStop(IStackSource source, IStackTarget target);
    bool ShouldStop(IList<IStackItem> sourceItems, IStackTarget target);
}
```

### Examples:

```csharp
public class StopWhenTargetFull : IStackTransferCondition
{
    public bool ShouldStop(IStackSource source, IStackTarget target) => !target.CanAccept();
}
```

```csharp
public class StopWhenSourceEmpty : IStackTransferCondition
{
    public bool ShouldStop(IStackSource source, IStackTarget target) => !source.CanProvide(_filter);
}
```

---

## 🔁 StackAction: Modular Transfer Logic

`StackAction` coordinates item transfer between sources and targets.

```csharp
public void StartTransferFromSource(
    IStackSource source,
    IStackTarget target,
    params IStackTransferCondition[] conditions)
```

Variants:

- `StartTransferFromList()` – for static stacks
- `StartTransferFromSource()` – no filter
- `StartFilteredTransferFromSource()` – filtered transfer

Internally uses **`UniTask`** for async execution.

---

## 📦 StackHandler: The Core Implementation

`StackHandler` implements both `IStackSource` and `IStackTarget`, and manages stack visuals.

- Holds stack of `IStackItem`
- Handles adding/removing with filtering
- Reacts to upgrades via `IStackUpgradeSource`

Handles visuals using injected `IStackLayout`.

```csharp
public bool CanProvide(IStackFilter filter)
public IStackItem TakeItem(IStackFilter filter)
public void AddItem(IStackItem item)
```

---

## 🧱 Layout System

Handles the visual positioning of stack items.

```csharp
public interface IStackLayout
{
    void CalculateLayout(...);
    Vector3 GetNextStackGlobalPosition(...);
}
```

### Example:

```csharp
public class VerticalStackLayout : IStackLayout
{
    public void CalculateLayout(...) { ... }
}
```

---

## ✅ Benefits

- ✅ Clean separation of concerns
- ✅ Easily extendable (new filters, conditions, layouts)
- ✅ Plug & play architecture with interfaces
- ✅ Works smoothly with dependency injection

---

## 🔄 Example Use

```csharp
_stackAction.StartFilteredTransferFromSource(
    source: someStack,
    target: targetStack,
    filter: new StackTypeFilter(EItemType.Bread),
    new StopWhenTargetFull(),
    new StopWhenSourceEmpty(filter)
);
```

---

This system is a great demonstration of how to apply **Strategy Pattern**, **DI**, and **async transfer control** in Unity while maintaining scalability and flexibility.
