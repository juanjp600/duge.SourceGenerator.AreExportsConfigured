# duge.SourceGenerators.AreExportsConfigured

Generates an `AreExportsConfigured` method for every C# node you define for a Godot project. It returns false if any of the node's exported members are null.

This method has the [MemberNotNullWhen](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/attributes/nullable-analysis#helper-methods-membernotnull-and-membernotnullwhen) attribute to allow the C# compiler to issue warnings in a [nullable context](https://learn.microsoft.com/en-us/dotnet/csharp/nullable-references).

Usage example:
```cs
public partial class MyNodeA : Node
{
    [Export]
    public MyNodeB? ExportedNode { get; set; }

    public override void DoThing()
    {
        if (!AreExportsConfigured())
        {
            // Returns if ExportedNode is null
            return;
        }

        // No warning issued by the compiler because of the check above
        ExportedNode.DoOtherThing();
    }
}
```
