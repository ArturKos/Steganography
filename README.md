# Steganografia

Image steganography tool that hides encrypted text within image files. Uses AES-256 encryption with SHA-512 password hashing for secure message concealment.

## Features

- AES-256 encryption (Rijndael, CBC mode) with PBKDF2 key derivation
- SHA-512 password hashing
- LSB (Least Significant Bit) steganography on RGB pixel channels
- Message length encoded in first 8 pixels, payload in remaining image data
- GUI with image preview, text input, and one-click encode/decode

Built with C# and Windows Forms (.NET 4.0).

![steganografia](https://user-images.githubusercontent.com/17749811/152380975-c267a0a7-2db1-484f-8d52-c3a4364646c6.JPG)
