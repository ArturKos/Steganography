# Steganography

A Windows Forms desktop application that hides encrypted text messages inside image files using **LSB steganography** combined with **AES-256 encryption** and **SHA-512 password hashing**.

![C#](https://img.shields.io/badge/C%23-4.0-239120?logo=csharp)
![.NET](https://img.shields.io/badge/.NET_Framework-4.0-512BD4?logo=dotnet)
![Windows Forms](https://img.shields.io/badge/Windows_Forms-GUI-0078D4?logo=windows)

## Features

- **AES-256 encryption** (Rijndael, CBC mode) with PBKDF2 key derivation (1000 iterations) for strong message confidentiality
- **SHA-512 password hashing** applied to the user-supplied password before key derivation
- **LSB pixel encoding** -- message bits are embedded into the least significant bit of each RGB channel across image pixels
- **Length header** encoded in the first 8 pixels, followed by the encrypted payload in remaining image data
- **Side-by-side preview** -- original and steganographic images displayed together for visual comparison
- **One-click encode/decode** -- load an image, type a message and password, then encode or decode with a single button press

## Screenshot

![steganografia](https://user-images.githubusercontent.com/17749811/152380975-c267a0a7-2db1-484f-8d52-c3a4364646c6.JPG)

## Dependencies

| Component | Version | Purpose |
|-----------|---------|---------|
| .NET Framework | 4.0 | Runtime and base class libraries |
| System.Drawing | built-in | Bitmap pixel manipulation |
| System.Windows.Forms | built-in | GUI framework |
| System.Security.Cryptography | built-in | AES-256, SHA-512, PBKDF2 |

## How It Works

1. The user loads a carrier image and enters a plaintext message with a password.
2. The password is hashed with **SHA-512** and used to derive an AES-256 key via **Rfc2898DeriveBytes** (PBKDF2).
3. The plaintext is encrypted with **AES-256-CBC**.
4. The ciphertext length (1 byte) is encoded into the LSB of the first 8 pixel channels (R, G, B).
5. Each bit of the ciphertext is then written into the LSB of successive pixel channels across the entire image.
6. Decoding reverses the process: extract length, extract ciphertext bits, decrypt with the same password.

## Building

### Visual Studio

1. Open `kodowanie.csproj` in Visual Studio 2010 or later.
2. Set the build configuration to **Debug** or **Release** (x86).
3. Build the solution (`Ctrl+Shift+B`).

### Command Line (MSBuild)

```bash
msbuild kodowanie.csproj /p:Configuration=Release /p:Platform=x86
```

The compiled binary will be placed in `bin\Release\`.

## Usage

1. Click **Load Image** to select a carrier image (BMP, PNG, JPG).
2. Enter the secret message in the **Text to encrypt** field.
3. Enter a password in the **Password** field.
4. Click **Embed message into image** to produce the steganographic image (shown on the right).
5. To decode, click **Read hidden message** with the same password entered.

## Project Structure

```
Steganography/
├── CryptAES_Class.cs       # AES-256 encrypt/decrypt with PBKDF2 key derivation
├── Form1.cs                # Main UI logic: LSB encode/decode, image I/O
├── Form1.Designer.cs       # Windows Forms designer layout
├── Form1.resx              # Form resource file
├── kodowanie.csproj        # MSBuild project file (.NET 4.0, x86)
├── Program.cs              # Application entry point
├── Properties/
│   ├── AssemblyInfo.cs     # Assembly metadata
│   ├── Resources.resx      # Embedded resources
│   └── Settings.settings   # Application settings
└── README.md
```

## License

This project is provided as-is for educational purposes.
