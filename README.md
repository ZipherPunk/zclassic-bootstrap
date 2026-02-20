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

- **Block Height**: 2933984
- **Date**: 2025-12-06
- **Total Size**: 7.8G (compressed)
- **Parts**: 5 files

## Zcash Parameters

Cryptographic parameters required by zclassicd for shielded transactions.

- **Release**: [zcash-params-v1](https://github.com/ZipherPunk/zclassic-bootstrap/releases/tag/zcash-params-v1)
- **Total Size**: 1.54 GB (compressed) / 1.69 GB (uncompressed)
- **Compression**: zstd level 19

### Files

| File | Compressed | Original | Purpose |
|------|------------|----------|---------|
| sapling-spend.params.zst | 45 MB | 47 MB | Prove shielded spends |
| sapling-output.params.zst | 3.2 MB | 3.5 MB | Create shielded outputs |
| sprout-groth16.params.zst | 655 MB | 725 MB | Legacy Sprout proofs |
| sprout-proving.key.zst | 837 MB | 868 MB | Generate Sprout proofs |
| sprout-verifying.key.zst | 1.4 KB | 1.4 KB | Verify Sprout proofs |

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
# Download the helper script
gh release download --repo ZipherPunk/zclassic-bootstrap --pattern "download-and-combine.sh"
chmod +x download-and-combine.sh
./download-and-combine.sh
```

#### Option 2: Manual Download
1. Go to the [latest release](https://github.com/ZipherPunk/zclassic-bootstrap/releases/latest)
2. Download all `zclassic-bootstrap-*-part-*.part` files
3. Download `bootstrap-checksums.txt`
4. Verify checksums: `shasum -a 256 -c bootstrap-checksums.txt`
5. Combine parts: `cat zclassic-bootstrap-*-part-*.part > zclassic-bootstrap.tar.zst`

## Installation

### macOS
```bash
# Stop zclassicd if running
pkill zclassicd

# Backup your wallet first!
cp "$HOME/Library/Application Support/Zclassic/wallet.dat" ~/wallet.dat.backup

# Extract bootstrap
cd "$HOME/Library/Application Support/Zclassic"
zstd -d ~/Downloads/zclassic-bootstrap.tar.zst -o - | tar -x --strip-components=1

# Start zclassicd
zclassicd
```

### Linux
```bash
# Stop zclassicd if running
pkill zclassicd

# Backup your wallet first!
cp ~/.zclassic/wallet.dat ~/wallet.dat.backup

# Extract bootstrap
cd ~/.zclassic
zstd -d ~/Downloads/zclassic-bootstrap.tar.zst -o - | tar -x --strip-components=1

# Start zclassicd
zclassicd
```

### Windows (PowerShell)
```powershell
# Stop zclassicd if running
taskkill /IM zclassicd.exe /F 2>nul

# Backup your wallet first!
copy "%APPDATA%\Zclassic\wallet.dat" "%USERPROFILE%\wallet.dat.backup"

# Install zstd if not present (using winget or chocolatey)
# winget install Facebook.zstd
# OR: choco install zstd

# Navigate to Zclassic data directory
cd %APPDATA%\Zclassic

# Extract bootstrap (requires zstd in PATH)
zstd -d "%USERPROFILE%\Downloads\zclassic-bootstrap.tar.zst" -o - | tar -xf -

# Alternative: Use WSL if available
# wsl zstd -d ~/Downloads/zclassic-bootstrap.tar.zst -o - | wsl tar -x --strip-components=1

# Start zclassicd
zclassicd
```

## File List

- `zclassic-bootstrap-block-2933984-20251206_052149-part-01.part` (1.9G)
- `zclassic-bootstrap-block-2933984-20251206_052149-part-02.part` (1.9G)
- `zclassic-bootstrap-block-2933984-20251206_052149-part-03.part` (1.9G)
- `zclassic-bootstrap-block-2933984-20251206_052149-part-04.part` (1.9G)
- `zclassic-bootstrap-block-2933984-20251206_052149-part-05.part` (318M)
- `bootstrap-checksums.txt`
- `download-and-combine.sh`
- `BOOTSTRAP_README.md`

## Checksums

```
c6fc052add092c186f0cfe2e136b61b1e79c45d5c504c97c4a5522fddea334b7  zclassic-bootstrap-block-2933984-20251206_052149-part-01.part
2d11a48c027271addb13a881498185938252b636e6844d64684b78d4d74f1b79  zclassic-bootstrap-block-2933984-20251206_052149-part-02.part
6a4d818f3654ff7583ae9487f98e5e47bce81b0012530ede0bdbcb2423a6dcec  zclassic-bootstrap-block-2933984-20251206_052149-part-03.part
6e6bdfacb333abd95bc162bb19e904d2b377550929166ac175692239e7d23055  zclassic-bootstrap-block-2933984-20251206_052149-part-04.part
0c5018efb15859a88955101ad618adbb38e62ef81ce4de1f62a7e699a6f15bf7  zclassic-bootstrap-block-2933984-20251206_052149-part-05.part
```

## Archive Contents

- **blocks/** - Blockchain data files
- **blocks/index/** - Block index database (LevelDB)
- **chainstate/** - UTXO set database (LevelDB)

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

## ⚠️ Important

- **Always backup wallet.dat before using bootstrap**
- Verify SHA256 checksums before extraction
- Compatible with Zclassic Core 1.x and ZipherX wallet

## Links

- [ZipherX Wallet](https://github.com/ZipherPunk/ZipherX) - Modern Zclassic wallet with automatic bootstrap
- [Zclassic](https://zclassic.org/) - Official Zclassic website

---

🤖 Generated with ZipherX Bootstrap Creator
