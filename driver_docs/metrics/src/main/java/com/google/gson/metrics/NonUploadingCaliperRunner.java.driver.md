# Purpose
The provided Java source code defines a utility class named [`NonUploadingCaliperRunner`](#NonUploadingCaliperRunnerNonUploadingCaliperRunner) within the package `com.google.gson.metrics`. This class is designed to facilitate the execution of performance benchmarks using the Caliper framework, specifically by running benchmarks without uploading the results to a web application. The class achieves this by modifying the arguments passed to the Caliper runner to include a configuration that disables result uploads. This is particularly useful in scenarios where users want to run benchmarks locally without sharing results externally, addressing a specific issue noted in the Caliper project.

The class contains a private constructor, indicating that it is not intended to be instantiated. Instead, it provides a static method [`run`](#NonUploadingCaliperRunnerrun), which serves as the main entry point for executing benchmarks. The [`run`](#NonUploadingCaliperRunnerrun) method takes a `Class<?>` and a `String[]` as parameters, representing the benchmark class and additional arguments, respectively. It utilizes a private static method [`concat`](#NonUploadingCaliperRunnerconcat) to prepend a specific configuration string to the arguments, ensuring that the results upload feature is disabled. This class does not define public APIs or external interfaces beyond its static method, focusing narrowly on its intended functionality of running Caliper benchmarks without uploading results.
# Imports and Dependencies

---
- `com.google.gson.metrics`
- `com.google.caliper.runner.CaliperMain`


# Classes

---
### NonUploadingCaliperRunner<!-- {{#class:com.google.gson.metrics.NonUploadingCaliperRunner}} -->
- **Description**: The `NonUploadingCaliperRunner` class is designed to execute Caliper benchmarks without uploading the results to a web application, which is the default behavior of Caliper. It achieves this by modifying the arguments passed to the Caliper runner to include a flag that disables result uploads. The class contains a private constructor to prevent instantiation and a static method `run` that takes a class and an array of arguments, concatenating them with a specific option to disable uploads before invoking the Caliper runner.
- **Methods**:
    - [`com.google.gson.metrics.NonUploadingCaliperRunner.NonUploadingCaliperRunner`](#NonUploadingCaliperRunnerNonUploadingCaliperRunner)
    - [`com.google.gson.metrics.NonUploadingCaliperRunner.concat`](#NonUploadingCaliperRunnerconcat)
    - [`com.google.gson.metrics.NonUploadingCaliperRunner.run`](#NonUploadingCaliperRunnerrun)

**Methods**

---
#### NonUploadingCaliperRunner\.NonUploadingCaliperRunner<!-- {{#callable:com.google.gson.metrics.NonUploadingCaliperRunner.NonUploadingCaliperRunner}} -->
The `NonUploadingCaliperRunner` constructor is a private method that prevents instantiation of the class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which means it cannot be accessed from outside the class.
    - There is no implementation within the constructor, indicating that it is intentionally left empty to prevent instantiation.
- **Output**:
    - There is no output from this constructor as it is empty and private.
- **See also**: [`com.google.gson.metrics.NonUploadingCaliperRunner`](#NonUploadingCaliperRunner)  (Base Class)


---
#### NonUploadingCaliperRunner\.concat<!-- {{#callable:com.google.gson.metrics.NonUploadingCaliperRunner.concat}} -->
The `concat` method combines a single string with an array of strings into a new array.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `first`: The first string to be included in the resulting array.
    - `others`: A varargs parameter representing an array of additional strings to be concatenated with the first string.
- **Control Flow**:
    - Check if the `others` array is empty.
    - If `others` is empty, return a new array containing only the `first` string.
    - If `others` is not empty, create a new array `result` with a length of `others.length + 1`.
    - Assign the `first` string to the first position of the `result` array.
    - Use `System.arraycopy` to copy all elements from `others` into the `result` array starting from the second position.
    - Return the `result` array.
- **Output**:
    - A new array of strings that includes the `first` string followed by all strings in the `others` array.
- **See also**: [`com.google.gson.metrics.NonUploadingCaliperRunner`](#NonUploadingCaliperRunner)  (Base Class)


---
#### NonUploadingCaliperRunner\.run<!-- {{#callable:com.google.gson.metrics.NonUploadingCaliperRunner.run}} -->
The `run` method executes a Caliper benchmark for a given class with specified arguments, disabling result uploads by default.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `c`: The class object representing the benchmark to be run.
    - `args`: An array of strings representing additional arguments to be passed to the Caliper benchmark.
- **Control Flow**:
    - The method calls a private static method [`concat`](#NonUploadingCaliperRunnerconcat) to prepend the string '-Cresults.upload.options.url=' to the `args` array, effectively disabling result uploads.
    - The `CaliperMain.main` method is invoked with the class `c` and the modified arguments array, executing the benchmark.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.metrics.NonUploadingCaliperRunner.concat`](#NonUploadingCaliperRunnerconcat)
- **See also**: [`com.google.gson.metrics.NonUploadingCaliperRunner`](#NonUploadingCaliperRunner)  (Base Class)



