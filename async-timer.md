
# AsyncTickTimer

`AsyncTickTimer` is a utility class designed for Unity using UniTask to run asynchronous timers with tick updates. It is helpful for situations where you want continuous progress reporting over a defined duration, such as visual progress bars, delayed actions, or step-based animations.

## Features

- 🔁 Ticks continuously using `Time.deltaTime`
- ⏱️ Sends progress through `OnTick` event (normalized 0-1)
- ✅ Triggers `OnCompleted` event when finished
- ✋ Can be `Paused`, `Resumed`, or `Canceled`
- 🔄 Works with `CancellationToken` for external control

## Events

- `OnTick(float)` — Invoked every tick with normalized progress (0-1).
- `OnCompleted()` — Called once the timer finishes.
- `OnCanceled()` — Called if timer is canceled.
- `OnPause(bool)` — Called when paused/resumed.

## Usage Example

```csharp
AsyncTickTimer timer = new AsyncTickTimer(3f); // 3 seconds

timer.OnTick += progress => Debug.Log($"Progress: {progress:P0}");
timer.OnCompleted += () => Debug.Log("Timer completed!");
timer.OnCanceled += () => Debug.Log("Timer canceled!");

await timer.StartAsync(); // Can be awaited inside UniTask-compatible methods
```

## Pausing / Resuming / Canceling

```csharp
timer.Pause();
timer.Resume();
timer.Cancel();
```

## Integration Tip

You can inject a cancellation token from `CancellationTokenSource` to externally stop the timer or tie it to another lifecycle.

```csharp
var cts = new CancellationTokenSource();
await timer.StartAsync(cts.Token);
```

## Namespace

```csharp
using Safa.Utils;
```

## Dependencies

- [UniTask (Cysharp.Threading.Tasks)](https://github.com/Cysharp/UniTask)
- Unity `Time.deltaTime` (must be run during play mode)
