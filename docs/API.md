# PDF reading · 0.1.0

`Import pdfkit`. `New PDFReader(file)` opens an existing local PDF. Read `PageCount`, `IsLocked`, `IsEncrypted`; use `PageText(zeroBasedIndex)` and `Metadata(key)` (for example `"Title"`). `Unlock(password)` explicitly attempts a password; passwords are neither saved nor logged. `Close()` is final/idempotent. Empty text can mean a scanned page: OCR is not provided. Use a reader on one thread at a time and keep it open while reading.

These native operations require macOS; `PDFKitSupported()` returns False on Windows/Linux, and unsupported operations throw rather than silently emulating an Apple API. All six compiler targets are checked; native execution is verified on macOS arm64.

Maintainers run the private validation suite before release. See the repository README for public build instructions.

Inspired by [macoslib’s Cocoa examples](https://github.com/macoslib/macoslib); implemented independently against [Apple’s API](https://developer.apple.com/documentation/pdfkit/pdfdocument).
