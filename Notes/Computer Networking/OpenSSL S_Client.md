Sure! Here's a detailed breakdown of **`openssl s_client`**, from first principles:

---

## 🔐 What is `openssl s_client`?

**`openssl s_client`** is a **command-line diagnostic tool** provided by the [OpenSSL library](https://www.openssl.org/), which lets you:

> 👉 **Manually establish a secure SSL/TLS connection to a remote server.**

It’s like a secure version of `telnet` — but specifically for testing and debugging **TLS** connections.

---

## 🧠 Why and When Is It Used?

| Use Case                        | Description                                                       |
| ------------------------------- | ----------------------------------------------------------------- |
| ✅ Test a TLS connection         | Check if a server supports TLS and which versions/ciphers it uses |
| ✅ Inspect certificates          | See the full certificate chain, validity, and metadata            |
| ✅ Debug HTTPS, SMTP, IMAP, etc. | Interact with TLS-enabled services using raw text                 |
| ✅ Test mutual TLS (mTLS)        | Supply client certificate/key to test secure APIs                 |

---

## 🔧 Basic Usage

```bash
openssl s_client -connect <host:port>
```

### Example:

```bash
openssl s_client -connect google.com:443
```

This will:

* Open a TCP connection to `google.com` on port 443
* Initiate a **TLS handshake**
* Show detailed debug info (protocol version, certificate, cipher suite, etc.)

You can then **type a manual HTTP request**:

```
GET / HTTP/1.1
Host: google.com

```

And get back the raw HTTP response over TLS.

---

## ⚙️ Key Options

| Option                     | Purpose                                       |
| -------------------------- | --------------------------------------------- |
| `-connect host:port`       | Where to connect (required)                   |
| `-servername name`         | Set SNI (for virtual hosting in HTTPS)        |
| `-showcerts`               | Show full certificate chain                   |
| `-CAfile file.pem`         | Use a custom CA file for verifying the server |
| `-cert client.pem`         | Client certificate (for mutual TLS)           |
| `-key key.pem`             | Private key for the client cert               |
| `-tls1_2`, `-tls1_3`, etc. | Force specific TLS version                    |
| `-crlf`                    | Convert LF to CRLF (useful for SMTP)          |

---

## 🧪 Examples

### 🔍 Test HTTPS Connection

```bash
openssl s_client -connect example.com:443 -servername example.com
```

### 📜 See Certificate Expiry

```bash
openssl s_client -connect example.com:443 </dev/null 2>/dev/null | openssl x509 -noout -dates
```

### 🔐 Test Mutual TLS

```bash
openssl s_client -connect api.example.com:443 \
  -cert client.crt -key client.key \
  -CAfile ca.crt
```

---

## 📤 Output Breakdown

The output includes:

* TLS handshake details (protocol version, cipher)
* Certificate chain (PEM format)
* Session details
* Option to type text to the server securely

---

## ✅ Summary

| Property       | Value                                               |
| -------------- | --------------------------------------------------- |
| Type           | CLI tool from OpenSSL                               |
| Purpose        | Manual TLS testing/debugging                        |
| Protocol Layer | Application layer (uses TLS over TCP)               |
| Use Cases      | HTTPS testing, mTLS, cert inspection, SMTP over TLS |

---

If you'd like to practice with a real server or want help writing a script to automate TLS checks, let me know — I can walk you through it!
