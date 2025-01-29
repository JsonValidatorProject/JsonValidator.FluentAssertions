# `{✓}` JSON Validator for Fluent Assertions
> [!warning]
> Due to licencing changes, the FluentAssertions library won't be updated above v7.1 (the last truely free version). We recommend using [Shouldly](https://github.com/shouldly/shouldly) and our [Shouldly extension](https://github.com/JsonValidatorProject/JsonValidator.Shouldly) instead.

This project provides a simple way to validate JSON objects in dotnet. The main use for the tool is in integration tests where you would — ideally — validate an API JSON response manually instead of using the model classes.

[![Build Status](https://github.com/JsonValidatorProject/JsonValidator.FluentAssertions/workflows/build-and-test/badge.svg "Build Status")](https://github.com/JsonValidatorProject/JsonValidator.FluentAssertions/actions?query=workflow%3A%22build-and-test%22)
[![Coverage](https://codecov.io/gh/JsonValidatorProject/JsonValidator.FluentAssertions/branch/main/graph/badge.svg)](https://codecov.io/gh/JsonValidatorProject/JsonValidator.FluentAssertions)
[![Nuget: JsonValidator.FluentAssertions](https://img.shields.io/nuget/v/JsonValidator.FluentAssertions?label=JsonValidator.FluentAssertions&logo=nuget)](https://www.nuget.org/packages/JsonValidator.FluentAssertions)
[![License: MIT](https://img.shields.io/badge/license-MIT-blueviolet)](https://opensource.org/licenses/MIT)
[![pull requests: welcome](https://img.shields.io/badge/pull%20requests-welcome-brightgreen)](https://github.com/JsonValidatorProject/JsonValidator/fork)

## Usage
- The `JsonValidator.FluentAssertions` package depends on and uses both [FluentAssertions](https://github.com/fluentassertions/fluentassertions) and the basic [JsonValidator](https://github.com/JsonValidatorProject/JsonValidator) package.
- This package provides extensions that can be accessed through FluentAssertions' `Should()` method.
- Available extensions:
  - for `System.Text.Json.JsonDocument`: `Match(...)` checks whether the JSON document matches the input object in both structure and values.
  - for `System.Net.Http.HttpResponseMessage`: `HaveJsonBody(...)` checks whether the HTTP response's body as a JSON string matches the input object in both structure and values.

### Examples
For `JsonDocument`:
```csharp
var json = JsonDocument.Parse(myJsonString);

json.Should().Match(
  new
  {
      name = "Anna Smith",
      level = 2,
  },
  "Because...");
```

For `HttpResponseMessage`:
```csharp
HttpResponseMessage response = await _client.SendAsync(request);

response.Should().HaveJsonBody(
  new
  {
      name = "Anna Smith",
      level = 2,
  },
  "Because...");
```
