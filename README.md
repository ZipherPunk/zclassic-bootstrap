# Zclassic Bootstrap

Pre-synced blockchain data for fast Zclassic node setup.

## Latest Bootstrap

| Version | Block Height | Date | Size |
|---------|--------------|------|------|
| [v20260220](https://github.com/ZipherPunk/zclassic-bootstrap/releases/tag/v20260220) | 50 (estimated from files) | 2026-02-20 | 9.4G |

## Quick Start

### Using ZipherX Wallet (Recommended)
[ZipherX Wallet](https://github.com/ZipherPunk/ZipherX) can automatically download and install the bootstrap.

### Manual Installation

1. **Stop the daemon**
   ```bash
   zclassic-cli stop
   ```

2. **Download all parts** from the [latest release](https://github.com/ZipherPunk/zclassic-bootstrap/releases/latest)

3. **Merge and extract**
   ```bash
   cat zclassic-bootstrap-*.tar.zst.part* > bootstrap.tar.zst
   zstd -d bootstrap.tar.zst
   tar -xf bootstrap.tar
   ```

4. **Copy to Zclassic directory**
   ```bash
   # macOS
   cp -R zclassic-bootstrap-*/* ~/Library/Application\ Support/Zclassic/

   # Linux
   cp -R zclassic-bootstrap-*/* ~/.zclassic/
   ```

5. **Start the daemon**
   ```bash
   zclassicd -daemon
   ```

## Verification

Verify file integrity using checksums:
```bash
shasum -a 256 -c checksums.txt
```

## Requirements

- **zstd** for decompression: `brew install zstd` (macOS) or `apt install zstd` (Linux)
- ~10GB free disk space

## Links

- [Zclassic](https://zclassic.org)
- [ZipherX Wallet](https://github.com/ZipherPunk/ZipherX)
- [ZipherPunk](https://zipherpunk.com/)

---
*Created by [ZipherPunk](https://zipherpunk.com/)*
