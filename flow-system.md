# 🌀 Flow System

The `FlowSystem` provides a clean, composable way to orchestrate sequences of gameplay logic or scene transitions using a set of independently defined steps.

---

## 🔧 Core Concept

The system is built around two main components:

### `IFlowStep`

```csharp
public interface IFlowStep
{
    UniTask ExecuteAsync();
    bool CanExecute();
}
```

Represents an atomic piece of logic that can run conditionally.

### `FlowRunner`

```csharp
public class FlowRunner
{
    private readonly List<IFlowStep> _steps;

    public FlowRunner(List<IFlowStep> steps) => _steps = steps;

    public async UniTask RunAsync()
    {
        foreach (var step in _steps)
        {
            if (step.CanExecute())
                await step.ExecuteAsync();
        }
    }
}
```

You build and inject your logic into the runner and execute the flow.

---

## ✅ Example Steps

### 1. `SetPlayerInputFlowStep`

```csharp
public class SetPlayerInputFlowStep : IFlowStep
{
    private readonly bool _status;
    private readonly IPlayerController _playerController;

    public SetPlayerInputFlowStep(bool status, IPlayerController playerController)
    {
        _status = status;
        _playerController = playerController;
    }

    public async UniTask ExecuteAsync()
    {
        if (_status) _playerController.EnableInput();
        else _playerController.DisableInput();
    }

    public bool CanExecute() => true;
}
```

### 2. `SwitchCameraToFlowStep`

```csharp
public class SwitchCameraToFlowStep : IFlowStep
{
    private readonly ICameraService _cameraService;
    private readonly Transform _followTarget;
    private readonly ECameraType _cameraType;
    private readonly bool _returnToPrevious;

    public SwitchCameraToFlowStep(ICameraService camService, Transform followTarget, ECameraType cameraType, bool returnToPrevious)
    {
        _cameraService = camService;
        _followTarget = followTarget;
        _cameraType = cameraType;
        _returnToPrevious = returnToPrevious;
    }

    public async UniTask ExecuteAsync()
    {
        await _cameraService.SwitchTo(_cameraType, _followTarget, _returnToPrevious);
    }

    public bool CanExecute() => true;
}
```

---

## 🧠 Use Cases

- 🎬 **Cutscene flow**: disable input, switch camera, play animation, re-enable input.
- 🎮 **Game phase transitions**: initialize systems, lock UI, show tutorial, start match.
- 📦 **Tutorial systems**: guide players step-by-step by chaining flows.
- 📸 **Camera choreography**: define and reuse cinematic shots with `SwitchCameraToFlowStep`.
- 🚪 **Area transitions**: fade out, move player, change camera, fade in, re-enable input.

---

## 💡 Advantages

- Easy to compose and test
- High modularity and separation of concerns
- Supports async logic (e.g. animations, loading)
- Extendable with custom conditions, delays, etc.

---

## 🏁 Creating a Flow

```csharp
var steps = new List<IFlowStep>
{
    new SetPlayerInputFlowStep(false, playerController),
    new SwitchCameraToFlowStep(cameraService, bossTransform, ECameraType.Cinematic, true),
    new SetPlayerInputFlowStep(true, playerController)
};

await new FlowRunner(steps).RunAsync();
```

---

## 🧱 Extend It

You can create your own steps like:

- Wait for seconds
- Play a sound
- Show dialog
- Teleport player
- Trigger enemy AI

Simply implement `IFlowStep`.