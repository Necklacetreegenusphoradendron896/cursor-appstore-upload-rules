# Apple deploy automation cursor rules 🚀

Automated IPA build, TestFlight upload, and App Store submission for **Flutter**, **React Native**, and **Native Swift/Xcode** projects — all from a single Cursor chat command.

---

## Prerequisites 📝

Before using this automation, make sure you have:

1. **macOS** with Xcode installed and command-line tools (`xcode-select --install`)
2. **App Store Connect API Key** — you'll need three things:
   - **Key ID** (10 characters, e.g. `ABC123DEFG`)
   - **Issuer ID** (UUID, e.g. `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`)
   - **.p8 private key file** contents (the `-----BEGIN PRIVATE KEY----- ... -----END PRIVATE KEY-----` block)

   > Get these from [App Store Connect → Users and Access → Integrations → App Store Connect API](https://appstoreconnect.apple.com/access/integrations/api). The key needs **App Manager** or **Admin** role.

---

## How to Use 🤔

### 1. Open your project in Cursor

Navigate to the root of your iOS project (Flutter, React Native, or native Xcode project).

### 2. Choose your mode

There are two modes:

| Mode | What it does | When to use |
|------|-------------|-------------|
| **Mode A — TestFlight Only** | Builds IPA, uploads to TestFlight|
| **Mode B — Full Submission** | Build ipa and submit it for review |

### 3. Type this in cursor chat (Auto mode is more than enough)
---

## Mode A — TestFlight Only

Just type:

```
UPLOAD_IPA_NOW testflight
framework: flutter
KEY_ID: ABC123DEFG
ISSUER_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
P8_KEY:
-----BEGIN PRIVATE KEY-----
MIGTAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBHkwdwIBAQQg...
-----END PRIVATE KEY-----
```

That's it. Cursor will:
1. Fix export compliance in Info.plist (one-time)
2. Build the IPA
3. Upload to TestFlight via `altool`
4. Print a status report

---

## Mode B — Full App Store Submission

```
UPLOAD_IPA_NOW
framework: react-native
KEY_ID: ABC123DEFG
ISSUER_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
P8_KEY:
-----BEGIN PRIVATE KEY-----
MIGTAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBHkwdwIBAQQg...
-----END PRIVATE KEY-----
What changed
1- en_us "Bug fixes and performance improvements"
2- ar_sa "إصلاح الأخطاء وتحسين الأداء"
```

Cursor will do everything in Mode A, **plus**:
- Create or reuse the App Store version
- Set App Store "What's New" notes
- Attach the build
- Submit for Apple review

---

## Framework Examples

### Flutter Project

```
UPLOAD_IPA_NOW testflight
framework: flutter
KEY_ID: 9M98FCPQGU
ISSUER_ID: c89e8147-11df-40c1-abfb-88298c838a1e
P8_KEY:
-----BEGIN PRIVATE KEY-----
MIGTAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBHkwdwIBAQQg...
-----END PRIVATE KEY-----
```

### React Native Project

```
UPLOAD_IPA_NOW testflight
framework: react-native
KEY_ID: 9M98FCPQGU
ISSUER_ID: c89e8147-11df-40c1-abfb-88298c838a1e
P8_KEY:
-----BEGIN PRIVATE KEY-----
MIGTAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBHkwdwIBAQQg...
-----END PRIVATE KEY-----
```

### Native Swift / Xcode Project

```
UPLOAD_IPA_NOW testflight
framework: swift
KEY_ID: 9M98FCPQGU
ISSUER_ID: c89e8147-11df-40c1-abfb-88298c838a1e
P8_KEY:
-----BEGIN PRIVATE KEY-----
MIGTAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBHkwdwIBAQQg...
-----END PRIVATE KEY-----
```

---

## Supported Locale Aliases

You can write locales in any of these formats — they'll be normalized automatically:

| You write | Apple gets |
|-----------|-----------|
| `en_us` / `english` / `en` | `en-US` |
| `ar_sa` / `arabic` / `ar` | `ar-SA` |
| `fr_fr` / `french` / `fr` | `fr-FR` |
| `de_de` / `german` / `de` | `de-DE` |
| `es_es` / `spanish` / `es` | `es-ES` |
| `pt_br` / `portuguese` / `pt` | `pt-BR` |
| `ja` / `japanese` | `ja` |
| `ko` / `korean` | `ko` |
| `zh_cn` / `chinese` | `zh-Hans` |
| `zh_tw` | `zh-Hant` |
| `tr_tr` / `turkish` / `tr` | `tr` |
| `it_it` / `italian` / `it` | `it` |
| `nl_nl` / `dutch` / `nl` | `nl-NL` |
| `ru_ru` / `russian` / `ru` | `ru` |
| `hi_in` / `hindi` / `hi` | `hi` |
| Any `xx_YY` | `xx-YY` |

---

## Timing Expectations

| Step | Typical Duration |
|------|-----------------|
| Test flight | 5-20 (including the proccessing time by apple) |
| Full app submition | 5-25 minutes |

---
