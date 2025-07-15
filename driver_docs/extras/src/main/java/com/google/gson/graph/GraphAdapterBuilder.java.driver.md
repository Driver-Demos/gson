# Purpose
The provided Java source code defines a class [`GraphAdapterBuilder`](#GraphAdapterBuilderGraphAdapterBuilder) within the `com.google.gson.graph` package, which is designed to facilitate the serialization and deserialization of object graphs with cyclic references using the Gson library. This class allows developers to register specific types for which cyclic references are permissible, enabling the serialization of complex object graphs as a list of named nodes. The primary functionality of this class is to ensure that objects referencing each other, or themselves, are correctly serialized and deserialized by assigning unique identifiers to each object instance during serialization and reconstructing the object graph during deserialization.

The [`GraphAdapterBuilder`](#GraphAdapterBuilderGraphAdapterBuilder) class is composed of several key components, including a map of `InstanceCreator` instances for registered types and a `ConstructorConstructor` to manage object construction. The class provides methods such as [`addType`](#GraphAdapterBuilderaddType) to register types with default or custom instance creators and [`registerOn`](#GraphAdapterBuilderregisterOn) to integrate the graph adapter with a `GsonBuilder`. The internal [`Factory`](#FactoryFactory) class implements both `TypeAdapterFactory` and `InstanceCreator` interfaces, handling the creation of type adapters that manage cyclic references by assigning unique names to objects and managing the graph during serialization and deserialization. The code also includes a [`Graph`](#GraphGraph) class to maintain the mapping of objects to their serialized forms and an [`Element`](#ElementElement) class to represent individual elements within the graph. This setup provides a robust mechanism for handling complex object graphs in JSON serialization and deserialization processes.
# Imports and Dependencies

---
- `com.google.gson.graph`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.InstanceCreator`
- `com.google.gson.JsonElement`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.internal.ConstructorConstructor`
- `com.google.gson.internal.ObjectConstructor`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `java.util.ArrayDeque`
- `java.util.Collections`
- `java.util.HashMap`
- `java.util.IdentityHashMap`
- `java.util.Map`
- `java.util.Queue`


# Classes

---
### GraphAdapterBuilder<!-- {{#class:com.google.gson.graph.GraphAdapterBuilder}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `GraphAdapterBuilder` class is a builder for constructing graph-aware type adapters in Gson, allowing for the serialization and deserialization of object graphs with cyclic references. It maintains a mapping between types and their corresponding `InstanceCreator` instances, enabling the serialization of objects as a list of named nodes. This approach ensures that objects referencing each other or themselves are properly handled during serialization and deserialization. The class provides methods to register types with default or custom instance creators and to register the graph adapter on a `GsonBuilder`, facilitating the creation of a `Gson` instance capable of handling complex object graphs.
- **Fields**:
    - `instanceCreators`: `Map<Type, InstanceCreator<?>>` A map that holds the association between types and their corresponding instance creators.
    - `constructorConstructor`: `ConstructorConstructor` An instance of `ConstructorConstructor` used to obtain object constructors for types.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilder.GraphAdapterBuilder`](#GraphAdapterBuilderGraphAdapterBuilder)
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](#GraphAdapterBuilderregisterOn)

**Methods**

---
#### GraphAdapterBuilder\.GraphAdapterBuilder<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.GraphAdapterBuilder}} -->
The `GraphAdapterBuilder` constructor initializes a new instance of the class with default settings for instance creators and constructor constructor.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor initializes the `instanceCreators` field as a new `HashMap` to store type-instance creator mappings.
    - It initializes the `constructorConstructor` field using a new `ConstructorConstructor` with empty maps and lists, allowing for default instance creation behavior.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder`](#GraphAdapterBuilder)  (Base Class)


---
#### GraphAdapterBuilder\.addType<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.addType}} -->
The [`addType`](#GraphAdapterBuilderaddType) method registers a specified type with a default instance creator for use in a graph-aware type adapter.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: The type to register, represented as a `Type` object.
- **Control Flow**:
    - Retrieve an `ObjectConstructor` for the given type using `constructorConstructor.get` with a `TypeToken` of the type.
    - Create an `InstanceCreator` anonymous class that uses the `ObjectConstructor` to construct instances of the type.
    - Call the overloaded [`addType`](#GraphAdapterBuilderaddType) method with the type and the newly created `InstanceCreator`.
- **Output**:
    - Returns the current `GraphAdapterBuilder` instance to allow method chaining.
- **Functions called**:
    - [`com.google.gson.internal.ConstructorConstructor.get`](../../../../../../../../gson/src/main/java/com/google/gson/internal/ConstructorConstructor.java.driver.md#ConstructorConstructorget)
    - [`com.google.gson.internal.ObjectConstructor.construct`](../../../../../../../../gson/src/main/java/com/google/gson/internal/ObjectConstructor.java.driver.md#ObjectConstructorconstruct)
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](#GraphAdapterBuilderaddType)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder`](#GraphAdapterBuilder)  (Base Class)


---
#### GraphAdapterBuilder\.addType<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.addType}} -->
The `addType` method registers a specified type with a provided instance creator in the `GraphAdapterBuilder`.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: The type to register, which is a `Type` object.
    - `instanceCreator`: The `InstanceCreator` used to create instances of the type during deserialization.
- **Control Flow**:
    - Check if either `type` or `instanceCreator` is null, and throw a `NullPointerException` if so.
    - Add the `type` and `instanceCreator` to the `instanceCreators` map.
    - Return the current instance of `GraphAdapterBuilder` for method chaining.
- **Output**:
    - Returns the current `GraphAdapterBuilder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder`](#GraphAdapterBuilder)  (Base Class)


---
#### GraphAdapterBuilder\.registerOn<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.registerOn}} -->
The `registerOn` method registers a custom type adapter factory and associated type adapters on a provided `GsonBuilder` to handle serialization and deserialization of object graphs with cyclic references.
- **Modifiers**: `public`
- **Inputs**:
    - `gsonBuilder`: The `GsonBuilder` instance on which the graph adapter and type adapters are to be registered.
- **Control Flow**:
    - Create a copy of the `instanceCreators` map to avoid affecting the original adapter factory.
    - Instantiate a `Factory` object using the copied `instanceCreators` map.
    - Register the `Factory` instance as a type adapter factory on the provided `gsonBuilder`.
    - Iterate over each entry in the `instanceCreators` map and register a type adapter for each type using the `Factory` instance on the `gsonBuilder`.
- **Output**:
    - The method does not return any value; it modifies the provided `GsonBuilder` by registering the necessary type adapters.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder`](#GraphAdapterBuilder)  (Base Class)



---
### Factory<!-- {{#class:com.google.gson.graph.GraphAdapterBuilder.Factory}} -->
- **Modifiers**: `static`
- **Description**: The `Factory` class is a specialized implementation of both `TypeAdapterFactory` and `InstanceCreator<Object>` interfaces, designed to handle the serialization and deserialization of object graphs with cyclic references using Gson. It manages a mapping of types to their respective `InstanceCreator` instances and utilizes a `ThreadLocal` to maintain a `Graph` object during serialization and deserialization processes. This allows the `Factory` to assign unique identifiers to objects, ensuring that cyclic references are correctly serialized and deserialized by maintaining a graph of objects as a list of named nodes.
- **Fields**:
    - `instanceCreators`: `Map<Type, InstanceCreator<?>>` A map that holds types and their corresponding instance creators.
    - `graphThreadLocal`: `ThreadLocal<Graph>` A ThreadLocal variable that holds the current graph being processed during serialization or deserialization.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilder.Factory.Factory`](#FactoryFactory)
    - [`com.google.gson.graph.GraphAdapterBuilder.Factory.create`](#Factorycreate)
    - [`com.google.gson.graph.GraphAdapterBuilder.Factory.createInstance`](#FactorycreateInstance)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### Factory\.Factory<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Factory.Factory}} -->
The `Factory` constructor initializes a `Factory` instance with a map of type-instance creator pairs.
- **Inputs**:
    - `instanceCreators`: A map where keys are `Type` objects and values are `InstanceCreator<?>` objects, used to create instances of the specified types during deserialization.
- **Control Flow**:
    - The constructor assigns the provided `instanceCreators` map to the `instanceCreators` field of the `Factory` instance.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Factory`](#GraphAdapterBuilder.Factory)  (Base Class)


---
#### Factory\.create<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Factory.create}} -->
The `create` method generates a `TypeAdapter` for a specified type, enabling serialization and deserialization of object graphs with cyclic references using unique identifiers.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of `Gson` used to obtain delegate adapters for serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Check if the `instanceCreators` map contains the specified type; if not, return null.
    - Obtain a delegate `TypeAdapter` for the specified type using the provided `Gson` instance.
    - Obtain a `TypeAdapter` for `JsonElement` using the provided `Gson` instance.
    - Return a new `TypeAdapter` instance with overridden [`write`](#Elementwrite) and [`read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread) methods.
    - In the [`write`](#Elementwrite) method, check if the value is null and write a null value if so.
    - Retrieve or create a `Graph` object from a thread-local variable to manage serialization state.
    - Determine if the entire graph should be written based on whether the graph is null.
    - Retrieve or create an `Element` for the value, adding it to the graph's map and queue if necessary.
    - If writing the entire graph, serialize each element in the graph's queue to JSON, otherwise write the element's ID.
    - In the [`read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread) method, check if the next token is null and return null if so.
    - Retrieve or create a `Graph` object from a thread-local variable to manage deserialization state.
    - Determine if the entire graph should be read based on whether the graph is null.
    - If reading the entire graph, read all elements into the graph's map from JSON.
    - Retrieve the `Element` for the current name and deserialize its value if necessary.
    - Return the deserialized value.
- **Output**:
    - A `TypeAdapter<T>` capable of serializing and deserializing object graphs with cyclic references, or null if the type is not supported.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
    - [`com.google.gson.Gson.getAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.graph.GraphAdapterBuilder.Graph.nextName`](#GraphnextName)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.graph.GraphAdapterBuilder.Element.write`](#Elementwrite)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderhasNext)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.TypeAdapter.read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.stream.JsonReader.endObject`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendObject)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Factory`](#GraphAdapterBuilder.Factory)  (Base Class)


---
#### Factory\.createInstance<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Factory.createInstance}} -->
The [`createInstance`](../../../../../../../../gson/src/main/java/com/google/gson/InstanceCreator.java.driver.md#InstanceCreatorcreateInstance) method creates an instance of a specified type using a registered `InstanceCreator` and manages the deserialization process within a graph context.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: The `Type` of the object to be created.
- **Control Flow**:
    - Retrieve the current `Graph` object from the `graphThreadLocal` thread-local variable.
    - Check if the `graph` is null or if `graph.nextCreate` is null, and throw an `IllegalStateException` if either is true, indicating an unexpected call to [`createInstance`](../../../../../../../../gson/src/main/java/com/google/gson/InstanceCreator.java.driver.md#InstanceCreatorcreateInstance).
    - Retrieve the `InstanceCreator` associated with the given `type` from the `instanceCreators` map.
    - Use the `InstanceCreator` to create an instance of the specified `type`.
    - Assign the created instance to `graph.nextCreate.value`.
    - Set `graph.nextCreate` to null, indicating that the current deserialization process is complete.
    - Return the created instance.
- **Output**:
    - Returns an `Object` which is an instance of the specified `type` created by the `InstanceCreator`.
- **Functions called**:
    - [`com.google.gson.InstanceCreator.createInstance`](../../../../../../../../gson/src/main/java/com/google/gson/InstanceCreator.java.driver.md#InstanceCreatorcreateInstance)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Factory`](#GraphAdapterBuilder.Factory)  (Base Class)



---
### Graph<!-- {{#class:com.google.gson.graph.GraphAdapterBuilder.Graph}} -->
- **Modifiers**: `static`
- **Description**: The `Graph` class is a utility class used within the `GraphAdapterBuilder` to manage the serialization and deserialization of object graphs, particularly handling cyclic references by maintaining a mapping of graph elements. It uses a map to store elements with keys as objects during serialization and string names during deserialization, and a queue to manage elements to be serialized. The class also provides a mechanism to generate unique names for elements and manages the current instance being deserialized.
- **Fields**:
    - `map`: `Map<Object, Element<?>>` A map storing graph elements with keys as objects during serialization and string names during deserialization.
    - `queue`: `Queue<Element<?>>` A queue of elements to be written during serialization, unused during deserialization.
    - `nextCreate`: `Element<Object>` The instance currently being deserialized, used as a backdoor between graph traversal and instance creation.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilder.Graph.Graph`](#GraphGraph)
    - [`com.google.gson.graph.GraphAdapterBuilder.Graph.nextName`](#GraphnextName)

**Methods**

---
#### Graph\.Graph<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Graph.Graph}} -->
The private constructor `Graph` initializes a `Graph` object with a given map of elements.
- **Modifiers**: `private`
- **Inputs**:
    - `map`: A `Map<Object, Element<?>>` that represents the graph elements, where keys are objects during serialization and string names during deserialization.
- **Control Flow**:
    - The constructor assigns the provided `map` to the instance variable `this.map`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Graph` class.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Graph`](#GraphAdapterBuilder.Graph)  (Base Class)


---
#### Graph\.nextName<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Graph.nextName}} -->
The `nextName` method generates a unique hexadecimal string identifier for an element to be inserted into the graph.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calculates the size of the `map` and adds 1 to it.
    - It converts this integer to a hexadecimal string using `Integer.toHexString`.
    - The method returns the hexadecimal string prefixed with '0x'.
- **Output**:
    - A string representing a unique hexadecimal identifier prefixed with '0x'.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Graph`](#GraphAdapterBuilder.Graph)  (Base Class)



---
### Element<!-- {{#class:com.google.gson.graph.GraphAdapterBuilder.Element}} -->
- **Modifiers**: `static`
- **Description**: The `Element` class is a generic inner class designed to represent an element within a graph structure during serialization and deserialization processes, specifically handling cyclic references by associating each element with a unique identifier, a value, a type adapter, and a JSON element.
- **Fields**:
    - `id`: `String` This is the unique identifier for the element within the top-level graph object.
    - `value`: `T` This holds the value of the element, which is lazily populated during deserialization.
    - `typeAdapter`: `TypeAdapter<T>` This is the type adapter for the element, used for serialization and deserialization, and is lazily populated during deserialization.
    - `element`: `JsonElement` This is the JSON element to be deserialized, and it is unused during serialization.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilder.Element.Element`](#ElementElement)
    - [`com.google.gson.graph.GraphAdapterBuilder.Element.write`](#Elementwrite)
    - [`com.google.gson.graph.GraphAdapterBuilder.Element.read`](#Elementread)

**Methods**

---
#### Element\.Element<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Element.Element}} -->
The `Element` constructor initializes an instance of the `Element` class with a value, an identifier, a type adapter, and a JSON element.
- **Inputs**:
    - `value`: The value of type `T` that this element represents.
    - `id`: A `String` representing the unique identifier for this element within the graph.
    - `typeAdapter`: A `TypeAdapter<T>` used for serializing and deserializing the value.
    - `element`: A `JsonElement` representing the JSON data associated with this element, used during deserialization.
- **Control Flow**:
    - Assigns the provided `value` to the instance variable `this.value`.
    - Assigns the provided `id` to the instance variable `this.id`.
    - Assigns the provided `typeAdapter` to the instance variable `this.typeAdapter`.
    - Assigns the provided `element` to the instance variable `this.element`.
- **Output**:
    - This constructor does not return a value as it is used to instantiate an `Element` object.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Element`](#GraphAdapterBuilder.Element)  (Base Class)


---
#### Element\.write<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Element.write}} -->
The [`write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite) method serializes a given value using a specified `TypeAdapter` and writes it to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` object where the serialized data will be written.
- **Control Flow**:
    - The method calls the [`write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite) method of the `typeAdapter` object, passing the `JsonWriter` and the `value` to be serialized.
- **Output**:
    - The method does not return any value; it writes the serialized data to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Element`](#GraphAdapterBuilder.Element)  (Base Class)


---
#### Element\.read<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilder.Element.read}} -->
The `read` method deserializes a JSON element into a Java object, ensuring no recursive calls occur during the process.
- **Inputs**:
    - `graph`: An instance of the Graph class that manages the mapping of elements during deserialization.
- **Control Flow**:
    - Check if `graph.nextCreate` is not null, indicating a recursive call, and throw an IllegalStateException if true.
    - Set `graph.nextCreate` to the current element cast to `Element<Object>`.
    - Deserialize the JSON element into a Java object using `typeAdapter.fromJsonTree(element)` and assign it to `value`.
    - If the deserialized `value` is null, throw an IllegalStateException indicating a non-null value was expected.
- **Output**:
    - The method does not return a value but updates the `value` field of the current `Element` instance with the deserialized object.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJsonTree`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJsonTree)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilder.Element`](#GraphAdapterBuilder.Element)  (Base Class)



