---
title: "Style Guide"
weight: 50
toc_hide: false
linkTitle: "Style Guide"
no_list: "true"
type: docs
description: "This topic provides direction for how best to stucture your proto definitions."
---

This document provides a style guide for `.proto` files. By following these
conventions, you'll make your protocol buffer message definitions and their
corresponding classes consistent and easy to read.

Note that protocol buffer style has evolved over time, so it is likely that you
will see `.proto` files written in different conventions or styles. **Respect
the existing style** when you modify these files. **Consistency is key**.
However, it is best to adopt the current best style when you are creating a new
`.proto` file.

## Standard File Formatting {#standard-file-formatting}

*   Keep the line length to 80 characters.
*   Use an indent of 2 spaces.
*   Prefer the use of double quotes for strings.

## File Structure {#file-structure}

Files should be named `lower_snake_case.proto`.

All files should be ordered in the following manner:

1.  License header (if applicable)
1.  File overview
1.  Syntax
1.  Package
1.  Imports (sorted)
1.  File options
1.  Everything else

## Packages {#packages}

Package names should be in lowercase. Package names should have unique names
based on the project name, and possibly based on the path of the file containing
the protocol buffer type definitions.

## Message and Field Names {#message-field-names}

Use PascalCase (with an initial capital) for message names – for example,
`SongServerRequest`. Use lower_snake_case for field names (including oneof field
and extension names) – for example, `song_name`.

```proto
message SongServerRequest {
  optional string song_name = 1;
}
```

Using this naming convention for field names gives you accessors like those
shown in the the following two code samples.

C++:

```cpp
const string& song_name() { ... }
void set_song_name(const string& x) { ... }
```

Java:

```java
public String getSongName() { ... }
public Builder setSongName(String v) { ... }
```

If your field name contains a number, the number should appear after the letter
instead of after the underscore. For example, use `song_name1` instead of
`song_name_1`

## Repeated Fields {#repeated-fields}

Use pluralized names for repeated fields.

```proto
repeated string keys = 1;
  ...
  repeated MyMessage accounts = 17;
```

## Enums {#enums}

Use PascalCase (with an initial capital) for enum type names and
CAPITALS_WITH_UNDERSCORES for value names:

```proto
enum FooBar {
  FOO_BAR_UNSPECIFIED = 0;
  FOO_BAR_FIRST_VALUE = 1;
  FOO_BAR_SECOND_VALUE = 2;
}
```

Each enum value should end with a semicolon, not a comma. Prefer prefixing enum
values instead of surrounding them in an enclosing message. The zero value enum
should have the suffix `UNSPECIFIED`, because a server or application that gets
an unexpected enum value will mark the field as unset in the proto instance. The
field accessor will then return the default value, which for enum fields is the
first enum value.

## Services {#services}

If your `.proto` defines an RPC service, you should use PascalCase (with an
initial capital) for both the service name and any RPC method names:

```proto
service FooService {
  rpc GetSomething(GetSomethingRequest) returns (GetSomethingResponse);
  rpc ListSomething(ListSomethingRequest) returns (ListSomethingResponse);
}
```

## Things to Avoid {#avoid}

*   Required fields (only for proto2)
*   Groups (only for proto2)
