<div align="center">

<img src="media/logo.png?raw=true" alt="Safetar logo" width="400"/>

![Node](https://img.shields.io/badge/Bash-000000?style=for-the-badge&logo=gnubash&logoColor=white)

</div>

# Safetar - Secure Archiver with Integrity Check

**Safetar** is a high-performance Bash utility for creating compressed archives with built-in integrity verification. It leverages parallel compression and provides multiple verification modes to ensure data integrity.

## ✨ Features

- **🚀 Fast Parallel Compression**: Uses `pigz` for multi-threaded gzip compression
- **📊 Real-time Progress**: Visual progress bars for compression and verification
- **✅ Integrity Verification**: Two verification modes:
  - **Quick Check**: Fast gzip test for basic validation
  - **Paranoid Mode**: Byte-by-byte diff comparison for maximum safety
- **🎨 Beautiful CLI**: Colored output with ASCII art and formatted boxes
- **🔄 Smart Overwrite Protection**: Prompts before overwriting existing archives
- **🖥️ Cross-Platform**: Works on macOS and Linux

## 📋 Requirements

The following dependencies are required:

- `pigz` - Parallel implementation of gzip
- `pv` - Pipe Viewer for progress monitoring
- `gtar` - GNU tar (on macOS, BSD tar on Linux)

## 🚀 Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd Safetar
```

2. Make the script executable:
```bash
chmod +x src/safetar
```

3. Optionally, symlink to your PATH:
```bash
ln -s "$(pwd)/src/safetar" /usr/local/bin/safetar
```

4. Install dependencies (macOS):
```bash
brew install pigz pv gnu-tar
```

## 📖 Usage

### Basic Syntax

```bash
safetar <folder> [options]
```

### Options

| Option | Description |
|--------|-------------|
| `-c, --check` | Perform quick integrity check after compression |
| `-p, --paranoid` | Perform thorough byte-by-byte verification |
| `-f, --force` | Overwrite existing archive without prompt |
| `-h, --help` | Display help message |

### Examples

**Standard compression:**
```bash
safetar my-folder
```

**With quick integrity check:**
```bash
safetar my-folder --check
```

**With paranoid verification:**
```bash
safetar my-folder --paranoid
```

**Force overwrite:**
```bash
safetar my-folder --force
```

## 🎯 Verification Modes

### Standard Mode
Creates a compressed `.tar.gz` archive without verification. Fast and suitable when integrity checking is not critical.

### Quick Check Mode (`--check`)
After compression, performs a gzip test to verify the archive can be decompressed. Quick validation of archive integrity.

### Paranoid Mode (`--paranoid`)
Performs a complete byte-by-byte comparison between the source folder and the decompressed archive content. Ensures absolute data integrity but takes longer.

## 🔧 How It Works

1. **Source Analysis**: Calculates folder size for progress tracking
2. **Compression**: Uses `tar` + `pigz -9` for maximum compression with parallel processing
3. **Progress Display**: Real-time progress bar shows compression status
4. **Verification** (optional): Tests archive integrity based on selected mode
5. **Result**: Outputs `.tar.gz` file in current directory

## 🎨 Output Example

```
┌────────────────────────────────────┐
│   SAFETAR Secure Archiver          │
├────────────────────────────────────┤
│ Output : my-folder.tar.gz          │
│ Mode   : Paranoid (Diff)           │
└────────────────────────────────────┘

Compressing :  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100%
Verifying   :  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100%

✔ Archive created successfully.
```

## 📊 Performance

Safetar uses parallel compression via `pigz`, which can significantly speed up compression on multi-core systems. The number of threads is automatically detected based on your CPU.

## ⚠️ Notes

- Archives are created in the current working directory
- The script automatically handles macOS (uses `gtar`) and Linux (uses `tar`)
- Progress updates occur every 0.1 seconds for smooth display
- Paranoid mode requires more time but guarantees data integrity

## 🛠️ Technical Details

- **Version**: 1.0.0
- **Author**: Quentin Lamamy
- **Date**: 2026-01-06
- **Language**: Bash
- **Compression**: tar + pigz (gzip level 9)

## 📝 License

See LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.
