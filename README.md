# Zclassic Bootstrap

Fast-sync your Zclassic node with pre-downloaded blockchain data.

> **DISCLAIMER**: This software and data are provided **"AS IS"**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. By downloading or using the bootstrap data, you acknowledge and agree that:
>
> - **USE AT YOUR OWN RISK.** The authors and contributors are not liable for any loss of funds, data corruption, or damages arising from the use of this software or data.
> - **ALWAYS VERIFY SHA256 CHECKSUMS** before extracting any downloaded file. Do not trust files that fail checksum verification.
> - **ALWAYS BACKUP `wallet.dat` BEFORE USING BOOTSTRAP.** Failure to do so may result in permanent, irreversible loss of funds.
> - **NO FINANCIAL ADVICE.** Nothing in this repository constitutes financial, investment, or legal advice. Cryptocurrency involves significant risk.
> - **NOT AUDITED.** The blockchain data in this bootstrap has not been independently audited. Use trusted sources only.
> - **STOP YOUR NODE** (`zclassicd`) before extracting bootstrap data. Extracting while the node is running will corrupt your database.
> - The bootstrap contains **publicly available blockchain data only** (blocks, UTXO set, index) — no private keys, seeds, or sensitive information are included.

## Current Bootstrap

- **Block Height**: 3017692
- **Date**: 2026-02-20
- **Total Size**: 9.4G (compressed)
- **Parts**: 10 files

## Zcash Parameters

Cryptographic parameters required by zclassicd for shielded transactions.

- **Release**: [zcash-params-v1](https://github.com/ZipherPunk/zclassic-bootstrap/releases/tag/zcash-params-v1)
- **Total Size**: 1.54 GB (compressed) / 1.69 GB (uncompressed)
- **Compression**: zstd level 19

### Files

| File | Size | Purpose |
|------|------|---------|
| sapling-spend.params |  46M | Prove shielded spends |
| sapling-output.params | 3.4M | Create shielded outputs |
| sprout-groth16.params | 692M | Legacy Sprout proofs |
| sprout-proving.key | 868M | Generate Sprout proofs |
| sprout-verifying.key | 4.0K | Verify Sprout proofs |

### Installation Location

- **macOS**: `~/Library/Application Support/ZcashParams/`
- **Linux**: `~/.zcash-params/`
- **Windows**: `%APPDATA%\ZcashParams\`

The ZipherX wallet automatically downloads and installs these parameters during bootstrap.

## Download

### Automatic (via ZipherX Wallet)
The ZipherX wallet will automatically download and install this bootstrap when needed.

### Manual Download

#### Option 1: Using GitHub CLI (Recommended)
```bash
# Download all parts from the latest release
gh release download --repo ZipherPunk/zclassic-bootstrap --pattern "*.part"
gh release download --repo ZipherPunk/zclassic-bootstrap --pattern "checksums.txt"

# Verify checksums
shasum -a 256 -c checksums.txt

# Combine parts
cat zclassic-bootstrap-20260220.tar.zst.part-*.part > zclassic-bootstrap.tar.zst
```

#### Option 2: Manual Download
1. Go to the [latest release](https://github.com/ZipherPunk/zclassic-bootstrap/releases/latest)
2. Download all `.part` files
3. Download `checksums.txt`
4. Verify checksums: `shasum -a 256 -c checksums.txt`
5. Combine parts: `cat zclassic-bootstrap-20260220.tar.zst.part-*.part > zclassic-bootstrap.tar.zst`

## Installation

### macOS
```bash
# Stop zclassicd if running
zclassic-cli stop

# Backup your wallet first!
cp "$HOME/Library/Application Support/Zclassic/wallet.dat" ~/wallet.dat.backup

# Extract bootstrap
cd "$HOME/Library/Application Support/Zclassic"
zstd -d ~/Downloads/zclassic-bootstrap.tar.zst -o - | tar -x --strip-components=1

# Start zclassicd
zclassicd -daemon
```

### Linux
```bash
# Stop zclassicd if running
zclassic-cli stop

# Backup your wallet first!
cp ~/.zclassic/wallet.dat ~/wallet.dat.backup

# Extract bootstrap
cd ~/.zclassic
zstd -d ~/Downloads/zclassic-bootstrap.tar.zst -o - | tar -x --strip-components=1

# Start zclassicd
zclassicd -daemon
```

### Windows (PowerShell)
```powershell
# Stop zclassicd if running
zclassic-cli stop

# Backup your wallet first!
copy "%APPDATA%\Zclassic\wallet.dat" "%USERPROFILE%\wallet.dat.backup"

# Install zstd if not present (using winget or chocolatey)
# winget install Facebook.zstd
# OR: choco install zstd

# Navigate to Zclassic data directory
cd %APPDATA%\Zclassic

# Extract bootstrap (requires zstd in PATH)
zstd -d "%USERPROFILE%\Downloads\zclassic-bootstrap.tar.zst" -o - | tar -xf -

# Start zclassicd
zclassicd
```

## File List


- `zclassic-bootstrap-20260220.tar.zst.part-00.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-01.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-02.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-03.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-04.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-05.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-06.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-07.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-08.part` (1.0G)
- `zclassic-bootstrap-20260220.tar.zst.part-09.part` (374M)
- `checksums.txt`

## Checksums

```
ddfa3b6063f256241b1b028bd135603ede7a83489251e8b1d90774015c903d98  zclassic-bootstrap-20260220.tar.zst.part-00.part
275b17d15f5219db487dfba0bd761b4793b616e961dc12ce188f26cd44599924  zclassic-bootstrap-20260220.tar.zst.part-01.part
90d8992d9348a2a0e236c4a527ce4c1631bb24f311cb32c737a555f8372c33ca  zclassic-bootstrap-20260220.tar.zst.part-02.part
bba982b9d0c08b225d8d7a646d5ca4a649ce57e855a063d2041766737ee0e5fd  zclassic-bootstrap-20260220.tar.zst.part-03.part
65572058bbd6d619029ee8474237faeb5baad0be0371c7f942e0a312f3d4bcc4  zclassic-bootstrap-20260220.tar.zst.part-04.part
6e48fb743dcccef3e597e62ff8a89ff31abc195f8bc846a43b6f59b76e6375a0  zclassic-bootstrap-20260220.tar.zst.part-05.part
682dc02fd5b4dabbeaa74e9e873e7f8e46c27b5d6f4f3f1d333b6914db8d0f66  zclassic-bootstrap-20260220.tar.zst.part-06.part
a7e65b73f69117f04076ffbb42a64c29ff35f941ac5da3ebb5ab16d30afdc772  zclassic-bootstrap-20260220.tar.zst.part-07.part
2b4fe88fbcefb496493554ebe42d41b45fd5f9ec1cffe9abeb84dc33b2cf1004  zclassic-bootstrap-20260220.tar.zst.part-08.part
afcab1fa7906660e6ab70d1ed4b2a1bd9431ce2f7f9e5f8300331537484ec924  zclassic-bootstrap-20260220.tar.zst.part-09.part
```

## Archive Contents

- **blocks/** - Blockchain data files
- **blocks/index/** - Block index database (LevelDB)
- **chainstate/** - UTXO set database (LevelDB)
- **ZcashParams/** - Sapling and Sprout cryptographic parameters

## Compression

- Algorithm: zstd
- Level: 19 (maximum compression)
- Ratio: ~50% better than gzip

## Requirements

- Enough disk space for extraction (~13 GB)
- zstd installed:
  - macOS: `brew install zstd`
  - Ubuntu/Debian: `apt install zstd`
  - Windows: Download from [zstd releases](https://github.com/facebook/zstd/releases)
- Stopped zclassicd daemon

## Important

- **Always backup wallet.dat before using bootstrap**
- Verify SHA256 checksums before extraction
- Compatible with Zclassic Core 1.x and ZipherX wallet

## Links

- [ZipherX Wallet](https://github.com/ZipherPunk/ZipherX) - Modern Zclassic wallet with automatic bootstrap
- [Zclassic](https://zclassic.org/) - Official Zclassic website

---

*Generated with ZipherX Bootstrap Creator*
