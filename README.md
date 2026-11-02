# macOS PDF text and metadata

`Import pdfkit`. `New PDFReader(file)` opens an existing local PDF. Read `PageCount`, `IsLocked`, `IsEncrypted`; use `PageText(zeroBasedIndex)` and `Metadata(key)` (for example `"Title"`). `Unlock(password)` explicitly attempts a password; passwords are neither saved nor logged. `Close()` is final/idempotent. Empty text can mean a scanned page: OCR is not provided. Use a reader on one thread at a time and keep it open while reading.

These native operations require macOS; `PDFKitSupported()` returns False on Windows/Linux, and unsupported operations throw rather than silently emulating an Apple API. All six compiler targets are checked; native execution is verified on macOS arm64.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add pdfkit --git https://github.com/BuoyBay/pdfkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Platform and scope

Native PDF operations require macOS. Check `PDFKitSupported()` on other targets. Text extraction does not perform OCR.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer pdfkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
