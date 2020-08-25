---
title: 'Basics of xUnit with .NET Core and VS Code'
date: 2020-05-06T19:48:30+03:00
author: 'codevictory'
description: 'How to get started with xUnit, .NET Core and VS Code.'
draft: false
---

## VS Code Extension

Extension: [NXUnit Test Explorer](https://marketplace.visualstudio.com/items?itemName=wghats.vscode-nxunit-test-adapter)

---

You need this to enable intellisense for xUnit library. GUI plugin in VS Code sidebar itself is faulty and useless. Under rigth-click menu there is option to hide it.

---

## Nuget packages

|                         |                                                                                        |
| ----------------------- | -------------------------------------------------------------------------------------- |
| Main library            | [xunit](https://www.nuget.org/packages/xunit/)                                         |
| Test runner application | [xunit.runner.visualstudio](https://www.nuget.org/packages/xunit.runner.visualstudio/) |

---

`dotnet new xunit` will create references to `Microsoft.NET.Test.Sdk` and `coverlet.collector` but I didn't find any use for them.

---

## Example test

```csharp
[Theory]
[InlineData(5.5, 3)]
[InlineData(14, 100)]
[InlineData(-45, 11)]
public void GetSarcophagi_OutputCheck(double sarcophagusLength, int sargophagusQuantity)
{
    var sarcophagi = TestDataGenerator.GetSargophagi(sarcophagusLength, sarcophagusQuantity);

    Assert.NotNull(sarcophagi); // Sarcophagus generator actually returns something.
    Assert.Equal(sargophagusQuantity, sarcophagi.Count); // Given quantity is respected.

    foreach (var sarcophagus in sarcophagi)
    {
        Assert.Equal(sarcophagusLength, sarcophagus.Length); // Given length is respected.
    }
}
```

### About comparison assertions

Every comparison assertion function's (like _Equal()_ or _Same()_) first parameter is _expected value_ and
the second is _actual value_. By keeping tested values always logically the same way you can keep track on
which value is which since, if test fails, explanation addresses values by _expected_ or _actual_.

## Running tests

```dotnetcli
dotnet test
```

Output should be something like:

```dotnet
A total of 1 test files matched the specified pattern.

Test Run Successful.
Total tests: 24
     Passed: 24
 Total time: 1.7065 Seconds

Test Run Successful.
Total tests: 5
     Passed: 5
 Total time: 1.7823 Seconds
```

I never managed to get any other total of test files matched than 1. I'd advise not to mind that.
