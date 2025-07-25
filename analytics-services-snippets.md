## Using Analytics Event Services with DI

This snippet demonstrates how I integrate analytics into my projects in a decoupled, scalable way using **Dependency Injection**. The goal is to abstract analytics calls from specific SDK implementations, allowing easy swapping or expansion of services.

---

### 🔹 1. Define an Interface

I begin with a simple, generic interface that supports various overloads for event tracking.

```csharp
public interface IAnalyticsEventService
{
    void SendCustomEvent(string eventName);
    void SendCustomEvent(string eventName, float value);
    void SendCustomEvent(string eventName, IDictionary<string, object> customField);
}
```

---

### 🔹 2. Implement a Concrete Service

In this case, I use GameAnalytics as the main analytics SDK. The class implements the `IAnalyticsEventService` interface.

```csharp
public class GameAnalyticsEventService : IAnalyticsEventService
{
    public void SendCustomEvent(string eventName)
    {
        GameAnalytics.NewDesignEvent(eventName);
    }

    public void SendCustomEvent(string eventName, float value)
    {
        GameAnalytics.NewDesignEvent(eventName, value);
    }

    public void SendCustomEvent(string eventName, IDictionary<string, object> customField)
    {
        GameAnalytics.NewDesignEvent(eventName, customField);
    }
}
```

> If I want to integrate more SDKs (like Firebase, Unity Analytics, Facebook, or even custom loggers), I can add more services implementing this interface.

---

### 🔹 3. Register with Dependency Container

In the `SDKInstaller`, I register my analytics service as a **singleton**, ensuring one instance throughout the app. Reflex's `ContainerBuilder` is used here.

```csharp
public class SDKInstaller : MonoBehaviour, IInstaller
{
    public void InstallBindings(ContainerBuilder containerBuilder)
    {
        // Other SDKs
        containerBuilder.AddScoped(typeof(GameAnalyticsService), typeof(ISDKService));
        containerBuilder.AddScoped(typeof(FacebookSDKService), typeof(ISDKService));
        containerBuilder.AddScoped(typeof(DummySDKService), typeof(ISDKService));

        // Analytics Event Service
        containerBuilder.AddSingleton(typeof(GameAnalyticsEventService), typeof(IAnalyticsEventService));
    }
}
```

---

### 🔹 4. Inject and Use in Your Systems

Anywhere I need to send analytics, I inject all available implementations of `IAnalyticsEventService`. This allows me to broadcast events to multiple SDKs simultaneously if needed.

```csharp
[Inject] private IEnumerable<IAnalyticsEventService> _analyticsEventServices;

...

foreach (var service in _analyticsEventServices)
{
    service.SendCustomEvent(
        $"Level_01:OrderServed:{CurrentOrder.GetItemIds().First()}",
        _customerAnalyticsData.TotalOrdersServed
    );
}
```

---

### 🔹 5. Benefits

- **Open/Closed Principle**: I can add new analytics backends without modifying existing code.
- **Testability**: Easily mock `IAnalyticsEventService` during unit tests.
- **Scalability**: Add as many implementations as needed, and they’ll all receive the same event.
- **Swapability**: Replace `GameAnalyticsEventService` with another service by changing only the installer.

---
