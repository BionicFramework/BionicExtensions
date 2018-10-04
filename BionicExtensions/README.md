# Bionic Extensions

Simple extensions to aid with Bionic development model.

### Install
```bash
dotnet -i BionicExtensions
```

### Contents

#### Injectable Attribute

**Intent:**

Automatically register new services with Blazor's ServiceCollection.

**Usage:**

1 - Add InjectableAttribute.RegisterInjectables function to your Blazor Startup.cs file:

```c#
namespace RxBlazor {
  public class Startup {
    public void ConfigureServices(IServiceCollection services) {
      InjectableAttribute.RegisterInjectables(services); // Add this line
    }

    public void Configure(IBlazorApplicationBuilder app) {
      app.AddComponent<App>("app");
    }
  }
}
```

2 - Annotate new services with Injectable attribute:

The Injectable attribute accepts two arguments: ```[Injectable(InterfaceType, ServiceType)]``` where:

InterfaceType = the annotated service interface
ServiceType = the type of service being registered: "singleton", "transient" or "scoped". default is "singleton"

The following example registers the CounterService as a Singleton for Dependency Injection with an interface of ICounterService. 
```C#
[Injectable(typeof(ICounterService))]
public class CounterService : ICounterService {
  // Service impl here...
}
```

If we want to make Transient instead of a Singleton, we can do:

```[Injectable(typeof(ICounterService), "transient")]```

For more information please refer to [Adding Service in DI](https://blazor.net/docs/dependency-injection.html#add-services-to-di) documentation.