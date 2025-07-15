# Purpose
The provided Java source code defines the [`GsonBuilder`](#GsonBuilderGsonBuilder) class, which is part of the Google Gson library. This class is designed to facilitate the creation of a `Gson` instance with customized configuration options beyond the default settings. The [`GsonBuilder`](#GsonBuilderGsonBuilder) class follows the builder design pattern, allowing users to configure various serialization and deserialization behaviors by chaining method calls. Key functionalities include setting field naming policies, enabling complex map key serialization, configuring date formats, and applying exclusion strategies for fields and classes. The class also supports registering custom type adapters and type adapter factories, which are essential for handling specific serialization and deserialization logic for custom types.

The [`GsonBuilder`](#GsonBuilderGsonBuilder) class provides a broad range of configuration options, making it a versatile tool for developers who need to tailor JSON processing to specific requirements. It includes methods for handling versioning, serialization of nulls, and special floating-point values, as well as options to disable certain default behaviors like HTML escaping and the use of JDK's `Unsafe`. The class also supports the addition of reflection access filters, which control the use of reflection during serialization and deserialization. By calling the `create()` method, a fully configured `Gson` instance is generated, ready for use in JSON processing tasks. This class is a crucial component of the Gson library, providing a flexible and powerful interface for JSON serialization and deserialization customization.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.gson.Gson.DEFAULT_COMPLEX_MAP_KEYS`
- `com.google.gson.Gson.DEFAULT_DATE_PATTERN`
- `com.google.gson.Gson.DEFAULT_ESCAPE_HTML`
- `com.google.gson.Gson.DEFAULT_FORMATTING_STYLE`
- `com.google.gson.Gson.DEFAULT_JSON_NON_EXECUTABLE`
- `com.google.gson.Gson.DEFAULT_NUMBER_TO_NUMBER_STRATEGY`
- `com.google.gson.Gson.DEFAULT_OBJECT_TO_NUMBER_STRATEGY`
- `com.google.gson.Gson.DEFAULT_SERIALIZE_NULLS`
- `com.google.gson.Gson.DEFAULT_SPECIALIZE_FLOAT_VALUES`
- `com.google.gson.Gson.DEFAULT_STRICTNESS`
- `com.google.gson.Gson.DEFAULT_USE_JDK_UNSAFE`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.errorprone.annotations.InlineMe`
- `com.google.gson.annotations.Since`
- `com.google.gson.annotations.Until`
- `com.google.gson.internal.Excluder`
- `com.google.gson.internal.GsonPreconditions`
- `com.google.gson.internal.bind.DefaultDateTypeAdapter`
- `com.google.gson.internal.bind.TreeTypeAdapter`
- `com.google.gson.internal.bind.TypeAdapters`
- `com.google.gson.internal.sql.SqlTypesSupport`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.lang.reflect.Type`
- `java.text.DateFormat`
- `java.text.SimpleDateFormat`
- `java.util.ArrayDeque`
- `java.util.ArrayList`
- `java.util.Collections`
- `java.util.Date`
- `java.util.HashMap`
- `java.util.List`
- `java.util.Map`
- `java.util.Objects`


# Classes

---
### GsonBuilder<!-- {{#class:com.google.gson.GsonBuilder}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `GsonBuilder` class is a builder for creating `Gson` instances with custom configurations, allowing users to specify various serialization and deserialization options such as field naming policies, exclusion strategies, date formats, and more. It follows the builder pattern, enabling the chaining of configuration methods to set desired options before calling `create()` to produce a `Gson` instance. This class provides flexibility in handling JSON data by allowing customization of how objects are serialized and deserialized, including support for complex map keys, special floating point values, and reflection access filters.
- **Fields**:
    - `excluder`: `Excluder` An instance of `Excluder` used to determine which fields and classes should be excluded from serialization and deserialization.
    - `longSerializationPolicy`: `LongSerializationPolicy` Defines the serialization policy for `Long` and `long` objects.
    - `fieldNamingPolicy`: `FieldNamingStrategy` Specifies the naming strategy for fields during serialization and deserialization.
    - `instanceCreators`: `Map<Type, InstanceCreator<?>>` A map of `Type` to `InstanceCreator` for creating instances of specific types during deserialization.
    - `factories`: `List<TypeAdapterFactory>` A list of `TypeAdapterFactory` instances for creating type adapters.
    - `hierarchyFactories`: `List<TypeAdapterFactory>` A list of `TypeAdapterFactory` instances for creating type adapters for type hierarchies.
    - `serializeNulls`: `boolean` Indicates whether null fields should be serialized.
    - `datePattern`: `String` The pattern used for serializing and deserializing `Date` objects.
    - `dateStyle`: `int` The style used for serializing and deserializing `Date` objects, as defined by `DateFormat`.
    - `timeStyle`: `int` The style used for serializing and deserializing time portions of `Date` objects, as defined by `DateFormat`.
    - `complexMapKeySerialization`: `boolean` Indicates whether complex map keys should be serialized as JSON arrays.
    - `serializeSpecialFloatingPointValues`: `boolean` Indicates whether special floating point values (NaN, Infinity) should be serialized.
    - `escapeHtmlChars`: `boolean` Indicates whether HTML characters should be escaped during serialization.
    - `formattingStyle`: `FormattingStyle` Defines the formatting style for JSON output, such as pretty printing.
    - `generateNonExecutableJson`: `boolean` Indicates whether the JSON output should be prefixed to prevent execution in JavaScript.
    - `strictness`: `Strictness` Defines the strictness level for JSON parsing and writing.
    - `useJdkUnsafe`: `boolean` Indicates whether JDK's `Unsafe` should be used for creating instances of classes without no-args constructors.
    - `objectToNumberStrategy`: `ToNumberStrategy` Defines the strategy for converting objects to numbers during deserialization.
    - `numberToNumberStrategy`: `ToNumberStrategy` Defines the strategy for converting numbers to numbers during deserialization.
    - `reflectionFilters`: `ArrayDeque<ReflectionAccessFilter>` A deque of `ReflectionAccessFilter` instances to control reflection access during serialization and deserialization.
- **Methods**:
    - [`com.google.gson.GsonBuilder.GsonBuilder`](#GsonBuilderGsonBuilder)
    - [`com.google.gson.GsonBuilder.GsonBuilder`](#GsonBuilderGsonBuilder)
    - [`com.google.gson.GsonBuilder.setVersion`](#GsonBuildersetVersion)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.GsonBuilder.generateNonExecutableJson`](#GsonBuildergenerateNonExecutableJson)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithoutExposeAnnotation`](#GsonBuilderexcludeFieldsWithoutExposeAnnotation)
    - [`com.google.gson.GsonBuilder.serializeNulls`](#GsonBuilderserializeNulls)
    - [`com.google.gson.GsonBuilder.enableComplexMapKeySerialization`](#GsonBuilderenableComplexMapKeySerialization)
    - [`com.google.gson.GsonBuilder.disableInnerClassSerialization`](#GsonBuilderdisableInnerClassSerialization)
    - [`com.google.gson.GsonBuilder.setLongSerializationPolicy`](#GsonBuildersetLongSerializationPolicy)
    - [`com.google.gson.GsonBuilder.setFieldNamingPolicy`](#GsonBuildersetFieldNamingPolicy)
    - [`com.google.gson.GsonBuilder.setFieldNamingStrategy`](#GsonBuildersetFieldNamingStrategy)
    - [`com.google.gson.GsonBuilder.setObjectToNumberStrategy`](#GsonBuildersetObjectToNumberStrategy)
    - [`com.google.gson.GsonBuilder.setNumberToNumberStrategy`](#GsonBuildersetNumberToNumberStrategy)
    - [`com.google.gson.GsonBuilder.setExclusionStrategies`](#GsonBuildersetExclusionStrategies)
    - [`com.google.gson.GsonBuilder.addSerializationExclusionStrategy`](#GsonBuilderaddSerializationExclusionStrategy)
    - [`com.google.gson.GsonBuilder.addDeserializationExclusionStrategy`](#GsonBuilderaddDeserializationExclusionStrategy)
    - [`com.google.gson.GsonBuilder.setPrettyPrinting`](#GsonBuildersetPrettyPrinting)
    - [`com.google.gson.GsonBuilder.setFormattingStyle`](#GsonBuildersetFormattingStyle)
    - [`com.google.gson.GsonBuilder.setLenient`](#GsonBuildersetLenient)
    - [`com.google.gson.GsonBuilder.setStrictness`](#GsonBuildersetStrictness)
    - [`com.google.gson.GsonBuilder.disableHtmlEscaping`](#GsonBuilderdisableHtmlEscaping)
    - [`com.google.gson.GsonBuilder.setDateFormat`](#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.setDateFormat`](#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.setDateFormat`](#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.checkDateFormatStyle`](#GsonBuildercheckDateFormatStyle)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.hasNonOverridableAdapter`](#GsonBuilderhasNonOverridableAdapter)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.GsonBuilder.disableJdkUnsafe`](#GsonBuilderdisableJdkUnsafe)
    - [`com.google.gson.GsonBuilder.addReflectionAccessFilter`](#GsonBuilderaddReflectionAccessFilter)
    - [`com.google.gson.GsonBuilder.create`](#GsonBuildercreate)
    - [`com.google.gson.GsonBuilder.addTypeAdaptersForDate`](#GsonBuilderaddTypeAdaptersForDate)

**Methods**

---
#### GsonBuilder\.GsonBuilder<!-- {{#callable:com.google.gson.GsonBuilder.GsonBuilder}} -->
The `GsonBuilder` constructor initializes a new instance of the `GsonBuilder` class with default configuration settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is empty and does not perform any operations or initializations beyond the default object instantiation.
- **Output**:
    - A new instance of the `GsonBuilder` class is created.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.GsonBuilder<!-- {{#callable:com.google.gson.GsonBuilder.GsonBuilder}} -->
The `GsonBuilder` constructor initializes a new `GsonBuilder` instance by copying the configuration settings from an existing `Gson` instance.
- **Modifiers**: ``
- **Inputs**:
    - `gson`: The `Gson` instance from which configuration settings are copied to initialize the `GsonBuilder`.
- **Control Flow**:
    - Copy the `excluder` from the provided `Gson` instance to the `GsonBuilder` instance.
    - Copy the `fieldNamingStrategy` from the provided `Gson` instance to the `GsonBuilder` instance.
    - Copy all `instanceCreators` from the provided `Gson` instance to the `GsonBuilder` instance.
    - Set `serializeNulls` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `complexMapKeySerialization` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `generateNonExecutableJson` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `escapeHtmlChars` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `formattingStyle` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `strictness` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `serializeSpecialFloatingPointValues` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `longSerializationPolicy` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `datePattern` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `dateStyle` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `timeStyle` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Add all `builderFactories` from the provided `Gson` instance to the `factories` list in the `GsonBuilder`.
    - Add all `builderHierarchyFactories` from the provided `Gson` instance to the `hierarchyFactories` list in the `GsonBuilder`.
    - Set `useJdkUnsafe` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `objectToNumberStrategy` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Set `numberToNumberStrategy` in the `GsonBuilder` to the value from the provided `Gson` instance.
    - Add all `reflectionFilters` from the provided `Gson` instance to the `reflectionFilters` deque in the `GsonBuilder`.
- **Output**:
    - A new `GsonBuilder` instance initialized with the same configuration as the provided `Gson` instance.
- **Functions called**:
    - [`com.google.gson.JsonArray.addAll`](JsonArray.java.driver.md#JsonArrayaddAll)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setVersion<!-- {{#callable:com.google.gson.GsonBuilder.setVersion}} -->
The `setVersion` method configures the GsonBuilder to support versioning by setting a specific version number, which is used to include or exclude fields and classes based on the `Since` and `Until` annotations.
- **Modifiers**: `public`
- **Inputs**:
    - `version`: A double representing the version number to be set for versioning support.
- **Control Flow**:
    - Check if the provided version is NaN or negative; if so, throw an IllegalArgumentException with a message indicating the invalid version.
    - If the version is valid, update the `excluder` field by calling its [`withVersion`](internal/Excluder.java.driver.md#ExcluderwithVersion) method with the provided version.
    - Return the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.withVersion`](internal/Excluder.java.driver.md#ExcluderwithVersion)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.excludeFieldsWithModifiers<!-- {{#callable:com.google.gson.GsonBuilder.excludeFieldsWithModifiers}} -->
The `excludeFieldsWithModifiers` method configures the GsonBuilder to exclude fields with specified Java modifiers from serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**:
    - `modifiers`: An array of integers representing the field modifiers to exclude, typically constants from the `java.lang.reflect.Modifier` class, such as `Modifier.TRANSIENT` or `Modifier.STATIC`.
- **Control Flow**:
    - The method first checks that the `modifiers` array is not null using `Objects.requireNonNull(modifiers)`.
    - It then updates the `excluder` field by calling `excluder.withModifiers(modifiers)`, which configures the excluder to exclude fields with the specified modifiers.
    - Finally, the method returns the current instance of `GsonBuilder` to allow for method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.withModifiers`](internal/Excluder.java.driver.md#ExcluderwithModifiers)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.generateNonExecutableJson<!-- {{#callable:com.google.gson.GsonBuilder.generateNonExecutableJson}} -->
The `generateNonExecutableJson` method sets a flag to make the JSON output non-executable in JavaScript and returns the current `GsonBuilder` instance.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `generateNonExecutableJson` field to `true` to indicate that the JSON output should be non-executable.
    - Returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.excludeFieldsWithoutExposeAnnotation<!-- {{#callable:com.google.gson.GsonBuilder.excludeFieldsWithoutExposeAnnotation}} -->
The [`excludeFieldsWithoutExposeAnnotation`](internal/Excluder.java.driver.md#ExcluderexcludeFieldsWithoutExposeAnnotation) method configures the GsonBuilder to exclude fields that do not have the `@Expose` annotation during serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`excludeFieldsWithoutExposeAnnotation`](internal/Excluder.java.driver.md#ExcluderexcludeFieldsWithoutExposeAnnotation) on the `excluder` object, which updates the excluder's configuration to exclude fields without the `@Expose` annotation.
    - The method returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance with updated exclusion settings.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.excludeFieldsWithoutExposeAnnotation`](internal/Excluder.java.driver.md#ExcluderexcludeFieldsWithoutExposeAnnotation)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.serializeNulls<!-- {{#callable:com.google.gson.GsonBuilder.serializeNulls}} -->
The `serializeNulls` method configures the GsonBuilder to include null fields during serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `serializeNulls` field of the `GsonBuilder` instance to `true`.
    - Returns the current `GsonBuilder` instance.
- **Output**:
    - Returns the current `GsonBuilder` instance with the `serializeNulls` configuration set to true.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.enableComplexMapKeySerialization<!-- {{#callable:com.google.gson.GsonBuilder.enableComplexMapKeySerialization}} -->
The `enableComplexMapKeySerialization` method configures the `GsonBuilder` to serialize `Map` objects with complex keys as JSON arrays.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `complexMapKeySerialization` field to `true`.
    - Returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance with complex map key serialization enabled.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.disableInnerClassSerialization<!-- {{#callable:com.google.gson.GsonBuilder.disableInnerClassSerialization}} -->
The [`disableInnerClassSerialization`](internal/Excluder.java.driver.md#ExcluderdisableInnerClassSerialization) method configures the GsonBuilder to exclude inner classes from serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`disableInnerClassSerialization`](internal/Excluder.java.driver.md#ExcluderdisableInnerClassSerialization) on the `excluder` object, which modifies the excluder's behavior to exclude inner classes.
    - The method returns the current instance of `GsonBuilder`, allowing for method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance with updated configuration to exclude inner classes.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.disableInnerClassSerialization`](internal/Excluder.java.driver.md#ExcluderdisableInnerClassSerialization)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setLongSerializationPolicy<!-- {{#callable:com.google.gson.GsonBuilder.setLongSerializationPolicy}} -->
The `setLongSerializationPolicy` method sets the serialization policy for `Long` and `long` objects in the `GsonBuilder` and returns the builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `serializationPolicy`: The `LongSerializationPolicy` to be used for serializing `Long` and `long` objects.
- **Control Flow**:
    - The method assigns the provided `serializationPolicy` to the `longSerializationPolicy` field of the `GsonBuilder` instance after ensuring it is not null using `Objects.requireNonNull`.
    - The method then returns the current instance of `GsonBuilder` to allow for method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setFieldNamingPolicy<!-- {{#callable:com.google.gson.GsonBuilder.setFieldNamingPolicy}} -->
The `setFieldNamingPolicy` method configures the GsonBuilder to use a specific field naming policy for serialization and deserialization by delegating to the [`setFieldNamingStrategy`](#GsonBuildersetFieldNamingStrategy) method.
- **Modifiers**: `public`
- **Inputs**:
    - `namingConvention`: An instance of FieldNamingPolicy that specifies the naming convention to be applied to fields during serialization and deserialization.
- **Control Flow**:
    - The method takes a FieldNamingPolicy object as an argument.
    - It calls the [`setFieldNamingStrategy`](#GsonBuildersetFieldNamingStrategy) method with the provided namingConvention argument.
    - The method returns the current instance of GsonBuilder.
- **Output**:
    - Returns the current instance of GsonBuilder, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setFieldNamingStrategy`](#GsonBuildersetFieldNamingStrategy)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setFieldNamingStrategy<!-- {{#callable:com.google.gson.GsonBuilder.setFieldNamingStrategy}} -->
The `setFieldNamingStrategy` method sets a custom field naming strategy for a `GsonBuilder` instance and returns the builder itself.
- **Modifiers**: `public`
- **Inputs**:
    - `fieldNamingStrategy`: An instance of `FieldNamingStrategy` that defines the naming strategy to be applied to fields during serialization and deserialization.
- **Control Flow**:
    - The method assigns the provided `fieldNamingStrategy` to the `fieldNamingPolicy` attribute of the `GsonBuilder` instance after ensuring it is not null using `Objects.requireNonNull`.
    - The method then returns the current `GsonBuilder` instance (`this`) to allow for method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setObjectToNumberStrategy<!-- {{#callable:com.google.gson.GsonBuilder.setObjectToNumberStrategy}} -->
The `setObjectToNumberStrategy` method sets a custom strategy for converting objects to numbers during deserialization in a `GsonBuilder` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `objectToNumberStrategy`: An instance of `ToNumberStrategy` that defines how objects should be converted to numbers during deserialization.
- **Control Flow**:
    - The method first checks that the `objectToNumberStrategy` parameter is not null using `Objects.requireNonNull`.
    - It assigns the `objectToNumberStrategy` to the instance variable `this.objectToNumberStrategy`.
    - The method returns the current `GsonBuilder` instance (`this`) to allow for method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setNumberToNumberStrategy<!-- {{#callable:com.google.gson.GsonBuilder.setNumberToNumberStrategy}} -->
The `setNumberToNumberStrategy` method sets a custom strategy for deserializing `Number` types and returns the `GsonBuilder` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `numberToNumberStrategy`: A `ToNumberStrategy` object that defines the strategy for deserializing `Number` types.
- **Control Flow**:
    - The method assigns the provided `numberToNumberStrategy` to the `numberToNumberStrategy` field of the `GsonBuilder` instance after ensuring it is not null using `Objects.requireNonNull`.
    - The method returns the current `GsonBuilder` instance to allow for method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setExclusionStrategies<!-- {{#callable:com.google.gson.GsonBuilder.setExclusionStrategies}} -->
The `setExclusionStrategies` method configures the GsonBuilder to apply a set of exclusion strategies during both serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**:
    - `strategies`: A varargs parameter of ExclusionStrategy objects to be applied during object serialization and deserialization.
- **Control Flow**:
    - The method first checks that the `strategies` parameter is not null using `Objects.requireNonNull` to prevent null pointer exceptions.
    - It iterates over each `ExclusionStrategy` in the `strategies` array.
    - For each strategy, it updates the `excluder` field by calling [`withExclusionStrategy`](internal/Excluder.java.driver.md#ExcluderwithExclusionStrategy) on it, passing the strategy and two boolean values `true` and `true`, indicating that the strategy should be applied to both serialization and deserialization.
    - Finally, the method returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.withExclusionStrategy`](internal/Excluder.java.driver.md#ExcluderwithExclusionStrategy)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.addSerializationExclusionStrategy<!-- {{#callable:com.google.gson.GsonBuilder.addSerializationExclusionStrategy}} -->
The `addSerializationExclusionStrategy` method adds a specified exclusion strategy to the GsonBuilder for serialization purposes.
- **Modifiers**: `public`
- **Inputs**:
    - `strategy`: An `ExclusionStrategy` object that defines the criteria for excluding fields or classes during serialization.
- **Control Flow**:
    - The method first checks if the `strategy` parameter is not null using `Objects.requireNonNull(strategy)`.
    - It then updates the `excluder` field by calling `excluder.withExclusionStrategy(strategy, true, false)`, which adds the given strategy for serialization but not for deserialization.
    - Finally, the method returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.withExclusionStrategy`](internal/Excluder.java.driver.md#ExcluderwithExclusionStrategy)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.addDeserializationExclusionStrategy<!-- {{#callable:com.google.gson.GsonBuilder.addDeserializationExclusionStrategy}} -->
The `addDeserializationExclusionStrategy` method adds an exclusion strategy to the GsonBuilder that will be applied during deserialization.
- **Modifiers**: `public`
- **Inputs**:
    - `strategy`: An ExclusionStrategy object that defines the criteria for excluding fields or classes during deserialization.
- **Control Flow**:
    - The method first checks that the provided strategy is not null using `Objects.requireNonNull(strategy)`.
    - It then updates the `excluder` field by calling `excluder.withExclusionStrategy(strategy, false, true)`, which adds the strategy for deserialization only.
    - Finally, it returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.withExclusionStrategy`](internal/Excluder.java.driver.md#ExcluderwithExclusionStrategy)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setPrettyPrinting<!-- {{#callable:com.google.gson.GsonBuilder.setPrettyPrinting}} -->
The `setPrettyPrinting` method configures the GsonBuilder to output JSON in a pretty-printed format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`setFormattingStyle`](#GsonBuildersetFormattingStyle) with `FormattingStyle.PRETTY` as the argument.
    - The [`setFormattingStyle`](#GsonBuildersetFormattingStyle) method sets the `formattingStyle` field of the `GsonBuilder` to `FormattingStyle.PRETTY`.
    - The method returns the current instance of `GsonBuilder`.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setFormattingStyle`](#GsonBuildersetFormattingStyle)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setFormattingStyle<!-- {{#callable:com.google.gson.GsonBuilder.setFormattingStyle}} -->
The `setFormattingStyle` method sets the formatting style for JSON output in the `GsonBuilder` and returns the builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `formattingStyle`: An instance of `FormattingStyle` that specifies the desired formatting style for JSON output.
- **Control Flow**:
    - The method assigns the provided `formattingStyle` to the `formattingStyle` field of the `GsonBuilder` instance after ensuring it is not null using `Objects.requireNonNull`.
    - The method then returns the current instance of `GsonBuilder` to allow for method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setLenient<!-- {{#callable:com.google.gson.GsonBuilder.setLenient}} -->
The `setLenient` method sets the strictness of the `GsonBuilder` to `Strictness.LENIENT`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with `@Deprecated`, indicating it is outdated and should not be used in new code.
    - The method is also annotated with `@InlineMe`, suggesting a replacement method call `this.setStrictness(Strictness.LENIENT)` for future use.
    - The method calls `setStrictness(Strictness.LENIENT)` internally to set the strictness level to lenient.
    - The method returns the current `GsonBuilder` instance after setting the strictness.
- **Output**:
    - Returns the current `GsonBuilder` instance with lenient strictness set.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setStrictness`](#GsonBuildersetStrictness)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setStrictness<!-- {{#callable:com.google.gson.GsonBuilder.setStrictness}} -->
The `setStrictness` method sets the strictness level for the GsonBuilder and returns the builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `strictness`: An instance of the Strictness enum that specifies the desired strictness level for JSON parsing and writing.
- **Control Flow**:
    - The method assigns the provided `strictness` value to the `strictness` field of the GsonBuilder instance after ensuring it is not null using `Objects.requireNonNull(strictness)`.
    - The method then returns the current instance of GsonBuilder (`this`) to allow for method chaining.
- **Output**:
    - The method returns the current instance of GsonBuilder, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.disableHtmlEscaping<!-- {{#callable:com.google.gson.GsonBuilder.disableHtmlEscaping}} -->
The `disableHtmlEscaping` method configures the GsonBuilder to not escape HTML characters in the JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `escapeHtmlChars` field to `false`, indicating that HTML characters should not be escaped.
    - Returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance with HTML escaping disabled.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setDateFormat<!-- {{#callable:com.google.gson.GsonBuilder.setDateFormat}} -->
The `setDateFormat` method configures the `GsonBuilder` to serialize and deserialize `Date` objects using a specified date pattern.
- **Modifiers**: `public`
- **Inputs**:
    - `pattern`: A `String` representing the date pattern to be used for serialization and deserialization; can be `null` to reset the pattern.
- **Control Flow**:
    - Check if the `pattern` is not `null`.
    - Attempt to create a `SimpleDateFormat` object with the given `pattern` to validate it.
    - Catch `IllegalArgumentException` if the `pattern` is invalid and throw a new `IllegalArgumentException` with a descriptive message.
    - Set the `datePattern` field of the `GsonBuilder` to the provided `pattern`.
    - Return the current `GsonBuilder` instance.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setDateFormat<!-- {{#callable:com.google.gson.GsonBuilder.setDateFormat}} -->
The `setDateFormat` method sets the date style for date serialization and deserialization in the `GsonBuilder` and returns the builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `dateStyle`: An integer representing the predefined date style constant from the `DateFormat` class, such as `DateFormat.MEDIUM`.
- **Control Flow**:
    - The method assigns the validated `dateStyle` to the `dateStyle` field of the `GsonBuilder` instance.
    - It sets the `datePattern` field to `null` to indicate that a date style, rather than a pattern, is being used.
    - The method returns the current instance of `GsonBuilder` to allow for method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.checkDateFormatStyle`](#GsonBuildercheckDateFormatStyle)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.setDateFormat<!-- {{#callable:com.google.gson.GsonBuilder.setDateFormat}} -->
The `setDateFormat` method configures the `GsonBuilder` to serialize `Date` objects according to specified date and time styles.
- **Modifiers**: `public`
- **Inputs**:
    - `dateStyle`: An integer representing the predefined date style constant from the `DateFormat` class.
    - `timeStyle`: An integer representing the predefined time style constant from the `DateFormat` class.
- **Control Flow**:
    - The method assigns the result of `checkDateFormatStyle(dateStyle)` to the `dateStyle` field.
    - The method assigns the result of `checkDateFormatStyle(timeStyle)` to the `timeStyle` field.
    - The `datePattern` field is set to `null`.
    - The method returns the current instance of `GsonBuilder`.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.checkDateFormatStyle`](#GsonBuildercheckDateFormatStyle)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.checkDateFormatStyle<!-- {{#callable:com.google.gson.GsonBuilder.checkDateFormatStyle}} -->
The `checkDateFormatStyle` method validates that a given date format style integer is within the acceptable range of 0 to 3, throwing an exception if it is not.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `style`: An integer representing the date format style to be validated.
- **Control Flow**:
    - Check if the input `style` is less than 0 or greater than 3.
    - If the condition is true, throw an `IllegalArgumentException` with a message indicating the invalid style.
    - If the condition is false, return the input `style`.
- **Output**:
    - Returns the validated date format style integer if it is within the valid range.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.registerTypeAdapter<!-- {{#callable:com.google.gson.GsonBuilder.registerTypeAdapter}} -->
The `registerTypeAdapter` method registers a custom type adapter for a specified type in the GsonBuilder, allowing for custom serialization and deserialization logic.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: The `Type` object representing the data type for which the type adapter is being registered.
    - `typeAdapter`: An object that must implement at least one of the interfaces: `JsonSerializer`, `JsonDeserializer`, `InstanceCreator`, or `TypeAdapter`, which defines custom serialization/deserialization logic for the specified type.
- **Control Flow**:
    - Check if the `type` is non-null using `Objects.requireNonNull` to ensure it is not null.
    - Verify that the `typeAdapter` is an instance of one of the required interfaces (`JsonSerializer`, `JsonDeserializer`, `InstanceCreator`, or `TypeAdapter`) using `GsonPreconditions.checkArgument`.
    - Check if the type has a non-overridable built-in adapter using [`hasNonOverridableAdapter`](#GsonBuilderhasNonOverridableAdapter); if so, throw an `IllegalArgumentException`.
    - If the `typeAdapter` is an instance of `InstanceCreator`, add it to the `instanceCreators` map with the `type` as the key.
    - If the `typeAdapter` is an instance of `JsonSerializer` or `JsonDeserializer`, create a `TypeToken` for the `type` and add a new factory to the `factories` list using `TreeTypeAdapter.newFactoryWithMatchRawType`.
    - If the `typeAdapter` is an instance of `TypeAdapter`, create a `TypeAdapterFactory` using `TypeAdapters.newFactory` and add it to the `factories` list.
    - Return the current `GsonBuilder` instance to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](internal/GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.GsonBuilder.hasNonOverridableAdapter`](#GsonBuilderhasNonOverridableAdapter)
    - [`com.google.gson.reflect.TypeToken.get`](reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.internal.bind.TreeTypeAdapter.newFactoryWithMatchRawType`](internal/bind/TreeTypeAdapter.java.driver.md#TreeTypeAdapternewFactoryWithMatchRawType)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactory`](internal/bind/TypeAdapters.java.driver.md#TypeAdaptersnewFactory)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.hasNonOverridableAdapter<!-- {{#callable:com.google.gson.GsonBuilder.hasNonOverridableAdapter}} -->
The `hasNonOverridableAdapter` method checks if a given `Type` is `Object.class`, indicating it has a non-overridable adapter.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `type`: The `Type` object to be checked for a non-overridable adapter.
- **Control Flow**:
    - The method compares the input `type` with `Object.class`.
    - If `type` is `Object.class`, it returns `true`.
    - Otherwise, it returns `false`.
- **Output**:
    - A boolean value indicating whether the `Type` has a non-overridable adapter (true if it is `Object.class`, false otherwise).
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.registerTypeAdapterFactory<!-- {{#callable:com.google.gson.GsonBuilder.registerTypeAdapterFactory}} -->
The `registerTypeAdapterFactory` method registers a `TypeAdapterFactory` with the `GsonBuilder` and returns the builder instance for method chaining.
- **Modifiers**: `public`
- **Inputs**:
    - `factory`: A `TypeAdapterFactory` instance to be registered with the `GsonBuilder`.
- **Control Flow**:
    - The method first checks if the `factory` argument is non-null using `Objects.requireNonNull(factory)`.
    - It then adds the `factory` to the `factories` list of the `GsonBuilder` instance.
    - Finally, it returns the current `GsonBuilder` instance (`this`) to allow for method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.registerTypeHierarchyAdapter<!-- {{#callable:com.google.gson.GsonBuilder.registerTypeHierarchyAdapter}} -->
The `registerTypeHierarchyAdapter` method registers a type adapter for a specified base class or interface and its subclasses, allowing for custom serialization or deserialization in Gson.
- **Modifiers**: `public`
- **Inputs**:
    - `baseType`: The class or interface for which the type adapter is being registered, including its subclasses.
    - `typeAdapter`: An object that must implement at least one of the interfaces: TypeAdapter, JsonSerializer, or JsonDeserializer.
- **Control Flow**:
    - The method first checks that the `baseType` is not null.
    - It then verifies that the `typeAdapter` is an instance of either JsonSerializer, JsonDeserializer, or TypeAdapter.
    - If the `typeAdapter` is an instance of JsonSerializer or JsonDeserializer, it adds a new type hierarchy factory to `hierarchyFactories`.
    - If the `typeAdapter` is an instance of TypeAdapter, it creates a new type hierarchy factory and adds it to `factories`.
    - Finally, the method returns the current instance of `GsonBuilder`.
- **Output**:
    - Returns the current `GsonBuilder` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](internal/GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.internal.bind.TreeTypeAdapter.newTypeHierarchyFactory`](internal/bind/TreeTypeAdapter.java.driver.md#TreeTypeAdapternewTypeHierarchyFactory)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.serializeSpecialFloatingPointValues<!-- {{#callable:com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues}} -->
The `serializeSpecialFloatingPointValues` method configures the GsonBuilder to serialize special floating point values like NaN and Infinity.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `serializeSpecialFloatingPointValues` field of the `GsonBuilder` instance to `true`.
    - Returns the current `GsonBuilder` instance.
- **Output**:
    - Returns the current `GsonBuilder` instance with the `serializeSpecialFloatingPointValues` field set to `true`.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.disableJdkUnsafe<!-- {{#callable:com.google.gson.GsonBuilder.disableJdkUnsafe}} -->
The `disableJdkUnsafe` method disables the use of JDK's `sun.misc.Unsafe` for object instantiation in GsonBuilder.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `useJdkUnsafe` field to `false`, indicating that JDK's `sun.misc.Unsafe` should not be used.
    - Returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - Returns the current `GsonBuilder` instance with `useJdkUnsafe` set to `false`.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.addReflectionAccessFilter<!-- {{#callable:com.google.gson.GsonBuilder.addReflectionAccessFilter}} -->
The `addReflectionAccessFilter` method adds a `ReflectionAccessFilter` to the beginning of the `reflectionFilters` deque in the `GsonBuilder` class.
- **Modifiers**: `public`
- **Inputs**:
    - `filter`: A `ReflectionAccessFilter` object that specifies which classes should be restricted from reflection access during serialization and deserialization.
- **Control Flow**:
    - The method first checks if the `filter` argument is non-null using `Objects.requireNonNull(filter);`.
    - It then adds the `filter` to the front of the `reflectionFilters` deque using `reflectionFilters.addFirst(filter);`.
    - Finally, it returns the current instance of `GsonBuilder` to allow method chaining.
- **Output**:
    - The method returns the current `GsonBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.create<!-- {{#callable:com.google.gson.GsonBuilder.create}} -->
The `create` method constructs and returns a new `Gson` instance based on the current configuration of the `GsonBuilder`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a new list `factories` with a size accommodating existing `factories` and `hierarchyFactories` plus three additional slots.
    - Add all elements from `this.factories` to `factories` and reverse the order of `factories`.
    - Create a new list `hierarchyFactories` from `this.hierarchyFactories` and reverse its order.
    - Add all elements from `hierarchyFactories` to `factories`.
    - Invoke [`addTypeAdaptersForDate`](#GsonBuilderaddTypeAdaptersForDate) with `datePattern`, `dateStyle`, `timeStyle`, and `factories` to add date type adapters.
    - Return a new `Gson` instance initialized with various configuration parameters and the `factories` list.
- **Output**:
    - A new `Gson` instance configured with the options set in the `GsonBuilder`.
- **Functions called**:
    - [`com.google.gson.JsonArray.addAll`](JsonArray.java.driver.md#JsonArrayaddAll)
    - [`com.google.gson.GsonBuilder.addTypeAdaptersForDate`](#GsonBuilderaddTypeAdaptersForDate)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)


---
#### GsonBuilder\.addTypeAdaptersForDate<!-- {{#callable:com.google.gson.GsonBuilder.addTypeAdaptersForDate}} -->
The `addTypeAdaptersForDate` method adds date-related type adapter factories to a list based on the provided date pattern or style.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `datePattern`: A string representing the date pattern to be used for creating date type adapters.
    - `dateStyle`: An integer representing the date style, used if the date pattern is not provided.
    - `timeStyle`: An integer representing the time style, used if the date pattern is not provided.
    - `factories`: A list of `TypeAdapterFactory` objects to which the date-related type adapters will be added.
- **Control Flow**:
    - Check if `datePattern` is not null and not empty after trimming.
    - If `datePattern` is valid, create a `dateAdapterFactory` using the date pattern.
    - Check if SQL types are supported, and if so, create `sqlTimestampAdapterFactory` and `sqlDateAdapterFactory` using the date pattern.
    - If `datePattern` is not valid, check if `dateStyle` or `timeStyle` is different from `DateFormat.DEFAULT`.
    - If styles are valid, create a `dateAdapterFactory` using the date and time styles.
    - Check if SQL types are supported, and if so, create `sqlTimestampAdapterFactory` and `sqlDateAdapterFactory` using the date and time styles.
    - If neither `datePattern` nor styles are valid, return without adding any adapters.
    - Add the `dateAdapterFactory` to the `factories` list.
    - If SQL types are supported, add `sqlTimestampAdapterFactory` and `sqlDateAdapterFactory` to the `factories` list.
- **Output**:
    - The method does not return a value; it modifies the `factories` list by adding appropriate type adapter factories.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
- **See also**: [`com.google.gson.GsonBuilder`](#GsonBuilder)  (Base Class)



