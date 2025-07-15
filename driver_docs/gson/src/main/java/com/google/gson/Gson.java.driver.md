# Purpose
The provided Java source code defines the [`Gson`](#GsonGson) class, which is the core component of the Gson library, a popular Java library developed by Google for converting Java objects to JSON and vice versa. The [`Gson`](#GsonGson) class offers a broad range of functionality for JSON serialization and deserialization, making it a versatile tool for handling JSON data in Java applications. It provides methods to serialize Java objects into JSON strings or JSON trees (`JsonElement`), and to deserialize JSON strings or trees back into Java objects. The class supports both simple and complex data types, including generic types, through the use of `TypeToken` to preserve type information during serialization and deserialization.

The [`Gson`](#GsonGson) class is designed to be thread-safe, allowing instances to be reused across multiple threads. It includes a variety of configuration options that can be set using the `GsonBuilder` class, such as pretty printing, custom serializers and deserializers, and strictness settings for JSON parsing. The class also supports advanced features like handling of complex map keys, HTML-safe JSON output, and serialization of special floating-point values. The [`Gson`](#GsonGson) class is a comprehensive solution for JSON processing in Java, providing a flexible and efficient API for developers to work with JSON data.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.internal.ConstructorConstructor`
- `com.google.gson.internal.Excluder`
- `com.google.gson.internal.GsonBuildConfig`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.internal.Primitives`
- `com.google.gson.internal.Streams`
- `com.google.gson.internal.bind.ArrayTypeAdapter`
- `com.google.gson.internal.bind.CollectionTypeAdapterFactory`
- `com.google.gson.internal.bind.DefaultDateTypeAdapter`
- `com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory`
- `com.google.gson.internal.bind.JsonTreeReader`
- `com.google.gson.internal.bind.JsonTreeWriter`
- `com.google.gson.internal.bind.MapTypeAdapterFactory`
- `com.google.gson.internal.bind.NumberTypeAdapter`
- `com.google.gson.internal.bind.ObjectTypeAdapter`
- `com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`
- `com.google.gson.internal.bind.SerializationDelegatingTypeAdapter`
- `com.google.gson.internal.bind.TypeAdapters`
- `com.google.gson.internal.sql.SqlTypesSupport`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.EOFException`
- `java.io.IOException`
- `java.io.Reader`
- `java.io.StringReader`
- `java.io.Writer`
- `java.lang.reflect.Type`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.text.DateFormat`
- `java.util.ArrayList`
- `java.util.Collections`
- `java.util.HashMap`
- `java.util.List`
- `java.util.Map`
- `java.util.Objects`
- `java.util.concurrent.ConcurrentHashMap`
- `java.util.concurrent.ConcurrentMap`
- `java.util.concurrent.atomic.AtomicLong`
- `java.util.concurrent.atomic.AtomicLongArray`


# Classes

---
### Gson<!-- {{#class:com.google.gson.Gson}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `Gson` class is the main entry point for using the Gson library, which provides a powerful and flexible way to convert Java objects to JSON and vice versa. It supports serialization and deserialization of complex data structures, including generic types, and offers various configuration options through the `GsonBuilder` class. The class is designed to be thread-safe, allowing instances to be reused across multiple threads. It includes a variety of default settings and type adapters for common Java types, and allows for customization through user-defined type adapters and factories.
- **Fields**:
    - `DEFAULT_JSON_NON_EXECUTABLE`: `boolean` Indicates whether JSON output should be non-executable by default.
    - `DEFAULT_STRICTNESS`: `Strictness` Defines the default strictness level for JSON parsing and writing.
    - `DEFAULT_FORMATTING_STYLE`: `FormattingStyle` Specifies the default formatting style for JSON output.
    - `DEFAULT_ESCAPE_HTML`: `boolean` Determines if HTML characters should be escaped in JSON output by default.
    - `DEFAULT_SERIALIZE_NULLS`: `boolean` Indicates if null values should be serialized in JSON output by default.
    - `DEFAULT_COMPLEX_MAP_KEYS`: `boolean` Specifies if complex map keys should be serialized in JSON by default.
    - `DEFAULT_SPECIALIZE_FLOAT_VALUES`: `boolean` Indicates if special floating point values should be serialized by default.
    - `DEFAULT_USE_JDK_UNSAFE`: `boolean` Determines if JDK's Unsafe should be used by default for object creation.
    - `DEFAULT_DATE_PATTERN`: `String` Specifies the default date pattern for JSON serialization.
    - `DEFAULT_FIELD_NAMING_STRATEGY`: `FieldNamingStrategy` Defines the default field naming strategy for JSON serialization.
    - `DEFAULT_OBJECT_TO_NUMBER_STRATEGY`: `ToNumberStrategy` Specifies the default strategy for converting objects to numbers in JSON.
    - `DEFAULT_NUMBER_TO_NUMBER_STRATEGY`: `ToNumberStrategy` Defines the default strategy for converting numbers to numbers in JSON.
    - `JSON_NON_EXECUTABLE_PREFIX`: `String` A prefix added to JSON output to make it non-executable in JavaScript.
    - `threadLocalAdapterResults`: `ThreadLocal<Map<TypeToken<?>, TypeAdapter<?>>>` A thread-local map to store type adapters during recursive adapter creation.
    - `typeTokenCache`: `ConcurrentMap<TypeToken<?>, TypeAdapter<?>>` A concurrent map caching type adapters for specific type tokens.
    - `constructorConstructor`: `ConstructorConstructor` Handles the creation of instances for types during deserialization.
    - `jsonAdapterFactory`: `JsonAdapterAnnotationTypeAdapterFactory` A factory for creating type adapters based on `@JsonAdapter` annotations.
    - `factories`: `List<TypeAdapterFactory>` A list of type adapter factories used by this Gson instance.
    - `excluder`: `Excluder` An excluder that determines which fields and classes are excluded from JSON serialization and deserialization.
    - `fieldNamingStrategy`: `FieldNamingStrategy` The strategy used for naming fields in JSON output.
    - `instanceCreators`: `Map<Type, InstanceCreator<?>>` A map of instance creators for specific types used during deserialization.
    - `serializeNulls`: `boolean` Indicates if null values should be serialized in JSON output.
    - `complexMapKeySerialization`: `boolean` Determines if complex map keys should be serialized in JSON.
    - `generateNonExecutableJson`: `boolean` Indicates if JSON output should be non-executable.
    - `htmlSafe`: `boolean` Specifies if JSON output should be HTML-safe, escaping HTML characters.
    - `formattingStyle`: `FormattingStyle` The formatting style used for JSON output.
    - `strictness`: `Strictness` The strictness level for JSON parsing and writing.
    - `serializeSpecialFloatingPointValues`: `boolean` Indicates if special floating point values should be serialized.
    - `useJdkUnsafe`: `boolean` Determines if JDK's Unsafe should be used for object creation.
    - `datePattern`: `String` The date pattern used for JSON serialization.
    - `dateStyle`: `int` The style used for formatting dates in JSON output.
    - `timeStyle`: `int` The style used for formatting times in JSON output.
    - `longSerializationPolicy`: `LongSerializationPolicy` The policy for serializing long values in JSON.
    - `builderFactories`: `List<TypeAdapterFactory>` A list of type adapter factories added by the builder.
    - `builderHierarchyFactories`: `List<TypeAdapterFactory>` A list of hierarchy type adapter factories added by the builder.
    - `objectToNumberStrategy`: `ToNumberStrategy` The strategy for converting objects to numbers in JSON.
    - `numberToNumberStrategy`: `ToNumberStrategy` The strategy for converting numbers to numbers in JSON.
    - `reflectionFilters`: `List<ReflectionAccessFilter>` A list of reflection access filters used by this Gson instance.
- **Methods**:
    - [`com.google.gson.Gson.Gson`](#GsonGson)
    - [`com.google.gson.Gson.Gson`](#GsonGson)
    - [`com.google.gson.Gson.newBuilder`](#GsonnewBuilder)
    - [`com.google.gson.Gson.excluder`](#Gsonexcluder)
    - [`com.google.gson.Gson.fieldNamingStrategy`](#GsonfieldNamingStrategy)
    - [`com.google.gson.Gson.serializeNulls`](#GsonserializeNulls)
    - [`com.google.gson.Gson.htmlSafe`](#GsonhtmlSafe)
    - [`com.google.gson.Gson.doubleAdapter`](#GsondoubleAdapter)
    - [`com.google.gson.Gson.floatAdapter`](#GsonfloatAdapter)
    - [`com.google.gson.Gson.checkValidFloatingPoint`](#GsoncheckValidFloatingPoint)
    - [`com.google.gson.Gson.longAdapter`](#GsonlongAdapter)
    - [`com.google.gson.Gson.atomicLongAdapter`](#GsonatomicLongAdapter)
    - [`com.google.gson.Gson.atomicLongArrayAdapter`](#GsonatomicLongArrayAdapter)
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
    - [`com.google.gson.Gson.getDelegateAdapter`](#GsongetDelegateAdapter)
    - [`com.google.gson.Gson.toJsonTree`](#GsontoJsonTree)
    - [`com.google.gson.Gson.toJsonTree`](#GsontoJsonTree)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.toJson`](#GsontoJson)
    - [`com.google.gson.Gson.newJsonWriter`](#GsonnewJsonWriter)
    - [`com.google.gson.Gson.newJsonReader`](#GsonnewJsonReader)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.fromJson`](#GsonfromJson)
    - [`com.google.gson.Gson.assertFullConsumption`](#GsonassertFullConsumption)
    - [`com.google.gson.Gson.toString`](#GsontoString)

**Methods**

---
#### Gson\.Gson<!-- {{#callable:com.google.gson.Gson.Gson}} -->
The `Gson` constructor initializes a `Gson` object with default configuration settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls another constructor of the `Gson` class with a set of default parameters.
    - These parameters include default settings for exclusion strategies, field naming strategies, serialization policies, and other configuration options.
    - The constructor initializes the `Gson` object with these default settings, allowing it to be used for JSON serialization and deserialization with standard behavior.
- **Output**:
    - A new `Gson` object is created with default settings.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.Gson<!-- {{#callable:com.google.gson.Gson.Gson}} -->
The `Gson` constructor initializes a Gson instance with various configuration options and sets up a list of type adapter factories for JSON serialization and deserialization.
- **Modifiers**: ``
- **Inputs**:
    - `excluder`: An `Excluder` object that determines which fields and classes are excluded from serialization and deserialization.
    - `fieldNamingStrategy`: A `FieldNamingStrategy` that defines the naming policy for fields during serialization and deserialization.
    - `instanceCreators`: A map of `Type` to `InstanceCreator` objects that provide custom instances for specific types during deserialization.
    - `serializeNulls`: A boolean indicating whether null values should be serialized.
    - `complexMapKeySerialization`: A boolean indicating whether complex map keys should be serialized as JSON objects.
    - `generateNonExecutableGson`: A boolean indicating whether to generate non-executable JSON by prefixing it with a special string.
    - `htmlSafe`: A boolean indicating whether the JSON output should be HTML-safe by escaping HTML characters.
    - `formattingStyle`: A `FormattingStyle` that defines the formatting style for the JSON output.
    - `strictness`: A `Strictness` level that defines how strictly the JSON should adhere to the JSON specification.
    - `serializeSpecialFloatingPointValues`: A boolean indicating whether special floating point values (NaN, Infinity) should be serialized.
    - `useJdkUnsafe`: A boolean indicating whether to use JDK's `Unsafe` for instance creation.
    - `longSerializationPolicy`: A `LongSerializationPolicy` that defines how long values should be serialized.
    - `datePattern`: A string representing the date pattern to use for date serialization.
    - `dateStyle`: An integer representing the date style for date serialization.
    - `timeStyle`: An integer representing the time style for time serialization.
    - `builderFactories`: A list of `TypeAdapterFactory` objects that are used to create type adapters.
    - `builderHierarchyFactories`: A list of `TypeAdapterFactory` objects that are used to create type adapters for hierarchical types.
    - `factoriesToBeAdded`: A list of `TypeAdapterFactory` objects that are added to the list of factories.
    - `objectToNumberStrategy`: A `ToNumberStrategy` that defines how objects should be converted to numbers.
    - `numberToNumberStrategy`: A `ToNumberStrategy` that defines how numbers should be converted to other number types.
    - `reflectionFilters`: A list of `ReflectionAccessFilter` objects that define access filters for reflection.
- **Control Flow**:
    - Initialize instance variables with the provided parameters.
    - Create a `ConstructorConstructor` using `instanceCreators`, `useJdkUnsafe`, and `reflectionFilters`.
    - Initialize a list of `TypeAdapterFactory` objects called `factories`.
    - Add built-in type adapters to the `factories` list, including JSON element and object type adapters.
    - Add the `excluder` to the `factories` list to precede user-defined type adapters.
    - Add user-defined type adapters from `factoriesToBeAdded` to the `factories` list.
    - Add type adapters for basic platform types such as String, Integer, Boolean, etc., to the `factories` list.
    - Add type adapters for composite and user-defined types, including collection and map type adapters, to the `factories` list.
    - Create a `JsonAdapterAnnotationTypeAdapterFactory` and add it to the `factories` list.
    - Make the `factories` list unmodifiable and assign it to the instance variable `factories`.
- **Output**:
    - A `Gson` instance configured with the specified options and a list of type adapter factories for JSON serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.getFactory`](internal/bind/ObjectTypeAdapter.java.driver.md#ObjectTypeAdaptergetFactory)
    - [`com.google.gson.JsonArray.addAll`](JsonArray.java.driver.md#JsonArrayaddAll)
    - [`com.google.gson.Gson.longAdapter`](#GsonlongAdapter)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactory`](internal/bind/TypeAdapters.java.driver.md#TypeAdaptersnewFactory)
    - [`com.google.gson.Gson.doubleAdapter`](#GsondoubleAdapter)
    - [`com.google.gson.Gson.floatAdapter`](#GsonfloatAdapter)
    - [`com.google.gson.Gson.atomicLongAdapter`](#GsonatomicLongAdapter)
    - [`com.google.gson.Gson.atomicLongArrayAdapter`](#GsonatomicLongArrayAdapter)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.newBuilder<!-- {{#callable:com.google.gson.Gson.newBuilder}} -->
The `newBuilder` method creates and returns a new `GsonBuilder` instance initialized with the current `Gson` instance's configuration.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns a new `GsonBuilder` object, passing `this` (the current `Gson` instance) to the `GsonBuilder` constructor.
- **Output**:
    - A new `GsonBuilder` instance initialized with the current `Gson` instance's settings.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.excluder<!-- {{#callable:com.google.gson.Gson.excluder}} -->
The `excluder` method returns the `Excluder` instance associated with the `Gson` object.
- **Modifiers**: `public`, `deprecated`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the `excluder` field of the `Gson` class.
- **Output**:
    - Returns the `Excluder` instance associated with the `Gson` object.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fieldNamingStrategy<!-- {{#callable:com.google.gson.Gson.fieldNamingStrategy}} -->
The `fieldNamingStrategy` method returns the field naming strategy used by the current Gson instance.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `fieldNamingStrategy` field of the `Gson` class.
- **Output**:
    - The method returns an instance of `FieldNamingStrategy`.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.serializeNulls<!-- {{#callable:com.google.gson.Gson.serializeNulls}} -->
The `serializeNulls` method returns the current configuration setting for whether null values should be serialized in JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `serializeNulls` boolean field.
- **Output**:
    - A boolean value indicating whether null values are serialized.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.htmlSafe<!-- {{#callable:com.google.gson.Gson.htmlSafe}} -->
The `htmlSafe` method returns the current state of the `htmlSafe` boolean field, indicating whether the Gson instance is configured to produce HTML-safe JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the value of the `htmlSafe` field.
- **Output**:
    - A boolean value indicating whether the Gson instance is configured to produce HTML-safe JSON output.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.doubleAdapter<!-- {{#callable:com.google.gson.Gson.doubleAdapter}} -->
The `doubleAdapter` method returns a `TypeAdapter<Number>` for handling JSON serialization and deserialization of `double` values, with special handling for special floating point values based on the input flag.
- **Modifiers**: `private`
- **Inputs**:
    - `serializeSpecialFloatingPointValues`: A boolean flag indicating whether special floating point values (NaN, Infinity) should be serialized.
- **Control Flow**:
    - Check if `serializeSpecialFloatingPointValues` is true.
    - If true, return the predefined `TypeAdapters.DOUBLE`.
    - If false, return a new `TypeAdapter<Number>` with overridden `read` and `write` methods.
    - In the `read` method, check if the next JSON token is `NULL`; if so, consume it and return `null`, otherwise return the next double value.
    - In the `write` method, check if the value is `null`; if so, write a `null` value, otherwise convert the number to a double, validate it, and write it.
- **Output**:
    - A `TypeAdapter<Number>` instance for handling `double` values in JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.nullValue`](stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.doubleValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberdoubleValue)
    - [`com.google.gson.Gson.checkValidFloatingPoint`](#GsoncheckValidFloatingPoint)
    - [`com.google.gson.stream.JsonWriter.value`](stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.floatAdapter<!-- {{#callable:com.google.gson.Gson.floatAdapter}} -->
The `floatAdapter` method returns a `TypeAdapter<Number>` for handling JSON serialization and deserialization of floating-point numbers, with special handling based on whether special floating-point values should be serialized.
- **Modifiers**: `private`
- **Inputs**:
    - `serializeSpecialFloatingPointValues`: A boolean indicating whether special floating-point values (like NaN or Infinity) should be serialized.
- **Control Flow**:
    - Check if `serializeSpecialFloatingPointValues` is true.
    - If true, return the predefined `TypeAdapters.FLOAT`.
    - If false, return a new `TypeAdapter<Number>` with custom `read` and `write` methods.
    - In the `read` method, check if the next JSON token is `NULL`, and if so, consume it and return `null`; otherwise, read the next double value and cast it to a float.
    - In the `write` method, check if the value is `null`, and if so, write a `null` value; otherwise, convert the value to a float, validate it, and write it as a JSON value.
- **Output**:
    - A `TypeAdapter<Number>` that can read and write JSON representations of floating-point numbers.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextDouble`](stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.nullValue`](stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.floatValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberfloatValue)
    - [`com.google.gson.Gson.checkValidFloatingPoint`](#GsoncheckValidFloatingPoint)
    - [`com.google.gson.stream.JsonWriter.value`](stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.checkValidFloatingPoint<!-- {{#callable:com.google.gson.Gson.checkValidFloatingPoint}} -->
The `checkValidFloatingPoint` method validates a double value to ensure it is neither NaN nor infinite, throwing an exception if it is.
- **Modifiers**: `static`
- **Inputs**:
    - `value`: A double value that needs to be validated against JSON specification for floating-point numbers.
- **Control Flow**:
    - The method checks if the input `value` is either NaN (Not-a-Number) or infinite using `Double.isNaN(value)` and `Double.isInfinite(value)`.
    - If either condition is true, the method throws an `IllegalArgumentException` with a message indicating that the value is not valid as per JSON specification and suggests using `GsonBuilder.serializeSpecialFloatingPointValues()` to override this behavior.
- **Output**:
    - The method does not return any value; it either completes without exception or throws an `IllegalArgumentException` if the input is invalid.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.longAdapter<!-- {{#callable:com.google.gson.Gson.longAdapter}} -->
The `longAdapter` method returns a `TypeAdapter<Number>` for handling JSON serialization and deserialization of `long` values based on the specified `LongSerializationPolicy`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `longSerializationPolicy`: An instance of `LongSerializationPolicy` that determines how `long` values should be serialized.
- **Control Flow**:
    - Check if the `longSerializationPolicy` is `LongSerializationPolicy.DEFAULT`.
    - If true, return the default `TypeAdapters.LONG` adapter.
    - If false, return a custom `TypeAdapter<Number>` that handles reading and writing of `long` values as strings.
- **Output**:
    - A `TypeAdapter<Number>` that serializes and deserializes `long` values according to the specified `LongSerializationPolicy`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextLong`](stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonWriter.nullValue`](stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.value`](stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.atomicLongAdapter<!-- {{#callable:com.google.gson.Gson.atomicLongAdapter}} -->
The `atomicLongAdapter` method creates a type adapter for `AtomicLong` that uses a provided `TypeAdapter<Number>` to handle JSON serialization and deserialization.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `longAdapter`: A `TypeAdapter<Number>` used to serialize and deserialize the `AtomicLong` value.
- **Control Flow**:
    - A new `TypeAdapter<AtomicLong>` is instantiated.
    - The [`write`](TypeAdapter.java.driver.md#TypeAdapterwrite) method of the adapter uses `longAdapter` to write the `AtomicLong` value to a `JsonWriter`.
    - The [`read`](TypeAdapter.java.driver.md#TypeAdapterread) method of the adapter uses `longAdapter` to read a `Number` from a `JsonReader` and converts it to an `AtomicLong`.
    - The adapter is returned as a null-safe adapter using the `nullSafe()` method.
- **Output**:
    - A `TypeAdapter<AtomicLong>` that is null-safe and uses the provided `longAdapter` for JSON operations.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.nullSafe`](TypeAdapter.java.driver.md#TypeAdapternullSafe)
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.TypeAdapter.read`](TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.atomicLongArrayAdapter<!-- {{#callable:com.google.gson.Gson.atomicLongArrayAdapter}} -->
The `atomicLongArrayAdapter` method creates a `TypeAdapter` for serializing and deserializing `AtomicLongArray` objects using a provided `TypeAdapter` for `Number`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `longAdapter`: A `TypeAdapter<Number>` used to serialize and deserialize individual long values within the `AtomicLongArray`.
- **Control Flow**:
    - A new `TypeAdapter<AtomicLongArray>` is created and returned.
    - The [`write`](TypeAdapter.java.driver.md#TypeAdapterwrite) method of the `TypeAdapter` begins a JSON array, iterates over the `AtomicLongArray`, and uses the `longAdapter` to write each long value to the `JsonWriter` before ending the JSON array.
    - The [`read`](TypeAdapter.java.driver.md#TypeAdapterread) method of the `TypeAdapter` begins reading a JSON array, uses the `longAdapter` to read each long value into a `List<Long>`, and then constructs an `AtomicLongArray` from this list before returning it.
    - The `TypeAdapter` is made null-safe by calling `nullSafe()` on it.
- **Output**:
    - A `TypeAdapter<AtomicLongArray>` that can serialize and deserialize `AtomicLongArray` objects to and from JSON.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.nullSafe`](TypeAdapter.java.driver.md#TypeAdapternullSafe)
    - [`com.google.gson.stream.JsonWriter.beginArray`](stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.length`](internal/Streams.java.driver.md#CurrentWritelength)
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.JsonStreamParser.hasNext`](JsonStreamParser.java.driver.md#JsonStreamParserhasNext)
    - [`com.google.gson.TypeAdapter.read`](TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
    - [`com.google.gson.JsonObject.add`](JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.size`](JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.JsonArray.set`](JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.getAdapter<!-- {{#callable:com.google.gson.Gson.getAdapter}} -->
The `getAdapter` method retrieves or creates a `TypeAdapter` for a given `TypeToken`, caching it for future use.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `TypeToken<T>` representing the type for which a `TypeAdapter` is requested.
- **Control Flow**:
    - Check if the `type` is null and throw a `NullPointerException` if it is.
    - Attempt to retrieve a cached `TypeAdapter` from `typeTokenCache` for the given `type`.
    - If a cached adapter is found, cast it to `TypeAdapter<T>` and return it.
    - Retrieve the current thread's map of ongoing adapter requests from `threadLocalAdapterResults`.
    - If no map exists, create a new one, set it in `threadLocalAdapterResults`, and mark this as the initial adapter request.
    - Check if there is an ongoing adapter request for the given `type` in the map; if found, return it.
    - Create a `FutureTypeAdapter` and put it in the map for the given `type`.
    - Iterate over the list of `TypeAdapterFactory` instances to create a `TypeAdapter` for the given `type`.
    - If a `TypeAdapter` is successfully created, set it as the delegate of the `FutureTypeAdapter`, replace the map entry with the actual adapter, and break the loop.
    - If this was the initial adapter request, remove the map from `threadLocalAdapterResults`.
    - If no `TypeAdapter` was created, throw an `IllegalArgumentException`.
    - If this was the initial adapter request, publish the resolved adapters to all threads by putting them in `typeTokenCache`.
    - Return the created `TypeAdapter`.
- **Output**:
    - A `TypeAdapter<T>` for the specified `TypeToken<T>`, either retrieved from cache or newly created.
- **Functions called**:
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonArray.set`](JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterput)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](../../../../../test/java/com/google/gson/JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.FutureTypeAdapter.setDelegate`](#FutureTypeAdaptersetDelegate)
    - [`com.google.gson.JsonObject.remove`](JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.getAdapter<!-- {{#callable:com.google.gson.Gson.getAdapter}} -->
The [`getAdapter`](#GsongetAdapter) method retrieves a `TypeAdapter` for a given class type by converting the class to a `TypeToken` and delegating to another [`getAdapter`](#GsongetAdapter) method.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: The class type for which a `TypeAdapter` is requested.
- **Control Flow**:
    - The method takes a `Class<T>` type as input.
    - It converts the class type to a `TypeToken` using `TypeToken.get(type)`.
    - It calls the overloaded [`getAdapter`](#GsongetAdapter) method with the `TypeToken` to retrieve the `TypeAdapter`.
- **Output**:
    - Returns a `TypeAdapter<T>` for the specified class type.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.getDelegateAdapter<!-- {{#callable:com.google.gson.Gson.getDelegateAdapter}} -->
The `getDelegateAdapter` method retrieves a type adapter for a specified type, bypassing a given factory, and throws an exception if no suitable adapter is found.
- **Modifiers**: `public`
- **Inputs**:
    - `skipPast`: A `TypeAdapterFactory` that should be bypassed when searching for a type adapter.
    - `type`: A `TypeToken<T>` representing the type for which a delegate adapter is being searched.
- **Control Flow**:
    - Check if `skipPast` and `type` are not null, throwing a `NullPointerException` if either is null.
    - If `jsonAdapterFactory` is a class-level JSON adapter factory for the given type and `skipPast`, set `skipPast` to `jsonAdapterFactory`.
    - Initialize a boolean `skipPastFound` to false to track if the `skipPast` factory has been encountered.
    - Iterate over the list of `factories` to find a suitable `TypeAdapter` for the given type.
    - If `skipPastFound` is false, check if the current factory is `skipPast`; if so, set `skipPastFound` to true and continue to the next iteration.
    - If `skipPastFound` is true, attempt to create a `TypeAdapter` using the current factory; if a non-null adapter is found, return it.
    - If no adapter is found after `skipPast` is encountered, throw an `IllegalArgumentException` indicating that the type cannot be serialized or deserialized.
    - If `skipPast` was not found, return the result of `getAdapter(type)` as a fallback.
- **Output**:
    - A `TypeAdapter<T>` for the specified type, or throws an `IllegalArgumentException` if no suitable adapter is found after `skipPast`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory.isClassJsonAdapterFactory`](internal/bind/JsonAdapterAnnotationTypeAdapterFactory.java.driver.md#JsonAdapterAnnotationTypeAdapterFactoryisClassJsonAdapterFactory)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](../../../../../test/java/com/google/gson/JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJsonTree<!-- {{#callable:com.google.gson.Gson.toJsonTree}} -->
The [`toJsonTree`](TypeAdapter.java.driver.md#TypeAdaptertoJsonTree) method converts an object into its JSON tree representation using its class type.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be converted into a JSON tree representation.
- **Control Flow**:
    - Check if the input object `src` is null.
    - If `src` is null, return `JsonNull.INSTANCE`.
    - If `src` is not null, call the overloaded [`toJsonTree`](TypeAdapter.java.driver.md#TypeAdaptertoJsonTree) method with `src` and its class type.
- **Output**:
    - Returns a `JsonElement` representing the JSON tree of the input object, or `JsonNull.INSTANCE` if the input is null.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJsonTree`](TypeAdapter.java.driver.md#TypeAdaptertoJsonTree)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJsonTree<!-- {{#callable:com.google.gson.Gson.toJsonTree}} -->
The `toJsonTree` method serializes an object into its JSON representation as a tree of `JsonElement`s.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
    - `typeOfSrc`: The specific genericized type of the object `src`, which can be obtained using `TypeToken`.
- **Control Flow**:
    - A new `JsonTreeWriter` instance is created to facilitate the writing of the JSON tree.
    - The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method is called with the source object, its type, and the `JsonTreeWriter` to perform the serialization.
    - The [`get`](JsonObject.java.driver.md#JsonObjectget) method of `JsonTreeWriter` is called to retrieve the resulting `JsonElement` tree.
- **Output**:
    - A `JsonElement` representing the JSON tree of the serialized object.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method serializes an object into its JSON representation, handling null objects by returning a JSON representation of `JsonNull.INSTANCE`.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
- **Control Flow**:
    - Check if the input object `src` is null.
    - If `src` is null, call `toJson(JsonNull.INSTANCE)` to get the JSON representation of a null object.
    - If `src` is not null, call `toJson(src, src.getClass())` to serialize the object using its class type.
- **Output**:
    - A JSON string representation of the input object.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method serializes an object into its JSON representation using a specified type and returns it as a string.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
    - `typeOfSrc`: The specific genericized type of the object to be serialized.
- **Control Flow**:
    - A new `StringBuilder` instance named `writer` is created to hold the JSON output.
    - The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method is called with `src`, `typeOfSrc`, and `writer` as arguments to perform the serialization.
    - The [`toString`](TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) method of `writer` is called to convert the accumulated JSON content into a string.
    - The resulting JSON string is returned.
- **Output**:
    - A string containing the JSON representation of the input object.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method serializes an object into its JSON representation and writes it to a specified writer.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
    - `writer`: An Appendable object where the JSON representation of the object will be written.
- **Control Flow**:
    - Check if the `src` object is not null.
    - If `src` is not null, call the overloaded [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method with `src`, its class type, and the writer.
    - If `src` is null, call the overloaded [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method with `JsonNull.INSTANCE` and the writer.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the object to the provided writer.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method serializes an object into its JSON representation and writes it to a specified `Appendable` writer.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
    - `typeOfSrc`: The specific genericized type of the source object, which can be obtained using `TypeToken`.
    - `writer`: An `Appendable` object where the JSON representation of the source object will be written.
- **Control Flow**:
    - A `JsonWriter` is created using a new JSON writer configured for the settings on this Gson instance, which is obtained by calling [`newJsonWriter`](#GsonnewJsonWriter) with a writer for the `Appendable` object.
    - The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method is called with the source object, its type, and the `JsonWriter` to perform the serialization.
    - If an `IOException` occurs during writing, it is caught and wrapped in a `JsonIOException`, which is then thrown.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the source object to the provided `Appendable` writer.
- **Functions called**:
    - [`com.google.gson.Gson.newJsonWriter`](#GsonnewJsonWriter)
    - [`com.google.gson.internal.Streams.writerForAppendable`](internal/Streams.java.driver.md#StreamswriterForAppendable)
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The `toJson` method serializes an object into its JSON representation using a specified `JsonWriter`, while managing writer settings and handling exceptions.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The object to be serialized into JSON.
    - `typeOfSrc`: The specific type of the object to be serialized, used to obtain the appropriate type adapter.
    - `writer`: The `JsonWriter` to which the JSON representation of the object will be written.
- **Control Flow**:
    - Obtain a type adapter for the specified type using [`getAdapter`](#GsongetAdapter) method.
    - Store the current strictness, HTML safety, and null serialization settings of the writer.
    - Set the writer's strictness to the instance's strictness if defined, or to `LENIENT` if the writer's strictness is `LEGACY_STRICT`.
    - Set the writer's HTML safety and null serialization settings to the instance's settings.
    - Use the type adapter to write the object to the writer.
    - Catch `IOException` and throw a `JsonIOException` with the caught exception.
    - Catch `AssertionError` and throw a new `AssertionError` with additional information.
    - In the `finally` block, restore the writer's original strictness, HTML safety, and null serialization settings.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the object to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.isHtmlSafe`](stream/JsonWriter.java.driver.md#JsonWriterisHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.getSerializeNulls`](stream/JsonWriter.java.driver.md#JsonWritergetSerializeNulls)
    - [`com.google.gson.stream.JsonWriter.setHtmlSafe`](stream/JsonWriter.java.driver.md#JsonWritersetHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls)
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method converts a `JsonElement` into its JSON string representation.
- **Modifiers**: `public`
- **Inputs**:
    - `jsonElement`: The `JsonElement` that needs to be converted into a JSON string.
- **Control Flow**:
    - A `StringBuilder` object named `writer` is instantiated to accumulate the JSON string.
    - The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method is called with `jsonElement` and `writer` as arguments to perform the conversion.
    - The accumulated JSON string in `writer` is returned as the output.
- **Output**:
    - A `String` representing the JSON format of the provided `JsonElement`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method serializes a `JsonElement` into its JSON representation and writes it to an `Appendable` writer.
- **Modifiers**: `public`
- **Inputs**:
    - `jsonElement`: The `JsonElement` that represents the JSON tree to be serialized.
    - `writer`: An `Appendable` object where the JSON representation of the `JsonElement` will be written.
- **Control Flow**:
    - A `JsonWriter` is created using a new writer obtained from the `Streams.writerForAppendable` method with the provided `writer` as an argument.
    - The [`toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson) method is called with the `jsonElement` and the newly created `JsonWriter`.
    - If an `IOException` occurs during writing, it is caught and wrapped in a `JsonIOException`, which is then thrown.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the `JsonElement` to the provided `Appendable` writer.
- **Functions called**:
    - [`com.google.gson.Gson.newJsonWriter`](#GsonnewJsonWriter)
    - [`com.google.gson.internal.Streams.writerForAppendable`](internal/Streams.java.driver.md#StreamswriterForAppendable)
    - [`com.google.gson.TypeAdapter.toJson`](TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toJson<!-- {{#callable:com.google.gson.Gson.toJson}} -->
The `toJson` method writes a JSON representation of a `JsonElement` to a `JsonWriter`, applying specific settings for HTML safety, null serialization, and strictness.
- **Modifiers**: `public`
- **Inputs**:
    - `jsonElement`: The `JsonElement` to be serialized into JSON.
    - `writer`: The `JsonWriter` to which the JSON representation of the `JsonElement` will be written.
- **Control Flow**:
    - Store the current settings of the `JsonWriter` for strictness, HTML safety, and null serialization.
    - Set the `JsonWriter`'s HTML safety and null serialization settings to match those of the current `Gson` instance.
    - Adjust the `JsonWriter`'s strictness setting based on the `Gson` instance's strictness or default to `LENIENT` if the writer's strictness is `LEGACY_STRICT`.
    - Attempt to write the `JsonElement` to the `JsonWriter` using `Streams.write`.
    - Catch `IOException` and throw a `JsonIOException` if an error occurs during writing.
    - Catch `AssertionError` and throw a new `AssertionError` with additional version information if an assertion fails.
    - In the `finally` block, restore the original settings of the `JsonWriter` for strictness, HTML safety, and null serialization.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the `JsonElement` to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.getStrictness`](stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.isHtmlSafe`](stream/JsonWriter.java.driver.md#JsonWriterisHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.getSerializeNulls`](stream/JsonWriter.java.driver.md#JsonWritergetSerializeNulls)
    - [`com.google.gson.stream.JsonWriter.setHtmlSafe`](stream/JsonWriter.java.driver.md#JsonWritersetHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.newJsonWriter<!-- {{#callable:com.google.gson.Gson.newJsonWriter}} -->
The `newJsonWriter` method creates and returns a new `JsonWriter` instance configured with specific settings from the `Gson` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `writer`: A `Writer` object to which the `JsonWriter` will write JSON data.
- **Control Flow**:
    - Check if `generateNonExecutableJson` is true; if so, write a non-executable JSON prefix to the writer.
    - Create a new `JsonWriter` instance using the provided `Writer`.
    - Set the formatting style of the `JsonWriter` to the `formattingStyle` of the `Gson` instance.
    - Set the HTML safety of the `JsonWriter` to the `htmlSafe` setting of the `Gson` instance.
    - Set the strictness of the `JsonWriter` to the `strictness` of the `Gson` instance, defaulting to `Strictness.LEGACY_STRICT` if `strictness` is null.
    - Set the `JsonWriter` to serialize nulls based on the `serializeNulls` setting of the `Gson` instance.
    - Return the configured `JsonWriter` instance.
- **Output**:
    - A `JsonWriter` instance configured with the settings from the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](stream/JsonWriter.java.driver.md#JsonWritersetFormattingStyle)
    - [`com.google.gson.stream.JsonWriter.setHtmlSafe`](stream/JsonWriter.java.driver.md#JsonWritersetHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.newJsonReader<!-- {{#callable:com.google.gson.Gson.newJsonReader}} -->
The `newJsonReader` method creates and returns a new `JsonReader` instance configured with the strictness setting of the `Gson` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `reader`: A `Reader` object from which JSON data will be read.
- **Control Flow**:
    - Create a new `JsonReader` instance using the provided `Reader` object.
    - Set the strictness of the `JsonReader` to the `strictness` of the `Gson` instance if it is not null; otherwise, set it to `Strictness.LEGACY_STRICT`.
    - Return the configured `JsonReader` instance.
- **Output**:
    - A `JsonReader` instance configured with the appropriate strictness setting.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON string into an object of a specified class type.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A JSON string that represents the object to be deserialized.
    - `classOfT`: The class of the type T into which the JSON string should be deserialized.
- **Control Flow**:
    - The method calls another overloaded [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the JSON string and a `TypeToken` created from the provided class type `classOfT`.
- **Output**:
    - Returns an object of type T, deserialized from the JSON string.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON string into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `String` containing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to be deserialized.
- **Control Flow**:
    - The method calls another overloaded [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the JSON string and a `TypeToken` created from the `typeOfT` parameter.
    - The `TypeToken.get(typeOfT)` is used to obtain a `TypeToken` instance for the specified type.
    - The method returns the result of the called [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, casting it to the generic type `T`.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON string, or throws a `JsonSyntaxException` if the JSON is not valid for the specified type.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON string into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A JSON string that represents the object to be deserialized.
    - `typeOfT`: A `TypeToken` representing the specific generic type of the object to be deserialized.
- **Control Flow**:
    - Check if the `json` string is `null`; if so, return `null` immediately.
    - Create a `StringReader` from the `json` string.
    - Call the overloaded [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method that takes a `Reader` and a `TypeToken`, passing the `StringReader` and `typeOfT` as arguments.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON string, or `null` if the input JSON string is `null`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes JSON data from a `Reader` into an object of a specified class type.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `Reader` object that provides the JSON data to be deserialized.
    - `classOfT`: The `Class` object representing the type of the object to be deserialized.
- **Control Flow**:
    - The method calls another [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the `json` `Reader` and a `TypeToken` created from `classOfT`.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON data.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes JSON data from a `Reader` into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `Reader` object that provides the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the specific type of the object to be deserialized.
- **Control Flow**:
    - The method calls another [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the `json` `Reader` and a `TypeToken` created from `typeOfT`.
    - The result of this call is cast to the generic type `T` and returned.
- **Output**:
    - An object of type `T` that is deserialized from the JSON data provided by the `Reader`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes JSON data from a `Reader` into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `Reader` object that provides the JSON data to be deserialized.
    - `typeOfT`: A `TypeToken<T>` representing the specific generic type of the object to be deserialized.
- **Control Flow**:
    - Create a `JsonReader` from the provided `Reader` using [`newJsonReader`](#GsonnewJsonReader) method.
    - Deserialize the JSON data into an object of type `T` using the [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method with the `JsonReader` and `TypeToken<T>`.
    - Call [`assertFullConsumption`](#GsonassertFullConsumption) to ensure that the entire JSON document has been consumed during deserialization.
    - Return the deserialized object.
- **Output**:
    - An object of type `T` deserialized from the JSON data.
- **Functions called**:
    - [`com.google.gson.Gson.newJsonReader`](#GsonnewJsonReader)
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.Gson.assertFullConsumption`](#GsonassertFullConsumption)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes JSON data from a `JsonReader` into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `reader`: A `JsonReader` object that provides the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to be deserialized.
- **Control Flow**:
    - The method calls another [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the `reader` and a `TypeToken` created from `typeOfT`.
    - The result of this call is cast to the generic type `T` and returned.
- **Output**:
    - Returns an object of type `T` that represents the deserialized JSON data.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The `fromJson` method deserializes JSON data from a `JsonReader` into an object of a specified type, handling various exceptions and strictness settings.
- **Modifiers**: `public`
- **Inputs**:
    - `reader`: A `JsonReader` object that provides the JSON data to be deserialized.
    - `typeOfT`: A `TypeToken<T>` representing the type of the object to be deserialized.
- **Control Flow**:
    - Initialize a boolean `isEmpty` to true and store the current strictness of the reader in `oldStrictness`.
    - Check if the `Gson` instance has a strictness setting; if so, apply it to the reader. Otherwise, if the reader's strictness is `LEGACY_STRICT`, set it to `LENIENT`.
    - Attempt to peek at the next JSON token to determine if the document is empty, setting `isEmpty` to false if not.
    - Retrieve a `TypeAdapter` for the specified type using `getAdapter(typeOfT)`.
    - Use the `TypeAdapter` to read and deserialize the JSON data into an object of type `T`.
    - Check if the deserialized object is an instance of the expected type, throwing a `ClassCastException` if not.
    - Return the deserialized object.
    - Catch `EOFException` and return null if the document is empty, otherwise throw a `JsonSyntaxException`.
    - Catch `IllegalStateException` and `IOException`, rethrowing them as `JsonSyntaxException`.
    - Catch `AssertionError` and rethrow it with additional version information.
    - In the `finally` block, restore the reader's strictness to its original setting.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON data, or null if the JSON document is empty.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.getStrictness`](stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.Gson.getAdapter`](#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.read`](TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.internal.Primitives.wrap`](internal/Primitives.java.driver.md#Primitiveswrap)
    - [`com.google.gson.reflect.TypeToken.getRawType`](reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON element into an object of a specified class type.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `classOfT`: The `Class` object representing the type of the desired object.
- **Control Flow**:
    - The method calls another overloaded [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method, passing the `json` element and a `TypeToken` created from the `classOfT` parameter.
    - The `TypeToken.get(classOfT)` is used to obtain a type token for the class type `T`.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON element.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON element into an object of a specified type using a type token.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the desired object.
- **Control Flow**:
    - The method casts the result of another [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method call, which takes a `JsonElement` and a `TypeToken`, to the specified type `T`.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON element.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.fromJson<!-- {{#callable:com.google.gson.Gson.fromJson}} -->
The [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method deserializes a JSON element into an object of a specified type using a `TypeToken`.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `TypeToken<T>` representing the specific generic type of the object to be deserialized.
- **Control Flow**:
    - Check if the `json` input is `null`, and if so, return `null`.
    - Create a `JsonTreeReader` from the `json` input.
    - Call the overloaded [`fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson) method with the `JsonTreeReader` and `typeOfT` to perform the deserialization.
- **Output**:
    - Returns an object of type `T` deserialized from the JSON element, or `null` if the input JSON is `null`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.assertFullConsumption<!-- {{#callable:com.google.gson.Gson.assertFullConsumption}} -->
The `assertFullConsumption` method checks if a JSON document has been fully consumed by a `JsonReader` and throws an exception if not.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `obj`: An object that was deserialized from the JSON document.
    - `reader`: A `JsonReader` instance used to read the JSON document.
- **Control Flow**:
    - The method first checks if the `obj` is not null and if the `reader` has not reached the end of the document using `reader.peek() != JsonToken.END_DOCUMENT`.
    - If both conditions are true, it throws a `JsonSyntaxException` indicating that the JSON document was not fully consumed.
    - The method catches `MalformedJsonException` and rethrows it as a `JsonSyntaxException`.
    - It also catches `IOException` and rethrows it as a `JsonIOException`.
- **Output**:
    - The method does not return any value; it throws exceptions if the JSON document is not fully consumed or if there are errors during the check.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)


---
#### Gson\.toString<!-- {{#callable:com.google.gson.Gson.toString}} -->
The `toString` method returns a string representation of the Gson object, detailing its configuration settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method constructs a string by concatenating the values of `serializeNulls`, `factories`, and `constructorConstructor` fields of the Gson object.
    - It uses the `+` operator to concatenate these values into a single string, formatted with labels for each field.
- **Output**:
    - A string that represents the current state of the Gson object, including its `serializeNulls`, `factories`, and `constructorConstructor` settings.
- **See also**: [`com.google.gson.Gson`](#Gson)  (Base Class)



---
### FutureTypeAdapter<!-- {{#class:com.google.gson.Gson.FutureTypeAdapter}} -->
- **Modifiers**: `static`
- **Description**: The `FutureTypeAdapter` class is a specialized type adapter used in Gson to handle cyclic type dependencies during serialization and deserialization processes. It acts as a proxy type adapter that initially holds a null delegate and is later set with the actual type adapter once it is created, allowing for the resolution of cyclic dependencies without causing stack overflow errors. This class extends `SerializationDelegatingTypeAdapter` and ensures that the delegate is set only once, throwing an error if an attempt is made to set it again or if it is accessed before being set.
- **Fields**:
    - `delegate`: `TypeAdapter<T>` Holds the actual `TypeAdapter` instance once it is set, initially null.
- **Methods**:
    - [`com.google.gson.Gson.FutureTypeAdapter.setDelegate`](#FutureTypeAdaptersetDelegate)
    - [`com.google.gson.Gson.FutureTypeAdapter.delegate`](#FutureTypeAdapterdelegate)
    - [`com.google.gson.Gson.FutureTypeAdapter.getSerializationDelegate`](#FutureTypeAdaptergetSerializationDelegate)
    - [`com.google.gson.Gson.FutureTypeAdapter.read`](#FutureTypeAdapterread)
    - [`com.google.gson.Gson.FutureTypeAdapter.write`](#FutureTypeAdapterwrite)

**Methods**

---
#### FutureTypeAdapter\.setDelegate<!-- {{#callable:com.google.gson.Gson.FutureTypeAdapter.setDelegate}} -->
The `setDelegate` method assigns a `TypeAdapter` to the `delegate` field if it hasn't been set already.
- **Modifiers**: `public`
- **Inputs**:
    - `typeAdapter`: A `TypeAdapter<T>` object that is intended to be set as the delegate.
- **Control Flow**:
    - Check if the `delegate` field is already set (not null).
    - If `delegate` is not null, throw an `AssertionError` with the message "Delegate is already set".
    - If `delegate` is null, assign the `typeAdapter` to the `delegate` field.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.Gson.FutureTypeAdapter`](#Gson.FutureTypeAdapter)  (Base Class)


---
#### FutureTypeAdapter\.delegate<!-- {{#callable:com.google.gson.Gson.FutureTypeAdapter.delegate}} -->
The `delegate` method returns the `TypeAdapter` instance if it is initialized, otherwise it throws an `IllegalStateException` if the adapter is used before its dependencies are resolved.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the `delegate` field of type `TypeAdapter<T>`.
    - Check if `delegate` is `null`.
    - If `delegate` is `null`, throw an `IllegalStateException` with a specific error message indicating a cyclic dependency issue.
    - If `delegate` is not `null`, return the `delegate`.
- **Output**:
    - Returns a `TypeAdapter<T>` instance if it is initialized, otherwise throws an `IllegalStateException`.
- **See also**: [`com.google.gson.Gson.FutureTypeAdapter`](#Gson.FutureTypeAdapter)  (Base Class)


---
#### FutureTypeAdapter\.getSerializationDelegate<!-- {{#callable:com.google.gson.Gson.FutureTypeAdapter.getSerializationDelegate}} -->
The `getSerializationDelegate` method returns the delegate `TypeAdapter` for serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the `delegate()` method to retrieve the `TypeAdapter` instance.
    - It returns the `TypeAdapter` instance obtained from the `delegate()` method.
- **Output**:
    - A `TypeAdapter<T>` instance that serves as the serialization delegate.
- **Functions called**:
    - [`com.google.gson.Gson.FutureTypeAdapter.delegate`](#FutureTypeAdapterdelegate)
- **See also**: [`com.google.gson.Gson.FutureTypeAdapter`](#Gson.FutureTypeAdapter)  (Base Class)


---
#### FutureTypeAdapter\.read<!-- {{#callable:com.google.gson.Gson.FutureTypeAdapter.read}} -->
The [`read`](TypeAdapter.java.driver.md#TypeAdapterread) method delegates the reading of JSON data from a `JsonReader` to another `TypeAdapter`.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which JSON data is to be read.
- **Control Flow**:
    - The method calls `delegate()` to obtain a `TypeAdapter` instance.
    - It then calls the [`read`](TypeAdapter.java.driver.md#TypeAdapterread) method on the obtained `TypeAdapter`, passing the `JsonReader` as an argument.
- **Output**:
    - Returns an object of type `T` that is read from the JSON data.
- **Functions called**:
    - [`com.google.gson.Gson.FutureTypeAdapter.delegate`](#FutureTypeAdapterdelegate)
    - [`com.google.gson.TypeAdapter.read`](TypeAdapter.java.driver.md#TypeAdapterread)
- **See also**: [`com.google.gson.Gson.FutureTypeAdapter`](#Gson.FutureTypeAdapter)  (Base Class)


---
#### FutureTypeAdapter\.write<!-- {{#callable:com.google.gson.Gson.FutureTypeAdapter.write}} -->
The [`write`](TypeAdapter.java.driver.md#TypeAdapterwrite) method delegates the writing of a JSON representation of a given value to another `TypeAdapter`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON representation.
    - `value`: The value of type `T` to be serialized into JSON.
- **Control Flow**:
    - The method calls the `delegate()` method to obtain a `TypeAdapter` instance.
    - It then calls the [`write`](TypeAdapter.java.driver.md#TypeAdapterwrite) method on the obtained `TypeAdapter`, passing the `JsonWriter` and the value to be serialized.
- **Output**:
    - The method does not return any value; it writes the JSON representation of the value to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.Gson.FutureTypeAdapter.delegate`](#FutureTypeAdapterdelegate)
    - [`com.google.gson.TypeAdapter.write`](TypeAdapter.java.driver.md#TypeAdapterwrite)
- **See also**: [`com.google.gson.Gson.FutureTypeAdapter`](#Gson.FutureTypeAdapter)  (Base Class)



