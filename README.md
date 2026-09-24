*This Project has been Created by khhammou*

# ft_otp (Python Edition)

A Time-based One-Time Password (TOTP) generator based on RFC 6238 and RFC 4226, written for the 42 Cybersecurity Piscine.

## Mandatory Part
- Encrypts a minimum 64-character hex key and safely stores it in `ft_otp.key`.
- Reads the encrypted file to generate a 6-digit dynamic TOTP.

## Bonuses Included 🚀
1. **QR Code Generation**: Automatically generates an `ft_otp.png` QR code with a Base32 encoded seed whenever a new key is encrypted, ready to scan with Google Authenticator or Authy.
2. **Graphical User Interface (GUI)**: Built safely using Python's `tkinter`. If `python3-tk` is missing, the CLI still works perfectly without crashing. Run without flags (`./ft_otp`) to open the GUI.

## Testing Reference
To verify that the generated codes are accurate, we test this project against `oathtool`.
You can test your generated keys with the reference tool like this:
```bash
$ oathtool --totp $(cat key.hex)
```

## Installation
Since this is a standalone Python script, there is no compilation step. Just ensure it has executable permissions and install the required external libraries:

```bash
chmod +x ft_otp
pip install -r requirements.txt
```

## Usage
**CLI Mode:**
```bash
# Encrypt and save key
./ft_otp -g key.hex

# Generate password
./ft_otp -k ft_otp.key
```

**GUI Mode:**
```bash
./ft_otp
```

## The Test Process
1. Create a dummy 64-character hex key
echo -n "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef" > key.hex
2. Run script to generate a TOTP
./ft_otp -g key.hex
./ft_otp -k ft_otp.key
3. Run OAthTool using same exact raw key
oathtool $(python3 -c "import base64; print(base64.b32encode(bytes.fromhex('$(cat key.hex)')).decode('utf-8'))")
./ft_otp -k ft_otp.key
