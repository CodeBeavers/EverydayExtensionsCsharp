# EverydayExtensionsCsharp


## String's extensions

```csharp
public static bool IsNullOrEmpty(this string value)
{
    return string.IsNullOrEmpty(value);
}
```

```csharp
public static bool NotNullOrEmpty(this string value)
{
    return !string.IsNullOrEmpty(value);
}
```