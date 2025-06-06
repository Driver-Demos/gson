
## Files
- **[SqlDateTypeAdapter.java](sql/SqlDateTypeAdapter.java.driver.md)**: The `SqlDateTypeAdapter.java` file provides a Gson `TypeAdapter` for serializing and deserializing `java.sql.Date` objects, ensuring thread safety by synchronizing access to the `DateFormat` used for parsing and formatting dates.
- **[SqlTimestampTypeAdapter.java](sql/SqlTimestampTypeAdapter.java.driver.md)**: The `SqlTimestampTypeAdapter.java` file implements a custom Gson `TypeAdapter` for serializing and deserializing SQL `Timestamp` objects using a `Date` type adapter.
- **[SqlTimeTypeAdapter.java](sql/SqlTimeTypeAdapter.java.driver.md)**: The `SqlTimeTypeAdapter.java` file provides a Gson `TypeAdapter` for serializing and deserializing `java.sql.Time` objects, ensuring thread safety by synchronizing access to the `DateFormat` used for parsing and formatting.
- **[SqlTypesSupport.java](sql/SqlTypesSupport.java.driver.md)**: The `SqlTypesSupport.java` file in the `gson` codebase provides a mechanism to handle `java.sql` types in Gson, ensuring compatibility even when the `java.sql` module is not present.
