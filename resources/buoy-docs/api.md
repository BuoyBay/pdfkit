---
title: "PDF reading API"
summary: "Public pdfkit types and operations with behavior and lifetime notes."
category: "Reference"
order: 20
keywords: ["pdfkit", "API", "reference"]
symbols: ["PDFKitSupported", "PDFReader", "PDFReader.PageCount", "PDFReader.IsLocked", "PDFReader.IsEncrypted", "PDFReader.Unlock", "PDFReader.PageText", "PDFReader.Metadata", "PDFReader.Close"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

`Import pdfkit` exposes the following public API. Properties described as read-only have no public setter.

| Symbol | Behavior |
| --- | --- |
| `PDFKitSupported() As Boolean` | Reports native PDFKit availability. |
| `PDFReader(file As FileSystemItem)` | Open an existing local PDF; invalid input throws. |
| `PDFReader.PageCount As Integer` | Read-only number of pages; requires an open reader. |
| `PDFReader.IsLocked As Boolean` | Read-only current lock state. |
| `PDFReader.IsEncrypted As Boolean` | Read-only encryption state, independent of whether it is unlocked. |
| `PDFReader.Unlock(password As String) As Boolean` | Explicitly try a password and return whether unlocking succeeded. |
| `PDFReader.PageText(index As Integer) As String` | Read text from a zero-based page; locked or invalid indices throw. |
| `PDFReader.Metadata(key As String) As String` | Read a string attribute such as Title; missing/non-string attributes return an empty string. |
| `PDFReader.Close()` | Release the document; subsequent queries throw. Repeated closes are safe. |

## Errors and availability

Native PDFKit operations require macOS. `PDFKitSupported()` is false on Windows and Linux; reader construction throws `UnsupportedOperationException` there. Nil paths, nonexistent or unreadable PDFs, out-of-range page indices, locked text access, and reads after close raise `InvalidArgumentException`. Page indices start at zero. Empty page text may indicate a scanned image page; no OCR is performed. Missing or non-string metadata returns an empty string. Close is final and idempotent; destruction also closes the reader. Passwords are not retained or logged by this package.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
