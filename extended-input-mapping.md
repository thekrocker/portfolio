# Extended Input Mapping System in Unity

This system abstracts Unity's **Input System** into a modular and extendable interface for reading inputs and mapping them to UI prompts, actions, or gameplay logic. It allows dynamic key rebinding, clean separation of logic, and context-based control usage.

---

## 🧩 Interfaces & Abstractions

### `IInputService`
```csharp
public interface IInputService
{
    bool GetKeyDown(string actionName);
    bool GetKey(string actionName);
    bool GetKeyUp(string actionName);
    string GetKeyBindingDisplay(string actionName);
}
```

### `InputService`
```csharp
public class InputService : IInputService
{
    private readonly Dictionary<string, InputActionReference> _bindings;

    public InputService(Dictionary<string, InputActionReference> bindings)
    {
        _bindings = bindings;
    }

    public bool GetKeyDown(string actionName)
    {
        return _bindings.TryGetValue(actionName, out var action) && action.action.WasPressedThisFrame();
    }

    public bool GetKey(string actionName)
    {
        return _bindings.TryGetValue(actionName, out var action) && action.action.IsPressed();
    }

    public bool GetKeyUp(string actionName)
    {
        return _bindings.TryGetValue(actionName, out var action) && action.action.WasReleasedThisFrame();
    }

    public string GetKeyBindingDisplay(string actionName)
    {
        if (_bindings.TryGetValue(actionName, out var action))
        {
            return action.action.GetBindingDisplayString();
        }
        return "Unbound";
    }
}
```

---

## 🎮 Use Cases

### 1. **Displaying Input Prompts in UI**
```csharp
[Inject] private IInputService _inputService;

private void UpdateKeyPrompt()
{
    string display = _inputService.GetKeyBindingDisplay("Use");
    promptText.text = $"Press [{display}] to interact";
}
```

### 2. **Custom Key Binds for Vehicles**
```csharp
if (_inputService.GetKey("Accelerate"))
{
    vehicle.MoveForward();
}
if (_inputService.GetKey("Brake"))
{
    vehicle.Stop();
}
```

### 3. **Gameplay: Input for Picking Up Items**
```csharp
if (_inputService.GetKeyDown("Pickup") && isItemNearby)
{
    inventory.AddItem(nearbyItem);
}
```

### 4. **Opening/Closing Inventory or Menus**
```csharp
if (_inputService.GetKeyDown("Inventory"))
{
    inventoryUI.Toggle();
}
```

---

## 💡 Benefits

- Easily support **rebindable keys**.
- Switch **input maps** per context (vehicle, UI, gameplay).
- Dynamically show user-friendly prompts without hardcoded keys.
- Abstract away Unity's direct `InputAction` usage — unit testable and mockable.

---

## 🔧 Notes

- Use `PlayerInput` component to manage input map switching.
- Bind all `InputActionReference` instances from a central configuration point (ScriptableObject or Bootstrapper).
- Supports adding gamepad bindings and joystick actions in future with the same system.

