## ⚡️ Stay tuned for updates: upcoming version 1.0.0 (currently in beta) ⚡️
<p align="center">Please <a href="https://github.com/tonystone/tracelog/stargazers">star</a> this github repository to stay up to date and show your support.</p>

# StickyEncoding ![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-lightgray.svg?style=flat)

<a href="https://github.com/stickytools/sticky-encoding/" target="_blank">
   <img src="https://img.shields.io/badge/platforms-iOS%20%7C%20macOS%20%7C%20watchOS%20%7C%20tvOS%20%7C%20Linux%20-lightgray.svg?style=flat" alt="Platforms: iOS | macOS | watchOS | tvOS | Linux" />
</a>
<a href="https://github.com/stickytools/sticky-encoding/" target="_blank">
   <img src="https://img.shields.io/badge/Swift-4.2-orange.svg?style=flat" alt="Swift 4.2">
</a>
<a href="http://cocoadocs.org/docsets/StickyEncoding" target="_blank">
   <img src="https://img.shields.io/cocoapods/v/StickyEncoding.svg?style=flat" alt="Version"/>
</a>
<a href="https://travis-ci.org/stickytools/sticky-encoding" target="_blank">
  <img src="https://travis-ci.org/stickytools/sticky-encoding.svg?branch=master" alt="travis-ci.org" />
</a>
<a href="https://codecov.io/gh/stickytools/sticky-encoding" target="_blank">
  <img src="https://codecov.io/gh/stickytools/sticky-encoding/branch/master/graph/badge.svg" alt="Codecov" />
</a>

---
StickyEncoding facilitates the encoding and decoding of `Codable` values into and out of a binary
format that can be stored on disk or sent over a socket.

## Documentation

* [User Guides & Reference](https://stickytools.io/sticky-encoding) - Extensive user guides and reference documentation!  100% documented API, full examples and many hidden details.
* [Contributing Guide](CONTRIBUTING.md) - If you'd like to contribute and need instructions on the build environment, this is the place to go.

## Quick Start Guide

Encoding is done using a `BinaryEncoder` instance and will encode any `Encodable` type whether you declare conformance to `Encodable` and let the compiler create the code, or you manually implement the conformance yourself.

Decoding is done using a `BinaryDecoder` instance and can decode any `Decodable` type that was previously encoded using the `BinaryEncoder`. Of course you can declare `Encodable` or `Decodable` conformance by using `Codable` as well.

StickyEncoding creates a compact binary format that represents the encoded object or data type.  You can read more about the format in the document [Binary Format](Sources/Documentation/Sections/Binary&#32;Format.md).

To facilitate many use cases, StickyEncoding encodes the data to an instance of `EncodedData`.  EncodedData contains a binary format suitable
for writing directly to memory, disk, or into a byte array. Or in the case of decoding, the format facilitates rapid decoding to Swift instances.

### Encoding

To create an instance of a BinaryEncoder:
```Swift
    let encoder = BinaryEncoder()
```

> Note: You may optionally pass your own userInfo `BinaryEncoder(userInfo:)` structure and it will be available to you during the encoding.

You can encode any top-level single value type including Int,
UInt, Double, Bool, and Strings. Simply pass the value to the instance
of the BinaryEncoder and call `encode`.
```Swift
   let string = "You can encode single values of any type."

   let bytes = try encoder.encode(string)
```
Basic structs and classes can also be encoded.
```Swift
   struct Employee: Codable {
        let first: String
        let last: String
        let employeeNumber: Int
   }

   let employee = Employee(first: "John", last: "Doe", employeeNumber: 2345643)

   let bytes = try encoder.encode(employee)
```
As well as Complex types with sub classes.

### Decoding

To create an instance of a BinaryDecoder:
```Swift
    let decoder = BinaryDecoder()
```

> Note: You may optionally pass your own userInfo `BinaryDecoder(userInfo:)` structure and it will be available to you during the decoding.

To decode, you pass the Type of object to create, and an instance of encoded data representing that type.
```Swift
   let employee = try decoder.decode(Employee.self, from: bytes)
```

### Encoded Data

The `BinaryEncoder.encode` method returns type `Array<UInt8>` (likewise `BinaryDecoder.decode` accepts an `Array<UInt8>` instance).

`[Array<UInt8>` is easily converted to other types such as `Swift.Data` for passing to Foundation methods to store and load data from file.
```Swift
   let bytes = try encoder.encode(employee)

   // Write the bytes directly to a file.
   FileManager.default.createFile(atPath: "employee.bin", contents: Data(bytes))
```

## Sources and Binaries

You can find the latest sources and binaries on [github](https://github.com/stickytools/sticky-encoding).

## Communication and Contributions

- If you **found a bug**, _and can provide steps to reliably reproduce it_, [open an issue](https://github.com/stickytools/sticky-encoding/issues).
- If you **have a feature request**, [open an issue](https://github.com/stickytools/sticky-encoding/issues).
- If you **want to contribute**
   - Fork it! [StickyEncoding repository](https://github.com/stickytools/sticky-encoding)
   - Create your feature branch: `git checkout -b my-new-feature`
   - Commit your changes: `git commit -am 'Add some feature'`
   - Push to the branch: `git push origin my-new-feature`
   - Submit a pull request :-)

> Note: for a instructions on how to build and test StickyEncoding for contributing please see the [Contributing Guide](CONTRIBUTING.md).

## Installation

### Swift Package Manager

**StickyEncoding** supports dependency management via Swift Package Manager on Darwin as well as Linux.

Please see [Swift Package Manager](https://swift.org/package-manager/#conceptual-overview) for further information.

### CocoaPods

StickyEncoding is available through [CocoaPods](http://cocoapods.org). To install it, simply add the following line to your Podfile:

```ruby
   pod "StickyEncoding"
```
## Minimum Requirements

Build Environment

| Platform | Swift | Swift Build | Xcode |
|:--------:|:-----:|:----------:|:------:|
| Linux    | 4.2 | &#x2714; | &#x2718; |
| OSX      | 4.2 | &#x2714; | Xcode 10.2 |

Minimum Runtime Version

| iOS |  OS X | tvOS | watchOS | Linux |
|:---:|:-----:|:----:|:-------:|:------------:|
| 8.0 | 10.10 | 9.0  |   2.0   | Ubuntu 14.04, 16.04, 16.10 |

> **Note:**
>
> To build and run on **Linux** we have a a preconfigure **Vagrant** file located at [https://github.com/tonystone/vagrant-swift](https://github.com/tonystone/vagrant-swift)
>
> See the [README](https://github.com/tonystone/vagrant-swift/blob/master/README.md) for instructions.
>

## Author

Tony Stone ([https://github.com/tonystone](https://github.com/tonystone))

## License

StickyEncoding is released under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)
