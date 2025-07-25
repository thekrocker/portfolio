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

### `IStackSource` & `IStackTarget`
These are the foundational interfaces for any object that can provide or accept stack items.

```csharp
public interface IStackSource
{
    bool CanProvide(IStackFilter filter);
    IStackItem TakeItem(IStackFilter filter); // returns first matching item
}

public interface IStackTarget
{
    bool HasItemType(EItemType itemType);
    bool CanAccept();
    void AddItem(IStackItem item);
    int GetStackCount();
    Vector3 GetNextStackGlobalPosition();
    IEnumerable<IStackItem> GetStack();
}
```

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

public void StartFilteredTransferFromSource(
    IStackSource source,
    IStackTarget target,
    IStackFilter filter,
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
- Handles visuals using `IStackLayout`.

```csharp
[SerializeReference]
private IStackLayout layout; // Allows us to pick layout from inspector

layout.CalculateLayout(_stack, out var positions, out var rotations); // Return positions & rotation to set stack visuals, like align vertically, grid based etc.

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

## 💡 Use Cases for Stack System

The modular Stack System architecture allows us to flexibly manage item flow between sources and targets in a game environment. Here are some practical scenarios:

---

### 🥣 Use Case 1: Order Delivery to Customer

**Scenario:** A chef prepares food and stacks it. When a customer is ready, the food must be delivered automatically.

- **Source:** `ChefCounterStackHandler`
- **Target:** `CustomerStackHandler`
- **Filter:** `StackTypeFilter(EItemType.Food)`
- **Condition:** `StopWhenSourceEmpty(filter)` or `StopWhenTargetFull()`

```csharp
var stackAction = new StackAction();
stackAction.StartFilteredTransferFromSource(
    chefCounter,
    customerStack,
    new StackTypeFilter(EItemType.Food),
    new StopWhenSourceEmpty(new StackTypeFilter(EItemType.Food)),
    new StopWhenTargetFull()
);
```

---

### 📦 Use Case 2: Resource Collection (e.g. Fruit Crate ➜ Basket)

**Scenario:** Fruits spawn in crates periodically. Workers should collect and stack them into storage baskets.

- **Source:** `FruitCrateStackHandler`
- **Target:** `BasketStackHandler`
- **Filter:** `StackTypeFilter(EItemType.Fruit)`
- **Condition:** `StopWhenSourceEmpty(filter)`, `StopWhenTargetFull()`

---

### 🛒 Use Case 3: Shop Restocking System

**Scenario:** When shelf items run low, a delivery box restocks the shelf automatically.

- **Source:** `DeliveryBoxStackHandler`
- **Target:** `ShelfStackHandler`
- **Filter:** `StackIdFilter("Apple")` (to restock only apples)
- **Condition:** Custom restocking condition like: `RestockWhenBelowThreshold("Apple", 5)`

---

### 🚚 Use Case 4: Truck Unloading to Warehouse

**Scenario:** Trucks deliver random items. Workers unload them into the warehouse stack.

- **Source:** `TruckStackHandler`
- **Target:** `WarehouseStackHandler`
- **Filter:** `AlwaysMatchFilter.Instance`
- **Condition:** `StopWhenSourceEmpty()`

---

### 🎯 Use Case 5: Prioritized Filtering Logic

**Scenario:** A universal storage sorts items into category-based zones.

- **Source:** `UniversalInputStackHandler`
- **Targets:** `MeatStorage`, `VegetableStorage`, etc.
- **Filter:** Custom filters based on item categories.
- **Approach:** Use separate `StackAction` instances per target with respective filters.

---

This flexible architecture allows for dynamic transfer logic, easy expansions, and clean separation of behaviors via filters and conditions.
