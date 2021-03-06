# Allure NUnit adapter
NUnit adapter for Allure Framework 

[![Build status](https://ci.appveyor.com/api/projects/status/5nomj0qw25bo8gnv?svg=true)](https://ci.appveyor.com/project/unickq/allure-nunit)[![NuGet](http://flauschig.ch/nubadge.php?id=NUnit.Allure)](https://www.nuget.org/packages/NUnit.Allure)[![Steps](http://flauschig.ch/nubadge.php?id=NUnit.Allure.Steps)](https://www.nuget.org/packages/NUnit.Allure.Steps)

### Allure report:

![Allure report](https://raw.githubusercontent.com/unickq/allure-nunit/master/AllureScreen.png)

### Code example:

```cs
[TestFixture(Author = "unickq", Description = "Examples")]
[AllureNUnit]
[AllureLink("https://github.com/unickq/allure-nunit")]
public class Tests
{
    [OneTimeSetUp]
    public void ClearResultsDir()
    {
        AllureLifecycle.Instance.CleanupResultDirectory();
    }

    //Allure.Steps required
    [AllureStep("This method is just saying hello")]
    private void SayHello()
    {
        Console.WriteLine("Hello!");
    }

    [Test]
    [AllureTag("NUnit", "Debug")]
    [AllureIssue("GitHub#1", "https://github.com/unickq/allure-nunit")]
    [AllureSeverity(SeverityLevel.critical)]
    [AllureFeature("Core")]
    public void EvenTest([Range(0, 5)] int value)
    {
        SayHello();
            
        //Wrapping Step
        AllureLifecycle.Instance.WrapInStep(
            () => { Assert.IsTrue(value % 2 == 0, $"Oh no :( {value} % 2 = {value % 2}"); },
            "Validate calculations");
    }
}
```  

### ToDo:
- [x] NET Standard 2.0 (NET 4.5 without steps)
- [x] Parallelizable test support
- [x] Attachments
- [x] Allure SetUp/TearDown support
- [x] Console Output as attached file
- [x] Add ignored (not started) tests to results. Assert.Ignore() works :) [AllureDisplayIgnored]
- [x] [Steps](https://github.com/unickq/allure-nunit/wiki/AllureStep) attribute for non-test methods

### Installation and Usage
- Download from Nuget with all dependencies
- Configure allureConfig.json
- Set `[AllureNUnit]` attribute under test fixture
- Use other [attributes](https://github.com/unickq/allure-nunit/wiki/Attributes) if needed