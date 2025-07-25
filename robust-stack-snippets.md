
# Stack System: Filterable, Condition-Based Item Transfer Architecture

The Stack System is designed to manage item stacking, filtering, and transferring logic in a highly flexible, decoupled, and extensible manner. It powers core systems like order delivery, machine outputs, and customer interactions, and it's composed of multiple interchangeable interfaces.

---

## Key Interfaces

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

## Filters

### `IStackFilter`
Filters are used to determine which items can be transferred.

```csharp
public interface IStackFilter
{
    bool IsMatch(IStackItem item);
}
```

#### Examples

- **AlwaysMatchFilter**: Accepts every item.
- **StackTypeFilter**: Filters by item type.
- **StackIdFilter**: Filters by item ID.

```csharp
public class StackTypeFilter : IStackFilter
{
    private readonly EItemType _foodItemType;
    public StackTypeFilter(EItemType foodItemType) => _foodItemType = foodItemType;

    public bool IsMatch(IStackItem item) => item.GetItemType() == _foodItemType;
}
```

---

## Conditions

### `IStackTransferCondition`
Transfer conditions define when transfers should stop.

```csharp
public interface IStackTransferCondition
{
    string GetConditionDescription();
    bool ShouldStop(IStackSource source, IStackTarget target);
    bool ShouldStop(IList<IStackItem> sourceItems, IStackTarget target);
}
```

#### Examples

- **StopWhenTargetFull**: Stops if the target cannot accept more items.
- **StopWhenSourceEmpty**: Stops if the source has no more items based on a filter.

---

## `StackAction`

The main class responsible for orchestrating the transfer logic. It supports multiple transfer entry points:

### Filtered Transfer (Recommended)

```csharp
public void StartFilteredTransferFromSource(
    IStackSource source,
    IStackTarget target,
    IStackFilter filter,
    params IStackTransferCondition[] conditions)
{
    StopTransfer();
    _cts = new CancellationTokenSource();
    TransferAsync(
        source,
        target,
        _transferInterval,
        filter,
        conditions,
        _cts.Token
    ).Forget();
}
```

This is the most flexible and readable way to start a transfer, as it allows both filtering and condition-based control.

---

## Layout System

Stack visuals are controlled by `IStackLayout`.

```csharp
public interface IStackLayout
{
    void CalculateLayout(IReadOnlyList<IStackItem> items, out Vector3[] positions, out Quaternion[] rotations);
    Vector3 GetNextStackGlobalPosition(IReadOnlyList<IStackItem> items);
}
```

### `VerticalStackLayout` Example

```csharp
[System.Serializable]
public class VerticalStackLayout : IStackLayout
{
    [SerializeField] private Vector3 offset = new(0, 0.25f, 0);

    public void CalculateLayout(IReadOnlyList<IStackItem> items, out Vector3[] positions, out Quaternion[] rotations)
    {
        positions = new Vector3[items.Count];
        rotations = new Quaternion[items.Count];

        for (int i = 0; i < items.Count; i++)
        {
            positions[i] = offset * i;
            rotations[i] = Quaternion.identity;
        }
    }

    public Vector3 GetNextStackGlobalPosition(IReadOnlyList<IStackItem> items)
    {
        return offset * items.Count;
    }
}
```

---

## Summary

✅ Decoupled and testable with `IStackSource` and `IStackTarget`  
✅ Fully customizable filtering and stopping conditions  
✅ Easy to extend with custom filters or conditions  
✅ Smooth stacking visuals with layout support  

This design supports scalability and flexibility—perfect for expanding gameplay systems like production lines, customer queues, delivery systems, or crafting mechanics.
