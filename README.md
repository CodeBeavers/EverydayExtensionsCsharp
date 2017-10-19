# EverydayExtensionsCsharp
This project contains examples of the `C#` extensions for everyday usage.
I am using them in each of my projects and happy about it :)


## Collection extensions

```csharp
public static List<T> NullToEmpty<T>(this List<T> source)
{
    return source ?? new List<T>();
}
```

```csharp
public static T[] ExpandArray<T>(this T[] array, T item)
{
    if (array == null || array.Length == 0)
    {
        array = new[] { item };
        return array;
    }

    var expandedArray = new T[array.Length + 1];
    Array.Copy(array, expandedArray, array.Length);
    expandedArray[array.Length] = item;

    return expandedArray;
}
```

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

## Json helpers (JSON.NET is required)

```csharp
public static string ToJson<T>(this T obj)
{
    return JsonConvert.SerializeObject(obj, Formatting.Indented);
}
```

## HttpRequest

```csharp
public static Encoding GetEncodingFromRequest(this HttpRequest request)
{
    try
    {
        var contentTypeHeader = request.Headers["Content-Type"];
        if (!contentTypeHeader.Any())
            return Encoding.UTF8;

        var contentType = new ContentType(contentTypeHeader);
        var charset = contentType.CharSet ?? "UTF-8";

        return Encoding.GetEncoding(charset);
    }
    catch
    {
        return null;
    }
}
```

## Entity Framework

```csharp
public static IQueryable<TEntity> Includes<TEntity>(this IQueryable<TEntity> source, 
    params Expression<Func<TEntity, object>>[] includes)
    where TEntity : class
{
    foreach (var include in includes)
    {
        source = source.Include(include);
    }
    
    return source;
}
```
