# 📦 RSTF (Rust Secure Transport Format)

<div align="center">
  <img src="https://raw.githubusercontent.com/warchs/warchs/refs/heads/main/image/rstf.png" width="420" alt="Logo" style="height: 200px; max-width: 100%;">

  <br />

  [![Release](https://img.shields.io/github/v/release/warchs/rstf-rust)](https://github.com/warchs/rstf-rust/releases)
  [![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
  [![Platform](https://img.shields.io/badge/platform-Win%20%7C%20Linux%20%7C%20Mac%20%7C%20Android-green)](https://github.com/warchs/rstf-rust/releases)
  [![GitHub Stars](https://img.shields.io/github/stars/warchs/rstf-rust?style=social)](https://github.com/warchs/rstf-rust)
</div>


**RSTF** is a high-performance file archiving utility built in Rust, prioritizing data security through modern encryption and efficient compression. It leverages cutting-edge cryptographic standards to safeguard files against emerging threats.

> Engineered for seamless cross-platform operation

---

## ⚡ Why RSTF?

Conventional archiving tools often employ outdated security measures vulnerable to contemporary attacks. **RSTF** stands out by integrating robust, forward-looking cryptography.

| Feature | 📦 RSTF (This Tool) | 🤐 7-Zip | 🗄️ ZIP |
| :--- | :--- | :--- | :--- |
| **Encryption** | **XChaCha20-Poly1305** (IETF Standard) | AES-256 | AES / ZipCrypto |
| **Key Derivation** | **Argon2id** (Memory-Hard) 🛡️ | PBKDF2 (Susceptible to GPU Attacks) | None / Weak |
| **Metadata** | **Fully Encrypted** 🔒 | Visible (Optional Encryption) | Visible |
| **Compression** | **Zstd** (Multithreaded) 🚀 | LZMA (Resource-Intensive) | Deflate |
| **Keyfile Support** | ✅ **Native** | ❌ No | ❌ No |
| **Mobile Native** | ✅ **Android/Termux Binary** | ❌ Requires App | ❌ Requires App |


---
## 📥 Installation


### 📱 Android (Termux) Users
No root privileges required. Install the pre-compiled binary directly (choose based on your device architecture):

```bash
# For ARM64 devices (most Android phones)
wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-android-arm64 -O $PREFIX/bin/rstf

chmod +x $PREFIX/bin/rstf

rstf --version

# For x86_64 emulators (if using Android emulator)
wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-android-x86_64 -O $PREFIX/bin/rstf

chmod +x $PREFIX/bin/rstf

rstf --version

# Help
rstf --help
```

### 🐧 Linux Users
Install system-wide (choose based on your architecture for best compatibility):

```bash
# For x86_64 systems (most common)
sudo wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-linux-amd64 -O /usr/local/bin/rstf

sudo chmod +x /usr/local/bin/rstf

rstf --version

# For ARM64 systems (e.g., Raspberry Pi or ARM servers)
sudo wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-linux-arm64 -O /usr/local/bin/rstf

sudo chmod +x /usr/local/bin/rstf

rstf --version

# For static musl versions (no dependencies, portable)
sudo wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-linux-amd64-musl -O /usr/local/bin/rstf

sudo chmod +x /usr/local/bin/rstf

rstf --version

# Help
rstf --help
```

### 🍎 macOS Users
Compatible with Intel and Apple Silicon (choose based on your chip):

```bash
# For Intel Macs (x86_64)
sudo wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-macos-amd64 -O /usr/local/bin/rstf

sudo chmod +x /usr/local/bin/rstf

rstf --version

# For Apple Silicon (ARM64, M1/M2 chips)
sudo wget -q https://github.com/warchs/rstf-rust/releases/latest/download/rstf-macos-arm64 -O /usr/local/bin/rstf

sudo chmod +x /usr/local/bin/rstf

rstf --version

# Help
rstf --help
```

### 💻 Windows Users
1. Download the appropriate .exe from the [Release Page](https://github.com/warchs/rstf-rust/releases) (MSVC recommended for compatibility, GNU as alternative).
2. Open Command Prompt or PowerShell in the download folder.
3. Run: `.\rstf-windows-amd64.exe --help` (or `.\rstf-windows-amd64-gnu.exe --help` for GNU version). (Optional: Add the folder to your PATH for easier access).

---

## 📖 Usage Guide
1. 🔒 Pack (Encrypt & Compress) Securely archive files or directories.

```bash
# Basic usage (Prompts for password securely)
rstf pack ./sensitive_data

# Advanced Mode (Maximum compression + Keyfile + Wipe originals)
rstf pack ./important_file.db --level 22 --wipe -k ./key_image.jpg
```
> Note: The --wipe flag securely deletes source files after successful archiving.

2. 🔓 Unpack (Decrypt & Extract) Restore archived data. Provide the password (and keyfile if used).

```bash
# Basic unpack
rstf unpack ./sensitive_data.rstf

# Unpack with Keyfile
rstf unpack ./important_file.rstf -k ./key_image.jpg
```

3. 📜 List Contents View archive contents without extraction. Credentials are needed since metadata is encrypted.

```bash
rstf list ./backup.rstf
```

---

## 🤝 Contributing
We welcome contributions from the community! RSTF is an open-source project, and your input helps improve security, performance, and usability. Here's how to get involved:

### Ways to Contribute
* **Report Issues:** Found a bug or have a feature request? Open an [issue](https://github.com/warchs/rstf-rust/issues) on GitHub.
* **Submit Pull Requests:** Fork the repo, make changes, and submit a PRequest. We follow standard Rust practices (e.g., `cargo fmt`, `cargo clippy`).
* **Improve Documentation:** Help translate or enhance this README, or add examples.
* **Test on New Platforms:** Try RSTF on untested devices and share feedback.

### Development Setup

1. Clone the repository:

```bash
git clone https://github.com/warchs/rstf-rust.git
cd rstf-rust
```

2. Install Rust (if not already):

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

3. Build and test:

```bash
cargo build --release
cargo test
```

4. Run the CI locally (optional):
Use GitHub Actions or tools like `cross` for cross-platform testing.

### Guidelines

* Follow the [Rust Code of Conduct](https://rust-lang.org/policies/code-of-conduct/).
* Ensure all changes pass tests and are well-documented.
* For security-related changes, discuss in issues first.

Thank you for contributing to RSTF! 🌟


---

## 🛠️ Technical Details

RSTF implements an **Encrypt-then-MAC** approach using modern cryptographic primitives:

* **Compression: Zstd** (Levels 1-22). Processes data in 64KB chunks for efficient memory use.
* **KDF (Key Derivation): Argon2id** (Version 19). Increases resistance to brute-force by demanding high computational and memory resources, countering GPU clusters.
* **Encryption: XChaCha20-Poly1305.** A performant authenticated stream cipher.
* **Randomness:** Relies on the OS's cryptographically secure random number generator (via the rand crate) for salts and nonces.

---

## ⚠️ Important Security Notice
**This software contains no backdoors.** Loss of your password or keyfile will make data irrecoverable. RSTF's cryptography is designed to resist brute-force attacks. Always secure backups and use strong, unique passwords.

---

## 👤 Author

**William Nathanael** (warchs)

* Independent Developer and Cybersecurity Enthusiast
* This README and the entire project were manually crafted by a human developer, drawing from personal experience in Rust programming and cryptography. No automated tools, bots, or AI were used in its creation to ensure authenticity and originality.
* [GitHub Profile](https://github.com/warchs)

* [Personal Website]()

---

## 🙏 Acknowledgments
A big thank you to the **Rust programming language** and its incredible community for providing a safe, fast, and productive ecosystem that made RSTF possible. Special thanks to the developers and maintainers of key crates that power RSTF:

* **Zstd** (compression library) for efficient, multithreaded data compression.
* **Argon2** (for Argon2id KDF) for robust password hashing against brute-force attacks.
* **ChaCha20-Poly1305** (via RustCrypto) for secure, authenticated encryption.
* **Rand** for cryptographically secure random number generation.
* And the broader open-source community for tools like `cross` for cross-compilation and GitHub Actions for CI/CD.

Your contributions keep the Rust ecosystem thriving—thank you! If you've contributed or inspired this project, feel free to reach out.


---

##  📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Build with 🥰 for everyone
