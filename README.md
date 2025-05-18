# SharpResults 📊

![GitHub Repo stars](https://img.shields.io/github/stars/RezaArda/SharpResults?style=social) ![NuGet](https://img.shields.io/nuget/v/SharpResults) ![License](https://img.shields.io/badge/license-MIT-blue.svg)

Welcome to **SharpResults**, a lightweight, zero-dependency C# library that implements the Result pattern for more explicit and type-safe error handling. With SharpResults, you can avoid using exceptions for control flow, making success and failure states clear in your code.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Features

- **Zero Dependencies**: SharpResults is designed to be lightweight and easy to integrate into your existing projects.
- **Type-Safe Error Handling**: Implement the Result pattern to handle errors without exceptions.
- **Fluent API**: Enjoy a clean and intuitive API for handling results.
- **Functional Programming Support**: Use functional programming concepts to enhance your code quality.
- **Monads**: Work with monads to manage side effects and improve code clarity.

## Installation

You can easily add SharpResults to your project via NuGet. Use the following command in your Package Manager Console:

```bash
Install-Package SharpResults
```

Alternatively, you can search for "SharpResults" in the NuGet Package Manager within Visual Studio.

For the latest releases, visit the [Releases section](https://github.com/RezaArda/SharpResults/releases).

## Usage

Using SharpResults is straightforward. Below is a simple example to get you started.

### Basic Example

```csharp
using SharpResults;

public class Example
{
    public Result<int> Divide(int numerator, int denominator)
    {
        if (denominator == 0)
        {
            return Result.Fail<int>("Cannot divide by zero.");
        }
        
        return Result.Ok(numerator / denominator);
    }
}
```

In this example, the `Divide` method returns a `Result<int>`. If the denominator is zero, it returns a failure result with an error message.

### Handling Results

You can easily handle results using the `OnSuccess` and `OnFailure` methods:

```csharp
var result = new Example().Divide(10, 0);

result.OnSuccess(value => Console.WriteLine($"Result: {value}"))
      .OnFailure(error => Console.WriteLine($"Error: {error}"));
```

This approach allows you to manage success and failure states clearly.

## Examples

### Chaining Results

SharpResults supports chaining, allowing you to create a sequence of operations:

```csharp
var result = new Example()
    .Divide(10, 2)
    .OnSuccess(value => new Example().Divide(value, 2));

result.OnSuccess(value => Console.WriteLine($"Final Result: {value}"))
      .OnFailure(error => Console.WriteLine($"Error: {error}"));
```

### Combining Results

You can also combine multiple results into a single result:

```csharp
var result1 = new Example().Divide(10, 2);
var result2 = new Example().Divide(20, 4);

var combinedResult = Result.Combine(result1, result2);

combinedResult.OnSuccess(() => Console.WriteLine("Both operations succeeded."))
              .OnFailure(error => Console.WriteLine($"Error: {error}"));
```

## API Reference

For a comprehensive list of methods and classes, check the official documentation. You can also explore the source code in the repository.

## Contributing

We welcome contributions to SharpResults. To contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/YourFeature`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add new feature'`).
5. Push to the branch (`git push origin feature/YourFeature`).
6. Open a Pull Request.

Please ensure your code adheres to our coding standards and includes tests where applicable.

## License

SharpResults is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

Thanks to all contributors and the open-source community for their support. Your contributions make projects like SharpResults possible.

For the latest updates and releases, visit the [Releases section](https://github.com/RezaArda/SharpResults/releases). 

---

Feel free to explore the code, report issues, and suggest improvements. Happy coding!