# 📦 Orbyss.Blazor.Syncfusion.JsonForms

**A full-featured Syncfusion-based UI renderer for [Orbyss.Blazor.JsonForms](https://github.com/orbyss-io/Orbyss.Blazor.JsonForms).**  
This package brings the power of Syncfusion Blazor components to schema-driven forms using [jsonforms.io](https://jsonforms.io/) standard. All you need need to generate your JSON forms are: 1) JSON Schema, 2) UI Schema, and 3) Translation Schema.
If you notice anything that is not working as you expect, please either let us know, or implement your own Components (see [Orbyss.Blazor.JsonForms README](https://github.com/orbyss-io/Orbyss.Blazor.JsonForms) how to do that)

![NuGet](https://img.shields.io/nuget/v/Orbyss.Blazor.Syncfusion.JsonForms)
![NuGet Downloads](https://img.shields.io/nuget/dt/Orbyss.Blazor.Syncfusion.JsonForms)
---

## 🎯 What is this?

This package implements the **`IFormComponentInstanceProvider`** interface for Syncfusion — plugging into the [Orbyss.Blazor.JsonForms](https://github.com/orbyss-io/Orbyss.Blazor.JsonForms) core form engine.

✅ You don’t need to write your own component provider  
✅ Just install this NuGet package and use `<JsonForm ... />` as normal
✅ Make sure to either inject `SyncfusionComponentInstanceProvider` in your DI container, or pass a fresh instance as parameter to 
`<JsonForm ComponentInstanceProvider=@provider ... >`

---

## 🧱 Components Rendered with Syncfusion

All form controls are implemented using Syncfusion Blazor components:

- ✅ `SfTextBox`, `SfDropDownList`, `SfSwitch`, `SfDatePicker`, etc.
- ✅ Supports layout controls like Grid, Columns, Lists, Buttons, and Stepper Navigation
- ✅ Fully compatible with cascading properties: `Language`, `Disabled`, `ReadOnly`
- ✅ Custom UI behavior via `options` in your UI schema

---

## 🚀 Quickstart

#### Syncfusion dependency
This library uses Syncfusion Blazor components internally. This package is built and tested against Syncfusion.Blazor 32.1.x.

#### Recommended (simplest)
Reference the Syncfusion Blazor bundle in .csproj. This includes all required Syncfusion components:
```xml
<PackageReference Include="Syncfusion.Blazor" Version="32.1.*" />
```

#### Advanced usage
If you prefer per-component packages, reference the required ones instead:
```xml
<PackageReference Include="Syncfusion.Blazor.Buttons" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.Calendars" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.DropDowns" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.Grid" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.Inputs" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.Navigations" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.SplitButtons" Version="32.1.*" />
<PackageReference Include="Syncfusion.Blazor.Themes" Version="32.1.*" />
```
Then add `Orbyss.Blazor.Syncfusion.JsonForms`
```bash
dotnet add package Orbyss.Blazor.Syncfusion.JsonForms
```

Then in Program.cs:
``` csharp
// Register Syncfusion Blazor Core services
builder.Services.AddSyncfusionBlazor();

// Register Syncfusion JSON Forms
builder.Services.AddSyncfusionJsonForms();
```

Then finally you can define the JsonForm Blazor component as follows:
```csharp
<JsonForm InitOptions=@options ComponentInstanceProvider=... />

@code {
    JsonFormContextInitOptions options = new(
        jsonSchema,
        uiSchema,
        translationSchema
    );
}
```
---

## ⚙️ Customization

One way to override default behavior is by subclassing or replacing specific Syncfusion components. Example:

```csharp
public class CustomProvider : SyncfusionFormComponentInstanceProvider
{
    public override InputFormComponentInstanceBase GetInputField(IJsonFormContext context, FormControlContext control)
    {
        if (control.JsonPath == "#/properties/mySpecialField")
            return new MyCustomInputInstance();

        return base.GetInputField(context, control);
    }
}
```

Another way is to configure specific delegates in the `SyncfusionFormComponentInstanceProviderOptions`. Example:
```csharp
var instanceProviderOptions = new SyncfusionFormComponentInstanceProviderOptions
{
    ConfigureButton = (defaultButton, type, form) =>
    {
        defaultButton.CanToggle = true;
        return defaultButton;
    },
    ConfigureBooleanInput = (defaultInstance, controlContext) =>
    {
        var customOption = $"{controlContext.Interpretation.GetOption("custom-boolean")}";
        if (customOption == "switch")
        {
            return new MyCustomSwitchInputInstance();
        }

        return defaultInstance;
    }
};
```

Or of course, you can provide and completely override your own components entirely, injecting the parameters and controlling the behavior as you wish (see the full example in [Orbyss.Blazor.JsonForms README](https://github.com/orbyss-io/Orbyss.Blazor.JsonForms)).

---

## 🔄 Under the hood: Powered by 3 schemas

Like all Orbyss JSON Forms integrations, this renderer works using:

| Schema              | Purpose                                             |
|---------------------|-----------------------------------------------------|
| **JSON Schema**     | Defines data structure (types, constraints, etc.)   |
| **UI Schema**       | Controls layout and per-control options, [rules](https://jsonforms.io/docs/uischema/rules/)             |
| **Translation Schema** | Manages localization, labels, error messages    |

All schema interactions are fully supported.

---

## 🧩 Other UI Options

Prefer a different component library? Try:

- 🎨 [Orbyss.Blazor.MudBlazor.JsonForms](https://www.nuget.org/packages/Orbyss.Blazor.MudBlazor.JsonForms)
- Or implement your own renderer via `IFormComponentInstanceProvider`

---

## 📄 License
MIT License  
© Orbyss.io

---

## 🔗 Links

- 🌍 **Website**: [https://orbyss.io](https://orbyss.io)
- 📦 **Core Engine**: [Orbyss.Blazor.JsonForms](https://www.nuget.org/packages/Orbyss.Blazor.JsonForms)
- 📦 **This Package**: [Orbyss.Blazor.Syncfusion.JsonForms](https://www.nuget.org/packages/Orbyss.Blazor.Syncfusion.JsonForms)
- 🧑‍💻 **GitHub**: [https://github.com/orbyss-io](https://github.com/orbyss-io)
- 📚 **Syncfusion Docs**: [Syncfusion Blazor UI](https://blazor.syncfusion.com/)
- 📝 **License**: [MIT](./LICENSE)

---


## 🤝 Contributing

This project is open source and contributions are welcome!

Whether it's bug fixes, improvements, documentation, or ideas — we encourage developers to get involved.  
Just fork the repo, create a branch, and open a pull request.

We follow standard .NET open-source conventions:
- Write clean, readable code
- Keep PRs focused and descriptive
- Open issues for larger features or discussions

No formal contribution guidelines — just be constructive and respectful.

---

⭐️ Found this useful? [Give us a star](https://github.com/orbyss-io/Orbyss.Blazor.Syncfusion.JsonForms/stargazers) and help spread the word!
