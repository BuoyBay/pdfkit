---
title: "PDF reading"
summary: "Read PDF page text and metadata with an explicitly owned native reader."
category: "Overview"
order: 0
keywords: ["pdfkit", "macOS", "native"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# PDF reading

Use `pdfkit` for existing local PDFs: count pages, inspect encryption state, read embedded text, and obtain string metadata. This package is a reader, not a PDF generator or OCR engine.

## Platform availability

Native PDFKit operations require macOS. `PDFKitSupported()` is false on Windows and Linux; reader construction throws `UnsupportedOperationException` there.

## Package use

Install `pdfkit-0.1.0.buipkg` in the consumer project's `packages/` directory, then use `Import pdfkit`. This package is independently sealed; it does not require importing the other desktop integration packages.

## Behavior and lifetime

Nil paths, nonexistent or unreadable PDFs, out-of-range page indices, locked text access, and reads after close raise `InvalidArgumentException`. Page indices start at zero. Empty page text may indicate a scanned image page; no OCR is performed. Missing or non-string metadata returns an empty string. Close is final and idempotent; destruction also closes the reader. Passwords are not retained or logged by this package.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
