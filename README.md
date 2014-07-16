UCreate [![Build status](https://ci.appveyor.com/api/projects/status/60v4v2cbl6nxmf0q)](https://ci.appveyor.com/project/nicbell/ucreate)
=======

Create DataTypes and MediaTypes for Umbraco 7 using code-first approach. Inspired by [USiteBuilder](https://github.com/spopovic/uSiteBuilder).

Available on NuGet
---
```
PM> Install-Package UCreate
```

Usage
---

Adding HTTP module to ```web.config```

```xml
...
<system.web>
	<httpModules>
		...
		<add name="CmsSyncHttpModule" type="NicBell.UCreate.CmsSyncHttpModule, NicBell.UCreate" />
	</httpModules>
</system.web>
...
<system.webServer>
	...
	<modules runAllManagedModulesForAllRequests="true">
		...
		<add name="CmsSyncHttpModule" type="NicBell.UCreate.CmsSyncHttpModule, NicBell.UCreate" />
	</modules>
	...
</system.webServer>
...
```

DataType Example
---
```csharp
[CustomDataType(EditorAlias = "Umbraco.ColorPickerAlias",
    Name = "Nice Color Picker",
    Key = "1bfca1e7-95d0-485e-bd94-9fe9c2b8821f",
    DBType = DataTypeDatabaseType.Nvarchar)]
public class NiceColorPicker : CustomDataTypeBase
{
    public override IDictionary<string, PreValue> PreValues
    {
        get
        {
            return new Dictionary<string, PreValue> {
                {"1", new PreValue("ff00ff")},
                {"2", new PreValue("1f00f1")},
                {"3", new PreValue("123123")}
            };
        }
    }
}
```

MediaType Example
---
```csharp
[CustomMediaType(SyncOrder = 2,
    Name = "Folder With Cover",
    Alias = "FolderWithCover",
    Key = "f188043d-62c5-40f5-b1b0-a4a83b21a902",
    Icon = "icon-folder color-blue",
    AllowedAsRoot = true,
    IsContainer = true,
    AllowedTypes = new[] { "FolderWithCover", "Image" })]
public class FolderWithCover
{
    [CustomTypeProperty(Alias = "coverImage", TypeName = PropertyTypes.MediaPicker, Description = "Cover image.", Mandatory = true)]
    public string CoverImage { get; set; }
}
```