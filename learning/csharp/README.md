# C# Learning Notes: From Python to .NET

I'm learning C# with Python as a reference point. These notes record the concepts, small exercises and debugging details I want to understand before using them in larger .NET applications.

**Current progress:** console apps through enums and pattern matching, recorded on 6 October 2026.

[Read the full notes in Chinese, with annotated C# and Python examples](notes.md).

## Covered so far

| Part | Topic | Focus |
| --- | --- | --- |
| 1 | Console apps and program entry | C#, .NET, Visual Studio, output, comments and top-level statements |
| 2 | Variables, types and operators | Explicit types, type inference, numeric rules and Python comparisons |
| 3 | Visual Studio tools | Code search, Git Changes and keyboard navigation |
| 4 | Conditionals | if/else, switch statements, braces and break |
| 5 | Arrays | Indexing and array basics; the tutorial's early “List” section introduces arrays |
| 6 | Loops and string interpolation | for, while, foreach, break and interpolated strings |
| 7 | Functions and methods | Parameters, return values and calling code |
| 8 | Multiplication-table exercise | A small exercise combining loops and formatted output |
| 9 | Strings | Formatting and common string operations |
| 10 | Classes and objects | Fields, properties, constructors and instance members |
| 11 | Inheritance and polymorphism | Base classes, virtual/override and member hiding |
| 12 | Debugging | Breakpoints, F10, F11, Locals, Watch and Python pdb |
| 13 | Enums and pattern matching | Typed grades, switch expressions and Python Enum/match comparisons |

## A few useful lessons

- Similar syntax does not guarantee identical behaviour. C# integer division, type inference and method dispatch need their own explanations.
- A string mismatch such as `"Good"` versus `"good"` can compile and still produce the wrong result. An enum gives each grade a named, typed value.
- Stepping over a method with F10 still runs it. F11 follows the call into source when the debugger can step into it.
- Watch expressions can execute code. A method reference and a method invocation should be read differently.
- The example's grade field defaults to the enum's zero value. Calling `SetGrade()` before calculating the bonus matters.

## Next topics

The appendix contains a learning roadmap, rather than completed lessons: overloads and expression-bodied members, nullable types, static members, generics and List, Object, exceptions, naming conventions, interfaces, tuples and lambdas.

LINQ and async/await with Task are planned after these fundamentals.

## How these notes were made

I work through a tutorial and use Codex to help annotate examples, compare them with Python and explain debugging screenshots. The full notes distinguish screenshot code, corrections and additional examples.

Python examples in the recent debugging and enum sections were executed to check behaviour. The C# examples in those sections were reviewed against Microsoft documentation; they were not compiled in the note-generation environment. Some snippets deliberately illustrate errors or intermediate tutorial states, so they are not all standalone programs.

The Python comparisons explain similar purposes while preserving differences between the languages.

## Sources

- [The C# tutorial I'm following](https://www.youtube.com/watch?v=KeqUmyNsNb4)
- [Microsoft C# documentation](https://learn.microsoft.com/en-us/dotnet/csharp/)
- [Microsoft .NET documentation](https://learn.microsoft.com/en-us/dotnet/)
- [Python documentation](https://docs.python.org/3/)

Specific reference links are included in the relevant chapters.
