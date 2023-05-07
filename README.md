# ByteReader

The `ByteReader` class is a utility for reading binary data from an `ArrayBuffer` object. It provides methods for reading various types of data such as integers, floats, strings, and extracting subarrays.

## Usage

To use the `ByteReader` class, you can import it as a default export:

```javascript
import ByteReader from 'ByteReader';
```

### Creating a ByteReader

To create an instance of `ByteReader`, you need to provide an `ArrayBuffer` object containing the binary data you want to read. Additionally, you can specify whether the data should be interpreted in little endian or big endian format (little endian by default).

```javascript
const bytes = new ArrayBuffer(/* ... */);
const reader = new ByteReader(bytes, true);
```

### Seeking

The `seek` method allows you to set the current position within the binary data. It takes an offset parameter that specifies the new position.

```javascript
reader.seek(10); // Set the position to the 10th byte
```

The `seekRel` method is similar to `seek`, but it moves the position relative to the current position.

```javascript
reader.seekRel(5); // Move the position 5 bytes forward
```

The `seekEnd` method sets the position relative to the end of the data. It expects a negative `whence` argument indicating the offset from the end.

```javascript
reader.seekEnd(-3); // Set the position to 3 bytes before the end
```

### Reading Data

The `ByteReader` class provides several methods for reading different types of data:

- `readInt8`: Reads a signed 8-bit integer and advances the position by 1 byte.
- `readUInt8`: Reads an unsigned 8-bit integer and advances the position by 1 byte.
- `readInt16`: Reads a signed 16-bit integer and advances the position by 2 bytes.
- `readUInt16`: Reads an unsigned 16-bit integer and advances the position by 2 bytes.
- `readInt32`: Reads a signed 32-bit integer and advances the position by 4 bytes.
- `readUInt32`: Reads an unsigned 32-bit integer and advances the position by 4 bytes.
- `readFloat`: Reads a 32-bit floating-point number and advances the position by 4 bytes.
- `readString`: Reads a string of characters until a null byte (0) is encountered or until a specified length is reached. Advances the position accordingly.

```javascript
const int8 = reader.readInt8(); // Read a signed 8-bit integer
const uint16 = reader.readUInt16(); // Read an unsigned 16-bit integer
const float = reader.readFloat(); // Read a floating-point number
const str = reader.readString(10); // Read a string of up to 10 characters
```

### Current Position

To retrieve the current position within the binary data, you can use the `tell` method, which returns the offset in bytes.

```javascript
const position = reader.tell(); // Get the current position
```

The `tellf` method returns a formatted string representing the current position in hexadecimal format.

```javascript
const positionStr = reader.tellf(); // Get the current position as a hexadecimal string
```

### Extracting Subarrays

The `subArray` method allows you to extract a subarray from the original `ArrayBuffer` based on start and end offsets. The resulting subarray is returned as a new `ArrayBuffer` object.

```javascript
const sub = reader.subArray(10, 20); // Extract a subarray from position 10 to 20 (exclusive)
```

### Converting to String

The `toString` method allows you to convert a range of bytes within the `ByteReader` to a string. It takes a start offset and an end offset (exclusive) as parameters and returns the corresponding string representation.

```javascript
const str = reader.toString(10, 20); // Convert bytes from position 10 to 20 (exclusive) to a string
```

Please note that this method interprets the bytes as signed 8-bit integers and converts them to their corresponding ASCII characters.

## Example Usage

Here's an example that demonstrates the usage of the `ByteReader` class:

```javascript
const bytes = new ArrayBuffer(/* ... */);
const reader = new ByteReader(bytes);

// Read some data
const int16 = reader.readInt16();
const float = reader.readFloat();
const str = reader.readString(10);

// Get current position
const position = reader.tell();

// Extract a subarray
const sub = reader.subArray(10, 20);

// Convert a range of bytes to string
const strRange = reader.toString(5, 15);
```

In this example, we create a `ByteReader` instance, read different types of data, get the current position, extract a subarray, and convert a range of bytes to a string.

Remember to adjust the method calls and parameters according to your specific use case and binary data format.

## Conclusion

The `ByteReader` class provides a convenient way to read binary data from an `ArrayBuffer`. It offers methods for seeking, reading different types of data, retrieving the current position, extracting subarrays, and converting byte ranges to strings. This utility can be helpful when working with binary file formats, network protocols, or any situation that requires parsing binary data.

## Copyright

Copyright 2023 DashGL Project MIT License
