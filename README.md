# Crypyt

**CRYPT-AES-256-GCM** - Military-grade encryption toolkit for secure communications

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![C++17](https://img.shields.io/badge/C++-17-00599C.svg)](https://isocpp.org/)
[![OpenSSL](https://img.shields.io/badge/OpenSSL-Required-red.svg)](https://www.openssl.org/)

## About

Crypyt is a lightweight, high-performance encryption toolkit implementing **AES-256-GCM** (Advanced Encryption Standard with Galois/Counter Mode), the same encryption standard used by governments and financial institutions worldwide. Designed as a middleware component for building secure communication applications, Crypyt provides battle-tested cryptographic operations through simple command-line tools.

### Key Features

- 🔐 **AES-256-GCM Encryption** - Industry-standard authenticated encryption
- 🛡️ **Authentication Tags** - Prevents message tampering and ensures integrity
- 🎲 **Random IVs** - Each encryption uses unique initialization vectors
- ⚡ **High Performance** - Optimized C++ implementation with OpenSSL
- 🔧 **Flexible Interface** - Command-line arguments or interactive mode
- 🔌 **Middleware Ready** - Perfect for building secure communication apps
- 🐧 **Linux Native** - Designed for Linux systems

### Use Cases

- Secure messaging applications
- File encryption services
- API authentication middleware
- Password managers
- Encrypted backup systems
- IoT device communication

## Installation

### Prerequisites

Crypyt requires OpenSSL libraries to be installed on your system:

```bash
# Debian/Ubuntu
sudo apt update
sudo apt install libssl3

# Fedora/RHEL
sudo dnf install openssl-libs

# Arch Linux
sudo pacman -S openssl
```

### Install Crypyt

```bash
# Download the binaries
# (download encrypter and decrypter from releases)

# Make them executable
chmod +x encrypter decrypter

# Install to system
sudo mv encrypter /usr/local/bin/crypyt-encrypt
sudo mv decrypter /usr/local/bin/crypyt-decrypt

# Verify installation
crypyt-encrypt -h
crypyt-decrypt -h
```

## Usage

### Command-Line Mode

**Encrypt a message:**
```bash
crypyt-encrypt -k "your_secret_key" -m "Hello, World!"
```

**Decrypt a message:**
```bash
crypyt-decrypt -k "your_secret_key" -c "iv:tag:ciphertext"
```

**Note:** Always wrap arguments containing special characters in quotes:
```bash
crypyt-encrypt -k "my;complex>key!" -m "Message with spaces"
```

### Interactive Mode

Simply run without arguments for guided prompts:
```bash
crypyt-encrypt
# Follow the prompts...

crypyt-decrypt
# Follow the prompts...
```

### Integration Example

Use Crypyt as middleware in your applications:

```bash
# Bash script example
#!/bin/bash

# Encrypt user message
encrypted=$(crypyt-encrypt -k "$SECRET_KEY" -m "$USER_MESSAGE")

# Send encrypted message over network
curl -X POST https://api.example.com/send -d "payload=$encrypted"

# Receive and decrypt response
response=$(curl https://api.example.com/receive)
decrypted=$(crypyt-decrypt -k "$SECRET_KEY" -c "$response")
echo "Received: $decrypted"
```

## Security Features

- **256-bit Key Derivation** - Uses SHA-256 to derive strong keys from passwords
- **Authenticated Encryption** - GCM mode provides both confidentiality and authenticity
- **Tamper Detection** - Any modification to encrypted data is automatically detected
- **No Key Reuse** - Random IVs ensure the same message encrypts differently each time
- **Memory Safety** - Sensitive data is cleared from memory after use

## How It Works

1. **Encryption Process:**
   - User provides encryption key and plaintext message
   - Key is derived using SHA-256 hash function (256 bits)
   - Random 12-byte IV (Initialization Vector) is generated
   - AES-256-GCM encrypts the message
   - 16-byte authentication tag is generated
   - Output: `IV:Tag:Ciphertext` (all in hexadecimal)

2. **Decryption Process:**
   - User provides encryption key and encrypted message
   - Message is parsed into IV, Tag, and Ciphertext components
   - Key is derived using the same SHA-256 process
   - AES-256-GCM decrypts and verifies authenticity
   - Original message is recovered (or authentication fails)

## Performance

- Encryption speed: ~500 MB/s (depending on hardware)
- Key derivation: <1ms per operation
- Memory footprint: <5 MB per process

## Contributing

Contributions are welcome! This project aims to provide robust encryption tools for the Linux community.

## License

MIT License - See LICENSE file for details

## Disclaimer

This software is provided for legitimate security purposes. Users are responsible for compliance with applicable laws and regulations regarding encryption in their jurisdiction.

## Support

For issues, questions, or feature requests, please open an issue on the project repository.

---

**Crypyt** - Secure communications made simple.
