# HiroixFramework
The Hiroix Framework is an application framework that was created to reduce boilerplate code and add common features to console and WinForms applications (MAUI support may be coming in the future). Hiroix Framework runs on [.NET 5](https://devblogs.microsoft.com/dotnet/announcing-net-5-0) and is written in C#.

Hiroix Framework ("HF") is constantly evolving as it is being used as the basis for multiple applications.

## Application Lifecycle
Before HF can take care of the functions of an application, it requires the following two classes to be created.

### AppPaths
This class derives from `Paths` and provides any File, Directory, and URL locations that your application can access via `App.Paths`. Any locations decorated with the `UserVisible` attribute will appear in appropriate locations such as the application's About form automatically.

```csharp
public class AppPaths : Paths
{
  public FileRef MyFile => this.DataDirectory + "MyFile.json";

  // The UserVisible() attribute can be omitted; with it, the link
  // will auto-appear in appropriate sections of your applications.
  [UserVisible("Website", "Hiroix Website", "Visit the Hiroix website...")]
  public UrlRef WebsiteUrl => "https://hiroix.com/";
}
```

### AppSettings
This class derives from `SerializableObject` and contains your application's settings which are accessible via `App.Settings`. The settings are loaded at application start-up and saved at shutdown; a save can be requested at any time via `App.Settings.Save()`.

```csharp
public class AppSettings : SerializableObject
{
  // Any properties are automatically (de)serialised on app start/shutdown.
  public StartupSettings Startup { get; init; } = new();
}
```

Once both classes are created, they can be plumbed in and HF can be instantiated using something similar to the following:

```csharp
internal readonly static WindowsFramework<AppPaths, AppSettings> App = new();
```

At this point, any configuration can be performed as you require, and then `App.Initialize()` is called. This initialises the entire HF system and performs the steps required to get your application set up. After this, you would pass in your application's main form via `App.Run()` to begin running it.

More information will be added to the [Wiki](https://github.com/BootBlock/Hiroix-Framework/wiki) over time.

A public release date for the Hiroix Framework has yet to be determined.
