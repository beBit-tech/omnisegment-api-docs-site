# Here is an example of encryption and decryption code for [Audience Sensitive Information API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Audience-Sensitive-Information-API-SPEC) identified field.

## Python
```python
class AES256Cipher:
    def __init__(self, key) -> None:
        self.key = hashlib.sha256(key.encode()).digest()

    def encrypt(self, raw_text):
        raw_text = pad(raw_text.encode(), AES.block_size)
        iv = Random.new().read(AES.block_size)
        cipher = AES.new(self.key, AES.MODE_CBC, iv)
        return base64.b64encode(iv + cipher.encrypt(raw_text))

    def decrypt(self, cipher_text):
        cipher_text = base64.b64decode(cipher_text)
        iv = cipher_text[: AES.block_size]
        cipher = AES.new(self.key, AES.MODE_CBC, iv)
        decrypt_text = cipher.decrypt(cipher_text[AES.block_size :])
        return unpad(decrypt_text, AES.block_size).decode("utf-8")

key = 'my_secret_key'
cipher = AES256Cipher(key)
encrypted = cipher.encrypt('Hello, World!')
print('Encrypted:', encrypted)
decrypted = cipher.decrypt(encrypted)
print('Decrypted:', decrypted)
```

## Javascript
```javascript
const crypto = require('crypto');

function encrypt(key, text) {
    const iv = crypto.randomBytes(16);
    const cipher = crypto.createCipheriv('aes-256-cbc', Buffer.from(hashKey(key)), iv);
    let encrypted = cipher.update(text, 'utf8', 'base64');
    encrypted += cipher.final('base64');
    return iv.toString('base64') + encrypted;
}

function hashKey(key) {
    return crypto.createHash('sha256').update(key).digest();
}

const key = 'my_secret_key';
const encrypted = encrypt(key, 'Hello, World!');
console.log('Encrypted:', encrypted);
```

## Go
```go
package main

import (
    "crypto/aes"
    "crypto/cipher"
    "crypto/sha256"
    "encoding/base64"
    "fmt"
)

func encrypt(key string, text string) (string, error) {
    hashedKey := sha256.Sum256([]byte(key))
    block, err := aes.NewCipher(hashedKey[:])
    if err != nil {
        return "", err
    }
    iv := make([]byte, aes.BlockSize) // AES block size
    mode := cipher.NewCBCEncrypter(block, iv)

    paddedText := pad([]byte(text), aes.BlockSize)
    ciphertext := make([]byte, len(paddedText))
    mode.CryptBlocks(ciphertext, paddedText)

    return base64.StdEncoding.EncodeToString(iv) + base64.StdEncoding.EncodeToString(ciphertext), nil
}

func pad(src []byte, blockSize int) []byte {
    padding := blockSize - len(src)%blockSize
    padtext := bytes.Repeat([]byte{byte(padding)}, padding)
    return append(src, padtext...)
}

func main() {
    key := "my_secret_key"
    encrypted, _ := encrypt(key, "Hello, World!")
    fmt.Println("Encrypted:", encrypted)
}
```

## Java
```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;
import java.util.Base64;

public class AES256Cipher {
    private static final String ALGORITHM = "AES/CBC/PKCS5Padding";

    public static String encrypt(String key, String data) throws Exception {
        SecretKey secretKey = new SecretKeySpec(hashKey(key), "AES");
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        byte[] iv = new byte[16]; // AES block size
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, new IvParameterSpec(iv));
        byte[] encrypted = cipher.doFinal(data.getBytes());
        return Base64.getEncoder().encodeToString(iv) + Base64.getEncoder().encodeToString(encrypted);
    }

    private static byte[] hashKey(String key) {
        return Arrays.copyOf(key.getBytes(), 32); // 32 bytes for AES-256
    }

    public static void main(String[] args) throws Exception {
        String key = "my_secret_key";
        String encrypted = encrypt(key, "Hello, World!");
        System.out.println("Encrypted: " + encrypted);
    }
}
```

## C#
```C#
using System;
using System.IO;
using System.Security.Cryptography;
using System.Text;

public class AES256Cipher
{
    private readonly byte[] key;

    public AES256Cipher(string key)
    {
        using (SHA256 sha256 = SHA256.Create())
        {
            this.key = sha256.ComputeHash(Encoding.UTF8.GetBytes(key));
        }
    }

    public string Encrypt(string plainText)
    {
        using (Aes aes = Aes.Create())
        {
            aes.Key = key;
            aes.Mode = CipherMode.CBC;
            aes.Padding = PaddingMode.PKCS7;
            aes.GenerateIV();

            using (var encryptor = aes.CreateEncryptor(aes.Key, aes.IV))
            using (var ms = new MemoryStream())
            {
                ms.Write(aes.IV, 0, aes.IV.Length); // Prepend IV to the encrypted data
                using (var cs = new CryptoStream(ms, encryptor, CryptoStreamMode.Write))
                {
                    byte[] plainBytes = Encoding.UTF8.GetBytes(plainText);
                    cs.Write(plainBytes, 0, plainBytes.Length);
                    cs.FlushFinalBlock();
                }

                return Convert.ToBase64String(ms.ToArray());
            }
        }
    }

    public string Decrypt(string cipherText)
    {
        byte[] cipherBytes = Convert.FromBase64String(cipherText);

        using (Aes aes = Aes.Create())
        {
            aes.Key = key;
            aes.Mode = CipherMode.CBC;
            aes.Padding = PaddingMode.PKCS7;

            // Extract IV from the beginning of the cipherBytes array
            byte[] iv = new byte[aes.BlockSize / 8];
            Array.Copy(cipherBytes, 0, iv, 0, iv.Length);
            aes.IV = iv;

            using (var decryptor = aes.CreateDecryptor(aes.Key, aes.IV))
            using (var ms = new MemoryStream(cipherBytes, iv.Length, cipherBytes.Length - iv.Length))
            using (var cs = new CryptoStream(ms, decryptor, CryptoStreamMode.Read))
            using (var sr = new StreamReader(cs))
            {
                return sr.ReadToEnd();
            }
        }
    }
}

class Program
{
    static void Main()
    {
        string key = "my_secret_key";
        AES256Cipher cipher = new AES256Cipher(key);

        string encrypted = cipher.Encrypt("Hello, World!");
        Console.WriteLine("Encrypted: " + encrypted);

        string decrypted = cipher.Decrypt(encrypted);
        Console.WriteLine("Decrypted: " + decrypted);
    }
}
```