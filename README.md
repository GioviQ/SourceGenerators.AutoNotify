# Source Generators

[![NuGet](https://img.shields.io/nuget/v/SourceGenerators.AutoNotify.svg?style=flat-square)](https://www.nuget.org/packages/SourceGenerators.AutoNotify/)

## AutoNotify

Original code from https://github.com/dotnet/roslyn-sdk/tree/main/samples/CSharp/SourceGenerators

### Default attribute arguments
```cs
[AutoNotify(CheckEquality = EqualityCheck.None, GetterVisibility = Visibility.Public, SetterVisibility = Visibility.Public)]
```

## Example

```cs
public partial class Filter
{
    [AutoNotify]
    private DateTime? _from;

    [AutoNotify]
    private DateTime? _to;
}
```

## Source Generator output

```cs
public partial class Filter : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    public DateTime? From 
    {
      get
      {
        return _from;
      }
      set
      {
        _from = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(From)));
      }
    }
     
    public DateTime? To 
    {
      get
      {
        return _to;
      }
      set
      {
        _to = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(To)));
      }
    }
}
```
