# 📦 ZIP Download & Extraction Actor

**The most efficient, reliable, and developer-friendly ZIP extraction solution on Apify**

---

## 🌟 Why Choose This Actor?

The ZIP Download & Extraction Actor delivers enterprise-grade performance with these advanced capabilities:

**Performance & Reliability:** Built optimized for high-throughput processing with intelligent retry logic and exponential backoff handling.

**Cost-Effective:** Pay-per-use model with no monthly rentals. Scale up or down based on your actual needs without being locked into expensive subscriptions.

**Lightning-Fast Extraction:** Download and extract ZIP files from any URL with blazing-fast performance. Process gigabytes of archived data in seconds, not minutes, with intelligent chunking and optimization.

**Precision Targeting & Advanced Filtering:** Extract only what you need with file type filtering, password protection support, and smart duplicate handling. Get precisely the files you need, when you need them.

**Rich, Structured Metadata:** Extract complete file manifests including paths, sizes, types, and timestamps. Our advanced parsing ensures you get clean, structured data ready for immediate use.

**Enterprise-Grade Configuration & Flexibility:** Built for developers and businesses who demand reliability. Highly configurable with intuitive controls, comprehensive error handling, and robust logging. Focus on your business logic while we handle the complexity of ZIP extraction.

**No Hidden Costs:** We do not charge monthly rentals. Our actor operates on a transparent pay-per-use model based on compute units consumed.

---

## 🚀 Features

### Core Capabilities
- **Universal ZIP Support:** Download from any accessible URL with automatic retry logic
- **Password Protection:** Full support for encrypted archives (PKWARE, AES-128/192/256)
- **Batch Processing:** Process multiple ZIP files in a single run
- **Smart Pagination:** Automatic handling of large archives with progress tracking
- **File Type Filtering:** Extract only specific file extensions to save time and storage

### Data Quality
- **Clean Output:** Structured JSON metadata for production-ready integration
- **Integrity Validation:** CRC checksum verification and ZIP structure validation
- **Path Security:** Built-in path traversal protection against malicious archives
- **Detailed Manifests:** Complete file metadata including size, type, and timestamps
- **Summary Reports:** Comprehensive processing statistics and error tracking

---

## 📖 Usage Examples

### Basic Extraction Example
Extract a single ZIP file with default settings.

```json
{
  "urls": [
    {"url": "https://example.com/archive.zip"}
  ]
}
```

### Advanced Extraction Example
Batch process multiple password-protected ZIPs with file filtering and custom timeout.

```json
{
  "urls": [
    {"url": "https://example.com/backup1.zip"},
    {"url": "https://example.com/backup2.zip"},
    {"url": "https://example.com/backup3.zip"}
  ],
  "password": "MySecurePassword",
  "file_type_filter": "pdf,docx,xlsx",
  "handle_duplicates": "rename",
  "timeout": 600,
  "keep_zip": false
}
```

### Memory-Only Processing Example
Extract metadata without storing files (perfect for inventory/audit).

```json
{
  "urls": [
    {"url": "https://example.com/large-archive.zip"}
  ],
  "extract_to_memory": true,
  "file_type_filter": "csv,json"
}
```

---

## 🔍 Input Configuration

### Input Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `urls` | Array | ✅ | Sample ZIP | Array of URL objects: `[{"url": "https://..."}]` |
| `extract_to_memory` | Boolean | ❌ | `false` | Delete files after processing (metadata only mode) |
| `keep_zip` | Boolean | ❌ | `false` | Retain downloaded ZIP file after extraction |
| `password` | String | ❌ | `null` | Password for encrypted archives |
| `handle_duplicates` | String | ❌ | `"rename"` | Strategy: `rename` \| `skip` \| `overwrite` |
| `timeout` | Number | ❌ | `300` | Download timeout in seconds |
| `file_type_filter` | String | ❌ | `""` | Comma-separated extensions (e.g., `"pdf,jpg,png"`) |

### Duplicate Handling Strategies

| Strategy | Behavior | Example |
|----------|----------|---------|
| **`rename`** | Appends numeric suffix | `file.txt` → `file_1.txt`, `file_2.txt` |
| **`skip`** | Keeps first occurrence | First `file.txt` kept, others ignored |
| **`overwrite`** | Keeps last occurrence | Latest `file.txt` overwrites previous |

---

## 📊 Output Format

### Individual ZIP Result Structure

```json
{
  "success": true,
  "url": "https://example.com/archive.zip",
  "filename": "archive.zip",
  "files_extracted": 42,
  "bytes_downloaded": 5242880,
  "processing_time_seconds": 12.34,
  "extracted_files": [
    {
      "path": "subfolder/document.pdf",
      "size": 1048576,
      "type": ".pdf",
      "modified": "2024-12-20T15:30:00"
    }
  ],
  "skipped_files": 0,
  "corrupted_files": 0,
  "timestamp": "2024-12-20T15:35:00"
}
```

### Summary Report Structure

```json
{
  "report_type": "summary",
  "total_urls_processed": 5,
  "successful_extractions": 4,
  "failed_extractions": 1,
  "total_bytes_downloaded": 52428800,
  "total_files_extracted": 215,
  "total_skipped_files": 3,
  "total_corrupted_files": 0,
  "total_errors": 1,
  "processing_duration_seconds": 67.89,
  "timestamp": "2024-12-27T10:30:00Z"
}
```

### Error Output Structure

```json
{
  "success": false,
  "url": "https://example.com/broken.zip",
  "error": "Invalid or corrupted zip file",
  "error_type": "BadZipFile",
  "timestamp": "2024-12-27T10:30:00Z"
}
```

---

## 🎯 Use Cases

### 📊 Data Extraction & ETL Pipelines
Automate extraction of data files (CSV, JSON, Parquet) from scheduled backups, API downloads, and database exports. **Benefits:** Eliminate manual steps, schedule automated ingestion, integrate seamlessly with data workflows.

### 💾 Backup & Disaster Recovery
Process bulk backup archives for cloud restoration, integrity validation, and selective file recovery. **Benefits:** Rapid disaster recovery, automated testing, selective restoration.

### 🌐 Web Scraping Workflows
Extract downloadable content from websites including bulk documents, archives, and datasets. **Benefits:** Automate repetitive downloads, process batches overnight, chain with other Apify actors.

### 📄 Document Processing
Extract and process documents at scale: PDF archives, image collections, invoices, and legal documents. **Benefits:** Batch processing, automated categorization, OCR/AI integration ready.

### 🗄️ Database Dumps
Handle large database export archives: SQL dumps, MongoDB exports, PostgreSQL/MySQL backups. **Benefits:** Automated decompression, GB+ file support, enterprise reliability.

### 🎬 Media Asset Management
Process bulk media archives: photo galleries, video collections, audio libraries, design packages. **Benefits:** Fast large-file extraction, type filtering, organized structure.

---

## 🔧 Advanced Features

### 🔄 Automatic Retry with Exponential Backoff
Failed downloads automatically retry with increasing wait times (2s → 4s → 8s → 16s). Maximum 3 attempts before marking as failed. Handles temporary network issues gracefully.

### ✅ ZIP Integrity Validation
Multi-stage verification: pre-extraction structure checks, CRC checksum validation, size verification, and early corruption detection.

### 🛡️ Path Traversal Protection
Security features prevent malicious ZIPs from writing outside extraction directory. Blocks `../` patterns, absolute paths, and sanitizes all filenames.

### 🔐 Password-Protected Archives
Supports Traditional PKWARE, AES-128, AES-192, and AES-256 encryption. Simply provide the password in input configuration.

### 📊 Real-Time Progress Tracking
Monitor extraction with detailed breakdowns: download progress with speed metrics, extraction progress every 10%, file counts, and error notifications.

### 🗂️ File Type Filtering
Extract only specific file types to save time and storage. Supports any file extension. **Benefits:** Faster processing, reduced storage, focused extraction.

---

## 🛠️ Troubleshooting

### ❌ "HTTP 404: URL not found"
**Problem:** ZIP file URL returns 404 error  
**Solution:** Verify URL accessibility, test in browser, check authentication requirements, ensure direct ZIP link (not download page)

### ⏱️ "Timeout downloading ZIP"
**Problem:** Download exceeded timeout limit  
**Solution:** Increase `timeout` parameter (default: 300s). For files >500MB, try `timeout: 900` or higher. Check network stability.

### 🔐 "Bad password for encrypted file"
**Problem:** Incorrect password provided  
**Solution:** Verify case-sensitive password, check for spaces, ensure supported encryption (PKWARE/AES), test locally first.

### 🗜️ "Invalid or corrupted ZIP file"
**Problem:** ZIP file damaged or invalid  
**Solution:** Download locally and verify, check with `unzip -t`, ensure complete download, verify actual ZIP content (not HTML error).

### 📏 "Extraction size exceeds limit"
**Problem:** Extracted content exceeds size limits  
**Solution:** Use `file_type_filter` for selective extraction, enable `extract_to_memory` for metadata-only, split large archives, contact support for limits.

### 🔄 "Multiple extraction failures"
**Problem:** Several ZIPs failing extraction  
**Solution:** Check Actor logs for errors, verify URL accessibility, test single known-good ZIP first, ensure storage space, check network connectivity.

---

## 💬 Support & Community

### 🐛 Report Bugs
Found a bug? [Create an issue](https://github.com/anuj123upadhyay/zip-extractor-actor/issues)

**Please include:** ZIP URL, complete error message, expected vs actual behavior, file size/count, input configuration JSON

### 💡 Request Features
Have an idea? [Submit a feature request](https://github.com/anuj123upadhyay/zip-extractor-actor/issues)

**Popular requests:** 7z/rar/tar.gz support, cloud storage integration, content scanning, regex filtering, enhanced analytics

### 📚 Documentation & Resources
- [Apify SDK Python Documentation](https://docs.apify.com/sdk/python)
- [Apify Academy - Python Tutorials](https://docs.apify.com/academy/python)
- [Apify Platform Guide](https://docs.apify.com/platform)
- [Data Storage Documentation](https://docs.apify.com/sdk/python/docs/concepts/storages)
- [Scheduling & Monitoring](https://docs.apify.com/platform/actors/running/tasks-and-schedules)

### 👥 Community Support
- 💬 [Apify Discord Server](https://discord.com/invite/jyEM2PRvMU)
- 🐦 [Twitter/X: @apify](https://twitter.com/apify)
- 📧 Email: support@apify.com

---


### Performance Benchmarks

**Download:** Network limited (10-100 Mbps), 8KB chunked, automatic retry, parallel processing  
**Extraction:** ~50-200 files/second, SSD-backed, optimized for bulk operations  
**Resources:** ~256MB base + file sizes, temporary storage, low-moderate CPU, bandwidth dependent  
**Scalability:** Process 1000+ files/run, handle multi-GB archives, concurrent processing, automatic management

### Optimization Tips
1. Use file type filtering to extract only needed files
2. Enable `extract_to_memory` for metadata-only mode
3. Batch multiple URLs in single run for efficiency
4. Increase timeout for large files to avoid re-runs
5. Use appropriate duplicate strategy to minimize processing

---

## 📄 License & Legal

### License
This Actor is licensed under the [MIT License](LICENSE) - free for commercial and personal use.

### Privacy & Security
**Data Handling:** No ZIP content logged/stored, isolated temporary processing, extracted files deleted after run, only metadata saved to datasets.

**Security:** Path traversal protection, ZIP bomb protection, CRC validation, isolated execution, no external transmission.

**Platform:** SOC 2 Type II, GDPR compliant, ISO 27001 certified, regular security audits.

[Read Apify Security Documentation](https://docs.apify.com/platform/security)

### Legal Disclaimer
You are responsible for content you download/extract. Respect intellectual property rights, ensure access permissions, comply with source website terms, use only for lawful purposes. Tool provided "as-is" without warranty.

### Responsible Use
**✅ Do:** Extract permitted files, legitimate automation, respect rate limits, comply with laws  
**❌ Don't:** Download copyrighted content without permission, bypass access controls, overload servers, malicious use

---

## 🤝 Contributing

We welcome contributions! Report bugs, suggest features, submit code improvements.

**Quick Start:**
1. Fork repository: `git clone https://github.com/anuj123upadhyay/zip-extractor-actor.git`
2. Create branch: `git checkout -b feature/your-feature-name`
3. Make changes (follow code style, add tests, update docs)
4. Test locally: `apify run`
5. Submit pull request with clear description

**Other ways to help:** Fix documentation typos, add usage examples, translate content, create tutorials, star repository, share with others.

---

## 📝 Changelog

### v1.0 (Current - December 2024)

**🎉 Initial Release**
- ZIP download and extraction functionality
- Password-protected archive support
- Multiple URL batch processing
- Smart duplicate file handling
- File type filtering
- Real-time progress tracking
- Comprehensive error handling
- Detailed output manifests

**🐛 Bug Fixes:** URL extraction from `requestListSources`, empty input handling, version format compatibility, improved retry logic

**🔒 Security:** Path traversal protection, ZIP integrity validation, CRC verification, enhanced error reporting

**⚡ Performance:** Optimized Docker image (Python 3.11), memory-efficient downloads, faster extraction, reduced footprint

### Upcoming Features (Roadmap)
- Support for 7z, tar.gz, rar formats
- Direct cloud storage integration (S3, GCS, Azure)
- Content validation and virus scanning
- Advanced regex filtering
- Enhanced analytics and reporting
- Incremental extraction support

---

## 🎉 Ready to Get Started?

**Check out the [Github repo](https://github.com/anuj123upadhyay/zip-extractor-actor) for quickstart examples and advanced configurations.**

---

**Made with ❤️ for the Apify community**

*Transform your ZIP extraction workflows with the most reliable and efficient solution on the market. Last Updated: 2024.12.27*

[🚀 Run on Apify](https://console.apify.com/) · [⭐ Star on GitHub](https://github.com/anuj123upadhyay/zip-extractor-actor) · [💬 Get Support](https://github.com/anuj123upadhyay/zip-extractor-actor/issues)