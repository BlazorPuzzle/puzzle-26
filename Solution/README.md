# Blazor Puzzle #26

## From RCL to Routable Page

YouTube Video: https://youtu.be/n9nNZye-ns0

BlazorPuzzle Home Page: https://blazorpuzzle.com

### The Challenge:

We have a Blazor Web App with a reference to a Razor Class Library project, in which we have the default Component1 component.

We can show that component easily in the Blazor app, but how can we make it routable so we can navigate to it?

### The Solution:

Step 1 of the solution is to add `AdditionalAssemvblies` to the `<Router>`:

*Routes.razor*:

```xml
<Router AppAssembly="typeof(Program).Assembly" AdditionalAssemblies="new [] {typeof(MyStuff.Component1).Assembly}">
    <Found Context="routeData">
        <RouteView RouteData="routeData" DefaultLayout="typeof(Layout.MainLayout)" />
        <FocusOnNavigate RouteData="routeData" Selector="h1" />
    </Found>
</Router>
```

Step 2 is to add `AdditionalAssemblies` in *Program.cs*:

*Program.cs*:

```c#
app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode()
    .AddAdditionalAssemblies(typeof(MyStuff._Imports).Assembly);
```

Step 3 is to add a `@page` directive to the top of `Component1`:

*Component1.razor*:

```xml
@page "/component1"
<div class="my-component">
    This component is defined in the <strong>MyStuff</strong> library.
</div>
```

