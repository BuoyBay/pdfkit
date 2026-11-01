---
title: "pdfkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["PDFReader"]
dependencies: []
symbols: ["PDFReader"]
related: ["api.md", "getting-started.md", "index.md"]
---

# pdfkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## PDFKit functions

### PDFKitSupported

`Public Function PDFKitSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## PDFReader

`Public Class PDFReader`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `PageCount` | `Integer` | Yes | No | — | — |
| `IsLocked` | `Boolean` | Yes | No | — | — |
| `IsEncrypted` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(file As FileSystemItem)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `file` | `FileSystemItem` | `ByVal` | Required |

Returns: no value.

### Unlock

`Public Function Unlock(password As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `password` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### PageText

`Public Function PageText(index As Integer) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### Metadata

`Public Function Metadata(key As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
