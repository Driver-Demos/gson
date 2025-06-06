# Purpose
The [`NonNullElementWrapperList`](#NonNullElementWrapperListNonNullElementWrapperList) class is a specialized implementation of a `List` that wraps around another `List` to enforce a constraint that no `null` elements can be inserted. This class extends `AbstractList` and implements `RandomAccess`, ensuring efficient random access to elements. The primary technical component of this class is its delegation to an `ArrayList`, which is explicitly chosen to guarantee that the underlying list supports random access. The class overrides several methods from `AbstractList` to enforce the non-null constraint, such as [`add`](#NonNullElementWrapperListadd), [`set`](#NonNullElementWrapperListset), and [`nonNull`](#NonNullElementWrapperListnonNull), which checks for null elements and throws a `NullPointerException` if a null is encountered.

The class provides a narrow functionality focused on maintaining a list that disallows null elements, making it useful in scenarios where null values could lead to errors or are semantically invalid. It does not define public APIs or external interfaces beyond those inherited from `AbstractList` and `List`. The class also overrides methods like [`remove`](#NonNullElementWrapperListremove), [`clear`](#NonNullElementWrapperListclear), and [`contains`](#NonNullElementWrapperListcontains) to ensure efficient operations, leveraging the underlying `ArrayList`'s capabilities. This class is part of the `com.google.gson.internal` package, indicating its use in internal operations, likely within the context of the Gson library, where maintaining non-null collections could be critical for data serialization and deserialization processes.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `java.util.AbstractList`
- `java.util.ArrayList`
- `java.util.Collection`
- `java.util.List`
- `java.util.Objects`
- `java.util.RandomAccess`


# Classes

---
### NonNullElementWrapperList<!-- {{#class:com.google.gson.internal.NonNullElementWrapperList}} -->
- **Modifiers**: `public`
- **Description**: The `NonNullElementWrapperList` class is a specialized implementation of the `List` interface that wraps an `ArrayList` to prevent the insertion of `null` elements, ensuring that all elements in the list are non-null. It extends `AbstractList` and implements `RandomAccess` to provide efficient random access to elements. The class overrides several methods to enforce the non-null constraint, throwing a `NullPointerException` if a `null` element is attempted to be added or set. It delegates most operations to the underlying `ArrayList`, ensuring that the list's behavior is consistent with standard list operations while maintaining the non-null invariant.
- **Fields**:
    - `delegate`: `ArrayList<E>` An `ArrayList` that serves as the underlying data structure for storing elements, ensuring `RandomAccess` capability.
- **Methods**:
    - [`com.google.gson.internal.NonNullElementWrapperList.NonNullElementWrapperList`](#NonNullElementWrapperListNonNullElementWrapperList)
    - [`com.google.gson.internal.NonNullElementWrapperList.get`](#NonNullElementWrapperListget)
    - [`com.google.gson.internal.NonNullElementWrapperList.size`](#NonNullElementWrapperListsize)
    - [`com.google.gson.internal.NonNullElementWrapperList.nonNull`](#NonNullElementWrapperListnonNull)
    - [`com.google.gson.internal.NonNullElementWrapperList.set`](#NonNullElementWrapperListset)
    - [`com.google.gson.internal.NonNullElementWrapperList.add`](#NonNullElementWrapperListadd)
    - [`com.google.gson.internal.NonNullElementWrapperList.remove`](#NonNullElementWrapperListremove)
    - [`com.google.gson.internal.NonNullElementWrapperList.clear`](#NonNullElementWrapperListclear)
    - [`com.google.gson.internal.NonNullElementWrapperList.remove`](#NonNullElementWrapperListremove)
    - [`com.google.gson.internal.NonNullElementWrapperList.removeAll`](#NonNullElementWrapperListremoveAll)
    - [`com.google.gson.internal.NonNullElementWrapperList.retainAll`](#NonNullElementWrapperListretainAll)
    - [`com.google.gson.internal.NonNullElementWrapperList.contains`](#NonNullElementWrapperListcontains)
    - [`com.google.gson.internal.NonNullElementWrapperList.indexOf`](#NonNullElementWrapperListindexOf)
    - [`com.google.gson.internal.NonNullElementWrapperList.lastIndexOf`](#NonNullElementWrapperListlastIndexOf)
    - [`com.google.gson.internal.NonNullElementWrapperList.toArray`](#NonNullElementWrapperListtoArray)
    - [`com.google.gson.internal.NonNullElementWrapperList.toArray`](#NonNullElementWrapperListtoArray)
    - [`com.google.gson.internal.NonNullElementWrapperList.equals`](#NonNullElementWrapperListequals)
    - [`com.google.gson.internal.NonNullElementWrapperList.hashCode`](#NonNullElementWrapperListhashCode)
- **Extends/Implements**:
    - `RandomAccess`

**Methods**

---
#### NonNullElementWrapperList\.NonNullElementWrapperList<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.NonNullElementWrapperList}} -->
The constructor `NonNullElementWrapperList` initializes the list by wrapping a non-null `ArrayList` delegate.
- **Modifiers**: `public`
- **Inputs**:
    - `delegate`: An `ArrayList<E>` that serves as the underlying list to be wrapped, which must not be null.
- **Control Flow**:
    - The constructor takes an `ArrayList<E>` as an argument.
    - It uses `Objects.requireNonNull` to ensure that the provided `delegate` is not null.
    - If `delegate` is null, a `NullPointerException` is thrown.
    - If `delegate` is not null, it is assigned to the instance variable `this.delegate`.
- **Output**:
    - This constructor does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.get<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.get}} -->
The `get` method retrieves the element at the specified index from the underlying list.
- **Modifiers**: `public`
- **Inputs**:
    - `index`: The position in the list from which to retrieve the element.
- **Control Flow**:
    - The method calls the `get` method on the `delegate` ArrayList with the provided `index`.
- **Output**:
    - The element at the specified index in the list.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.size<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.size}} -->
The `size` method returns the number of elements in the wrapped list.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls the `size` method on the `delegate` ArrayList instance and returns its result.
- **Output**:
    - An integer representing the number of elements in the `delegate` list.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.nonNull<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.nonNull}} -->
The `nonNull` method checks if the provided element is non-null and throws a `NullPointerException` if it is null.
- **Modifiers**: `private`
- **Inputs**:
    - `element`: The element of generic type E to be checked for nullity.
- **Control Flow**:
    - Check if the input element is null.
    - If the element is null, throw a `NullPointerException` with the message 'Element must be non-null'.
    - If the element is not null, return the element.
- **Output**:
    - The method returns the input element if it is non-null.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.set<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.set}} -->
The `set` method replaces the element at the specified position in the list with the specified non-null element.
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `index`: The position in the list where the element is to be replaced.
    - `element`: The new element to be stored at the specified position, which must be non-null.
- **Control Flow**:
    - The method calls the [`nonNull`](#NonNullElementWrapperListnonNull) helper method to ensure the `element` is not null, throwing a `NullPointerException` if it is.
    - The method then calls the `set` method on the `delegate` list with the `index` and the non-null `element`.
- **Output**:
    - The method returns the element previously at the specified position in the list.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.nonNull`](#NonNullElementWrapperListnonNull)
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.add<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.add}} -->
The `add` method inserts a non-null element at a specified index in the list.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `index`: The position in the list where the element should be inserted.
    - `element`: The element to be added to the list, which must not be null.
- **Control Flow**:
    - The method calls the [`nonNull`](#NonNullElementWrapperListnonNull) helper method to ensure the `element` is not null, throwing a `NullPointerException` if it is.
    - The method then delegates the addition of the element to the specified index in the `delegate` list.
- **Output**:
    - This method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.nonNull`](#NonNullElementWrapperListnonNull)
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.remove<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.remove}} -->
The `remove` method removes and returns the element at the specified index from the underlying list.
- **Modifiers**: `public`
- **Inputs**:
    - `index`: The position in the list from which the element should be removed.
- **Control Flow**:
    - The method calls the `remove` method on the `delegate` ArrayList with the provided index.
    - The element at the specified index is removed from the `delegate` list.
- **Output**:
    - The method returns the element that was removed from the list.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.clear<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.clear}} -->
The `clear` method removes all elements from the underlying list.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the `clear` method on the `delegate` ArrayList, which removes all elements from it.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.remove<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.remove}} -->
The `remove` method removes a specified object from the underlying list and returns whether the removal was successful.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be removed from the list.
- **Control Flow**:
    - The method calls the `remove` method on the `delegate` list, passing the object `o` as an argument.
    - The result of the `delegate.remove(o)` call, which is a boolean indicating if the object was successfully removed, is returned.
- **Output**:
    - A boolean value indicating whether the object was successfully removed from the list.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.removeAll<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.removeAll}} -->
The `removeAll` method removes all elements in the specified collection from the list.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `c`: A collection containing elements to be removed from the list.
- **Control Flow**:
    - The method delegates the call to the `removeAll` method of the `delegate` ArrayList, passing the collection `c` as an argument.
- **Output**:
    - Returns `true` if the list changed as a result of the call, otherwise `false`.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.retainAll<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.retainAll}} -->
The `retainAll` method retains only the elements in the list that are contained in the specified collection.
- **Modifiers**: `public`
- **Inputs**:
    - `c`: A collection containing elements to be retained in the list.
- **Control Flow**:
    - The method calls the `retainAll` method on the `delegate` ArrayList, passing the collection `c` as an argument.
    - The `delegate.retainAll(c)` operation modifies the list to retain only elements that are also contained in the specified collection `c`.
- **Output**:
    - Returns `true` if the list was modified as a result of the call, otherwise `false`.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.contains<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.contains}} -->
The `contains` method checks if a specified object is present in the underlying list.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be checked for presence in the list.
- **Control Flow**:
    - The method directly calls the `contains` method on the `delegate` ArrayList with the provided object `o`.
- **Output**:
    - Returns `true` if the object is found in the list, otherwise returns `false`.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.indexOf<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.indexOf}} -->
The [`indexOf`](GsonTypes.java.driver.md#GsonTypesindexOf) method returns the index of the first occurrence of a specified object in the list, or -1 if the object is not found.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `o`: The object to search for in the list.
- **Control Flow**:
    - The method calls the [`indexOf`](GsonTypes.java.driver.md#GsonTypesindexOf) method on the `delegate` ArrayList, passing the object `o` as an argument.
    - The result from the `delegate.indexOf(o)` call is returned directly.
- **Output**:
    - The method returns an integer representing the index of the first occurrence of the specified object in the list, or -1 if the object is not found.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.indexOf`](GsonTypes.java.driver.md#GsonTypesindexOf)
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.lastIndexOf<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.lastIndexOf}} -->
The `lastIndexOf` method returns the index of the last occurrence of a specified object in the list.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to search for in the list.
- **Control Flow**:
    - The method calls `lastIndexOf` on the `delegate` ArrayList, passing the object `o` as an argument.
    - The result from the `delegate`'s `lastIndexOf` method is returned.
- **Output**:
    - The method returns an integer representing the index of the last occurrence of the specified object in the list, or -1 if the object is not found.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.toArray<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.toArray}} -->
The [`toArray`](#NonNullElementWrapperListtoArray) method returns an array containing all of the elements in the list in proper sequence.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`toArray`](#NonNullElementWrapperListtoArray) method on the `delegate` ArrayList instance.
    - The result of the `delegate.toArray()` call is returned directly.
- **Output**:
    - An array of `Object` type containing all elements from the list.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.toArray`](#NonNullElementWrapperListtoArray)
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.toArray<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.toArray}} -->
The [`toArray`](#NonNullElementWrapperListtoArray) method returns an array containing all of the elements in this list, using the provided array if it is large enough.
- **Modifiers**: `public`
- **Inputs**:
    - `a`: An array into which the elements of the list are to be stored, if it is big enough; otherwise, a new array of the same runtime type is allocated for this purpose.
- **Control Flow**:
    - The method calls the [`toArray`](#NonNullElementWrapperListtoArray) method on the `delegate` ArrayList, passing the provided array `a` as an argument.
    - The result of the `delegate.toArray(a)` call is returned.
- **Output**:
    - An array containing all of the elements in this list.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.toArray`](#NonNullElementWrapperListtoArray)
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.equals<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.equals}} -->
The `equals` method checks if the current `NonNullElementWrapperList` is equal to another object by delegating the equality check to the underlying `ArrayList`.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be compared for equality with the current list.
- **Control Flow**:
    - The method calls the `equals` method on the `delegate` (an `ArrayList`) with the provided object `o` as the argument.
- **Output**:
    - A boolean value indicating whether the current list is equal to the specified object.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)


---
#### NonNullElementWrapperList\.hashCode<!-- {{#callable:com.google.gson.internal.NonNullElementWrapperList.hashCode}} -->
The `hashCode` method returns the hash code of the underlying delegate list.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls and returns the result of the `hashCode` method on the `delegate` object, which is an `ArrayList`.
- **Output**:
    - The method returns an integer representing the hash code of the `delegate` list.
- **See also**: [`com.google.gson.internal.NonNullElementWrapperList`](#NonNullElementWrapperList)  (Base Class)



