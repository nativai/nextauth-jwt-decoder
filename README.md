# NextAuth JWT Decoder

A simple client-side tool to decode NextAuth.js encrypted JWT session tokens.

**[Try it live](https://nativai.github.io/nextauth-jwt-decoder/)**

## The Problem

NextAuth.js encrypts session tokens using JWE (JSON Web Encryption), which makes debugging authentication issues frustrating:

- **jwt.io** - The most popular JWT tool doesn't support encrypted tokens at all
- **[Dino Chiesa's JWT Tool](https://dinochiesa.github.io/jwt)** - Requires the derived private key, not the original secret
- **[Authgear JWT & JWE Debugger](https://authgear.com/tools/jwt-jwe-debugger)** - Also requires the derived private key

These tools expect a cryptographic key that's derived from `NEXTAUTH_SECRET` through a specific key derivation process - not the secret itself.

## The Solution

This tool does one thing well: **paste your encrypted token and your `NEXTAUTH_SECRET`, and see the decoded content.**

No key derivation headaches. No configuration. Just paste and decode.

## Features

- Decodes NextAuth.js v4+ encrypted JWE tokens
- Works entirely client-side (your secrets never leave your browser)
- Handles the HKDF key derivation automatically
- Shows both header and payload in a readable format

## Usage

1. Copy your encrypted session token (from cookies or network requests)
2. Paste your `NEXTAUTH_SECRET` environment variable
3. Click "Decode" or press Ctrl+Enter

### Finding Your Session Cookie

The cookie name varies depending on your setup:

**NextAuth.js v4:**
- `next-auth.session-token` — Standard (HTTP or localhost)
- `__Secure-next-auth.session-token` — When using HTTPS with secure cookies

**Auth.js v5:**
- `authjs.session-token` — Standard (HTTP or localhost)
- `__Secure-authjs.session-token` — When using HTTPS with secure cookies

The `__Secure-` prefix is automatically added by NextAuth/Auth.js when cookies are set with the `Secure` flag (typically in production with HTTPS).

## Security

All decryption happens in your browser using the Web Crypto API. No data is sent to any server.
