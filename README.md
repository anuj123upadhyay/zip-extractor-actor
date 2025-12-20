# ZIP Download & Extraction Scraper | Fast, Reliable & Secure

> **Download ZIP files from URLs and automatically extract their contents with advanced features like retry logic, password protection, duplicate handling, and real-time progress tracking.**

---

## 🚀 What This Actor Does

The **ZIP Download & Extraction Scraper** is a production-ready Python Actor that downloads ZIP files from any URL and extracts their contents with enterprise-grade reliability. Perfect for automating data extraction, bulk file processing, and data pipelines that require downloading and unarchiving files at scale.

### Key Capabilities:
- ✅ **Download any ZIP file** from a URL with automatic retry logic
- ✅ **Extract all files** with folder structure preservation
- ✅ **Password-protected ZIPs** - decrypt encrypted archives with ease
- ✅ **Real-time progress tracking** - monitor downloads and extractions as they happen
- ✅ **Duplicate handling** - rename, skip, or overwrite duplicate files
- ✅ **Security features** - path traversal protection and ZIP integrity validation
- ✅ **Flexible output** - keep or delete temporary files based on your needs
- ✅ **Comprehensive error reporting** - detailed logs and error tracking

---

## 💡 Why Choose This Actor?

### **Reliability First**
- Automatic retry logic with exponential backoff for failed downloads
- ZIP integrity validation before and after extraction
- Comprehensive error handling for corrupted files
- Support for password-protected and encrypted archives

### **Built for Scale**
- Process multiple ZIP files in a single run
- Configurable timeout limits and file size constraints
- Memory-efficient chunked downloads (8KB chunks)
- Real-time progress updates for monitoring long-running jobs

### **Developer Friendly**
- Simple JSON input schema - just provide URLs
- Detailed JSON output with file manifests
- Clear error messages and troubleshooting info
- Fully documented input/output specifications

### **Enterprise Ready**
- Built on [Apify SDK for Python](https://docs.apify.com/sdk/python/)
- Automatic scheduling & monitoring on Apify platform
- Proxy rotation support
- API access for programmatic control

---

## 📋 Input & Output

### Input Schema

```json
{
  "urls": ["https://example.com/archive.zip"],
  "extract_to_memory": false,
  "keep_zip": false,
  "password": null,
  "handle_duplicates": "rename",
  "timeout": 300
}
```

| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `urls` | String or Array | ✅ Yes | Single URL or array of ZIP file URLs | — |
| `extract_to_memory` | Boolean | No | Delete extracted files after processing | `false` |
| `keep_zip` | Boolean | No | Retain downloaded ZIP file | `false` |
| `password` | String | No | Password for encrypted ZIPs | `null` |
| `handle_duplicates` | String | No | How to handle file conflicts: `rename`, `skip`, or `overwrite` | `rename` |
| `timeout` | Number | No | Download timeout in seconds | `300` |

### Sample Input

```json
{
  "urls": [
    "https://example.com/data.zip",
    "https://example.com/backup.zip"
  ],
  "extract_to_memory": false,
  "keep_zip": false,
  "password": null,
  "handle_duplicates": "rename",
  "timeout": 300
}
```

### Output Schema

Each processed ZIP generates a detailed JSON output:

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
    },
    {
      "path": "image.jpg",
      "size": 2097152,
      "type": ".jpg",
      "modified": "2024-12-20T15:25:00"
    }
  ],
  "skipped_files": 0,
  "corrupted_files": 0,
  "timestamp": "2024-12-20T15:35:00"
}
```

### Summary Output

After processing all URLs, you receive a comprehensive summary:

```json
{
  "type": "summary",
  "total_urls_processed": 2,
  "successful_extractions": 2,
  "failed_extractions": 0,
  "total_bytes_downloaded": 10485760,
  "total_files_extracted": 87,
  "total_skipped_files": 0,
  "total_corrupted_files": 0,
  "total_errors": 0,
  "processing_duration_seconds": 25.67,
  "timestamp": "2024-12-20T15:35:00"
}
```

---

## 🎯 Use Cases

### **Data Extraction & ETL Pipelines**
Automatically download and extract data files (CSV, JSON, Parquet) from scheduled backups or API responses.

### **Backup & Disaster Recovery**
Process bulk backup archives and restore files to your storage systems.

### **Web Scraping Workflows**
Extract downloadable content from websites in batch processes.

### **Document Processing**
Extract PDFs, images, and documents from archived sources for further processing.

### **Database Dumps**
Handle large database export archives with automatic decompression.

### **Media Asset Management**
Process bulk media files from archived sources efficiently.

---

## 🚀 Getting Started

### Option 1: Run Directly on Apify Platform

1. **Open this Actor** in your Apify console
2. **Provide your ZIP URLs** in the input field
3. **Click Run** and monitor progress in real-time
4. **Download results** from the Dataset tab

### Option 2: Run Locally

```bash
# Install Apify CLI
npm install -g apify-cli

# Create a local copy of this Actor
apify clone [actor-id]

# Install dependencies
pip install -r requirements.txt

# Run locally
apify run
```

### Option 3: Use Apify API

```bash
# Trigger the Actor via API
curl -X POST https://api.apify.com/v2/acts/[actor-id]/runs \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "urls": ["https://example.com/file.zip"]
  }'
```

<!-- ---

## 📊 Cost & Performance

### **Typical Processing Costs**

| Scenario | Dataset Items | Actor Compute | Estimated Cost |
|----------|---------------|---------------|-----------------|
| Single 50MB ZIP | 1 + summary | ~15 seconds | ~$0.02 |
| 10 ZIPs (500MB total) | 10 + summary | ~120 seconds | ~$0.15 |
| 100 ZIPs (5GB total) | 100 + summary | ~1200 seconds | ~$1.50 |

**Pricing breakdown:**
- Free plan includes 5 free Actor runs per month
- Paid plans start at $9/month with volume discounts
- Compute costs: ~$0.25 per 1000 compute units (1 unit = 1 second)

### **Performance Benchmarks**

- **Download Speed**: Limited by your source server and network (typically 10-100 Mbps)
- **Extraction Speed**: ~50-200 files per second depending on file size
- **Memory Usage**: Optimized for files up to 10GB (configurable)

--- -->

## 🔧 Advanced Features

### **Retry Logic with Exponential Backoff**
Automatically retries failed downloads with intelligent backoff (2s, 4s, 8s...) before giving up.

### **ZIP Integrity Validation**
Verifies ZIP file integrity before extraction to detect corrupted archives early.

### **Path Traversal Protection**
Prevents malicious ZIPs from writing files outside the extraction directory.

### **Smart Duplicate Handling**
- **rename**: Appends suffix (file_1.txt, file_2.txt)
- **skip**: Leaves existing files untouched
- **overwrite**: Replaces existing files

### **Password-Protected Archives**
Seamlessly handles encrypted ZIPs with password support.

### **Real-Time Progress Tracking**
Monitor extraction progress in real-time with detailed breakdowns (10% increments).

---

## ⚙️ Configuration Examples

### Example 1: Simple Single ZIP
```json
{
  "urls": "https://example.com/data.zip"
}
```

### Example 2: Batch Processing with Cleanup
```json
{
  "urls": [
    "https://example.com/backup1.zip",
    "https://example.com/backup2.zip",
    "https://example.com/backup3.zip"
  ],
  "extract_to_memory": true,
  "keep_zip": false
}
```

### Example 3: Password-Protected Archives
```json
{
  "urls": "https://example.com/secure-archive.zip",
  "password": "your-password-here",
  "keep_zip": true
}
```

### Example 4: Smart Duplicate Handling
```json
{
  "urls": ["https://example.com/archive1.zip", "https://example.com/archive2.zip"],
  "handle_duplicates": "rename",
  "timeout": 600
}
```

---

## 🛠️ Troubleshooting

### "HTTP 404 for URL"
**Problem**: The URL is not found  
**Solution**: Verify the ZIP file URL is correct and accessible. Test it in your browser first.

### "Timeout downloading"
**Problem**: Download took too long  
**Solution**: Increase the `timeout` parameter (default: 300 seconds). For large files, try 600+ seconds.

### "Bad password for encrypted file"
**Problem**: Incorrect password provided  
**Solution**: Verify the password is correct. Note: Passwords are case-sensitive.

### "Invalid or corrupted zip file"
**Problem**: ZIP file is damaged or not a valid ZIP  
**Solution**: Download and test the ZIP file locally. Re-upload if the source file is corrupted.

### "Extraction size exceeds limit"
**Problem**: ZIP is larger than 10GB  
**Solution**: Contact support for custom size limit configuration.

---

## 📞 Support & Issues

### Getting Help
- **Issues Tab**: Report bugs or request features in the [Issues section](https://github.com/your-repo/issues)
- **Email**: [support@example.com](mailto:support@example.com)
- **Discord**: Join the [Apify Developer Community](https://discord.com/invite/jyEM2PRvMU)

### Reporting Bugs
Include:
1. The exact URL you're trying to process
2. Error message from the output
3. File size and expected file count
4. Steps to reproduce

### Feature Requests
Suggest new features in the Issues tab. Popular requests include:
- Support for other archive formats (7z, rar, tar.gz)
- Automatic content scanning/validation
- File filtering during extraction

---

## 🔗 Integrations & Workflows

This Actor works seamlessly with:
- **[Zapier](https://zapier.com/)** - Trigger downloads from webhooks
- **[Make/Integromat](https://www.make.com/)** - Complex automation workflows
- **[GitHub Actions](https://github.com/features/actions)** - CI/CD pipelines
- **[Google Drive](https://www.google.com/drive/)** - Store extracted files
- **[Slack](https://slack.com/)** - Send notifications on completion

Example Make workflow:
```
Webhook (trigger) → ZIP Download Actor (extract) → Google Drive (save) → Slack (notify)
```

---

## 📚 Learn More

- **[Apify SDK Python Docs](https://docs.apify.com/sdk/python)** - Complete API reference
- **[Python Tutorials](https://docs.apify.com/academy/python)** - Step-by-step guides
- **[Apify Platform Guide](https://docs.apify.com/platform)** - Platform features overview
- **[Request Queues](https://docs.apify.com/sdk/python/docs/concepts/storages)** - Data storage docs
- **[Scheduling & Monitoring](https://docs.apify.com/platform/actors/publishing/task)** - Automate runs

---

## 📄 Legal & Terms

- **License**: [MIT](LICENSE)
- **Privacy**: No data is stored or logged beyond what Apify's platform tracks
- **Security**: ZIP files are extracted in isolated temporary directories
- **Disclaimer**: Users are responsible for respecting intellectual property rights when downloading files

---

## 🤝 Contributing

Found a bug or want to improve this Actor? Contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

---

## 🎉 Recent Updates

- ✨ **v1.0.0** - Initial release
- 🐛 Bug fixes for corrupted ZIP handling
- ⚡ Performance improvements for large file extraction
- 🔒 Enhanced security with path traversal protection

---

**Built with ❤️ for the Apify community**

*Last updated: December 2024 | Questions? Open an issue or reach out to support.*
