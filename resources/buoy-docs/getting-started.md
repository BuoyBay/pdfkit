---
title: "PDF reading getting started"
summary: "Install and use pdfkit with an availability check and a complete example."
category: "Guides"
order: 10
keywords: ["pdfkit", "install", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

## Install and import

Copy the sealed `pdfkit-0.1.0.buipkg` archive into your application's `packages/` folder. To build it from this repository, run `python3 tools/build_integrations.py pdfkit`.

## First use

Create `PDFReader` from an existing `FileSystemItem`. Keep it open while querying pages or metadata, and use one thread at a time. Check `IsLocked` before text access. If needed, call `Unlock` with a user-supplied password and check its Boolean result. Always call `Close`, preferably in a `Finally` block.

```buoy
Import pdfkit

Sub Main(args As Array Of String)
    If Not PDFKitSupported() Then
        Print "PDF reading requires macOS."
        Return
    End If
    If args.Count = 0 Then
        Print "Pass a local PDF path."
        Return
    End If
    Dim reader As New PDFReader(New FileSystemItem(args(0)))
    Try
        If reader.IsLocked Then
            Print "The PDF must be unlocked before reading text."
        ElseIf reader.PageCount > 0 Then
            Print reader.PageText(0)
        End If
    Finally
        reader.Close()
    End Try
End Sub
```

The example checks backend availability before invoking macOS-only operations. It does not catch input or access failures; catch exceptions at your application boundary and present a useful message to the user.

## Platform and error handling

Native PDFKit operations require macOS. `PDFKitSupported()` is false on Windows and Linux; reader construction throws `UnsupportedOperationException` there. Nil paths, nonexistent or unreadable PDFs, out-of-range page indices, locked text access, and reads after close raise `InvalidArgumentException`. Page indices start at zero. Empty page text may indicate a scanned image page; no OCR is performed. Missing or non-string metadata returns an empty string. Close is final and idempotent; destruction also closes the reader. Passwords are not retained or logged by this package.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
