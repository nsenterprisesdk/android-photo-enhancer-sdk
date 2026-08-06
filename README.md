<!-- Banner -->
<div align="center">
  <img src="./marketing_banner.png" alt="Clarify Photo Enhancer SDK Banner" width="100%" style="border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
</div>

<br/>

<div align="center">
  
[![Photo Enhancer SDK](https://img.shields.io/badge/Clarify_Enhancer_SDK-v1.0.6-8B5CF6?style=for-the-badge&logo=android)](https://github.com/nsenterprisesdk/android-photo-enhancer-sdk)
[![JitPack](https://jitpack.io/v/nsenterprise9865-stack/photoenhancer-sdk-distribution.svg?style=for-the-badge)](https://jitpack.io/#nsenterprise9865-stack/photoenhancer-sdk-distribution)
[![Platform](https://img.shields.io/badge/Platform-Android_API_26+-10B981?style=for-the-badge&logo=android)](https://developer.android.com)
[![License](https://img.shields.io/badge/License-Commercial-F97316?style=for-the-badge)](#-pricing)

<h3>The Ultimate On-Device Photo Enhancement SDK for Android</h3>
<p><b>No servers. No per-image costs. 100% private. Just one powerful license key.</b></p>

[**🚀 Quick Start**](#-quick-start-implementation) &nbsp; | &nbsp; [**✨ See the Magic**](#-see-the-magic-before--after) &nbsp; | &nbsp; [**💳 Get a License**](#-pricing--licensing)

</div>

---

## 🛑 Stop Paying Cloud APIs Per Image

Using Replicate, Stability AI, or custom cloud backends? You're paying **$0.01 – $0.05 per image**. That destroys your margins.

<div align="center">

| Monthly Active Users | Avg Enhancements | Competitor Cloud API Cost | **Clarify SDK Cost** |
|:---:|:---:|:---:|:---:|
| **1,000 users** | 2/session | ~$50 – $100 / mo | <b style="color:#10B981;">$49 / mo</b> |
| **10,000 users** | 2/session | ~$500 – $1,000 / mo | <b style="color:#10B981;">$49 / mo</b> |
| **100,000 users**| 2/session | ~$5,000 – $10,000 / mo | <b style="color:#10B981;">$149 / mo</b> |

</div>

> **Scale infinitely:** One license. Unlimited users. Unlimited enhancements. Processing happens directly on your user's device.

---

## ✨ See the Magic (Before & After)

We bring state-of-the-art **NSRestore** and **Real-FSRCNN** directly to the edge.

<table align="center" style="width: 100%; border-collapse: collapse;">
  <tr>
    <td align="center" width="50%">
      <b>🪄 Face Restoration (NSRestore)</b><br/>
      <p><i>Studio-level clarity using our ultra-lightweight (8.2MB) custom NSRestore model.</i></p>
    </td>
    <td align="center" width="50%">
      <b>⬆️ 4× Super-Resolution (FSRCNN)</b><br/>
      <p><i>Lightning fast (47KB model) upscaling for rich background details and textures.</i></p>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="./face_before_v2.jpg" width="48%" style="border-radius: 8px;"/>
      <img src="./face_after_v2.jpg" width="48%" style="border-radius: 8px;"/>
    </td>
    <td align="center">
      <img src="./upscale_before_v2.jpg" width="48%" style="border-radius: 8px;"/>
      <img src="./upscale_after_v2.jpg" width="48%" style="border-radius: 8px;"/>
    </td>
  </tr>
</table>

---

## 🛠️ Core Features

<table align="center">
  <tr>
    <td width="50%" valign="top">
      <h3>👤 Intelligent Face Blending</h3>
      <p>Advanced feathered-mask technology blends each restored face seamlessly back into the upscaled background. Zero "pasted-on" look.</p>
    </td>
    <td width="50%" valign="top">
      <h3>🔒 100% On-Device Privacy</h3>
      <p>Photos never leave the device. Processing runs on TensorFlow Lite/ONNX. Add this to your privacy policy and stay fully GDPR/CCPA compliant.</p>
    </td>
  </tr>
  <tr>
    <td valign="top">
      <h3>🎨 Fully Themed UI Included</h3>
      <p>Drop in our beautiful Jetpack Compose UI and instantly re-brand it with your colors, typography, and strings in seconds.</p>
    </td>
    <td valign="top">
      <h3>👻 Headless Mode (Custom UI)</h3>
      <p>Want total control? Build your own camera/picker and just use our invisible Headless API to power the underlying AI processing.</p>
    </td>
  </tr>
</table>

---

## 🚀 Quick Start (Implementation)

Integrating Clarify SDK takes less than 10 minutes.

### 1. Add Dependency
Add the JitPack repository to your `settings.gradle.kts` and the SDK to your `app/build.gradle.kts`:

```kotlin
// app/build.gradle.kts
dependencies {
    implementation("com.github.nsenterprise9865-stack:photoenhancer-sdk-distribution:1.0.6")
}
```

### 2. Initialize
Validate your license and start prefetching AI models securely:

```kotlin
lifecycleScope.launch {
    val isLicensed = PhotoEnhancerSDK.initialize(context, "YOUR_LICENSE_KEY")
    if (isLicensed) {
        PhotoEnhancerSDK.init(context) // Prefetch models
    }
}
```

### 3. Launch UI (3 Options)

<details open>
<summary><b>Option A: Plug & Play Compose UI</b> (Easiest)</summary>

Just drop our pre-built screen into your navigation graph.

```kotlin
PhotoEnhancerScreen(
    initialUri = userPickedUri, 
    onBack = { navController.popBackStack() },
    onNavigateToResult = { originalPath, enhancedPath ->
        // Proceed to your custom result screen
    }
)
```
</details>

<details>
<summary><b>Option B: Brand the UI (Theming)</b></summary>

Overwrite our UI with your own brand colors and text.

```kotlin
val myBrandTheme = SDKThemeConfig.Default.copy(
    primaryAccent = Color(0xFFFF5722),
    background = Color(0xFF121212),
    strings = SDKThemeConfig.Default.strings.copy(
        title = "My App Enhancer",
        buttonEnhance = "Make it HD ✦"
    )
)

PhotoEnhancerScreen(theme = myBrandTheme, onBack = { /* ... */ })
```
</details>

<details>
<summary><b>Option C: Headless API (100% Custom UI)</b></summary>

Build your own UI completely and use our AI engine in the background. You can let your users select the enhancement mode (Auto, Upscale Only, or Face Restore Only).

```kotlin
// Example: Process the image in an IO coroutine based on user selection
val enhancedBitmap = PhotoEnhancerSDK.processImageHeadless(
    context = context,
    bitmap = originalBitmap,
    mode = FaceEnhancementHelper.EnhanceMode.AUTO_ENHANCE // or UPSCALE, or RESTORE_FACE
) { progress ->
    // progress is a Float from 0.0 to 1.0
    // Update your custom UI progress bar
    runOnUiThread {
        customProgressBar.progress = (progress * 100).toInt()
        progressText.text = "Enhancing: ${(progress * 100).toInt()}%"
    }
}

if (enhancedBitmap != null) {
    // Show the result in your custom ImageView
    resultImageView.setImageBitmap(enhancedBitmap)
}
```
</details>

---

## 📱 Hardware & Device Support

The SDK leverages the device's neural processors (NPU/GPU) for heavy lifting. 

<table align="center" width="100%">
  <tr>
    <td width="50%" valign="top">
      <h3>✅ Supported Specs</h3>
      <ul>
        <li><b>OS:</b> Android 8.0 (API 26+)</li>
        <li><b>RAM:</b> Minimum <b>3GB</b> (4GB+ recommended)</li>
        <li><b>Arch:</b> <code>arm64-v8a</code> (Optimal) and <code>armeabi-v7a</code></li>
        <li><b>Runtime:</b> LiteRT / ONNX</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>⚠️ Limitations & Exclusions</h3>
      <ul>
        <li><b>Android Go / &lt;2GB RAM:</b> Will experience Out-Of-Memory (OOM) crashes on 4x upscaling.</li>
        <li><b>Legacy Arch:</b> <code>x86</code> and <code>mips</code> are not supported for production deployment.</li>
      </ul>
    </td>
  </tr>
</table>

> *Note: First-time usage requires a network connection to securely download the compressed AI models (~30MB). All subsequent usage is completely offline.*

---

## 💳 Pricing & Licensing

Get a commercial license tailored to your growth.

<div align="center">

| | **🌱 Indie License** | **🚀 Business License** |
|---|:---:|:---:|
| **Target** | Solo Developers / Startups | Agencies / Multiple Portfolios |
| **Price** | **$49 / month** | **$149 / month** |
| **Apps Supported** | 1 App Package | Unlimited Apps |
| **Processing Limits** | Unlimited On-Device | Unlimited On-Device |
| **Support** | Standard Email | Priority & Strategy |
| **Action** | [**Buy Indie →**](mailto:support.nsenterprise@gmail.com?subject=Indie%20License) | [**Buy Business →**](mailto:support.nsenterprise@gmail.com?subject=Business%20License) |

</div>

<br/>

### 🌍 How to Purchase (International)
We use **Paddle** for secure, global checkout (Card/PayPal).
1. Email **[support.nsenterprise@gmail.com](mailto:support.nsenterprise@gmail.com)** requesting a license.
2. You'll receive a secure Paddle checkout link.
3. Your License Key is delivered immediately upon payment.

### 🇧🇩 Local Purchase (Bangladesh - bKash)
1. Scan the QR code or Send Money to: **`01904891242`**
2. Send the BDT equivalent (e.g. $49 × Current Market Rate ৳).
3. Put your **Email** in the bKash Reference.
4. Email us your Transaction ID for instant activation.

<div align="center">
  <img src="./bkash_qr.jpeg" width="180" alt="bKash QR Code" style="border-radius: 12px; border: 2px solid #8B5CF6;"/>
</div>

---

## 📋 Changelog

### v1.0.6 — August 2026
- **New Models:** Replaced GFPGAN with our custom `NSRestore` (8.2MB) for superior face recovery.
- **New Upscaler:** Integrated `Real-FSRCNN` (47KB) for blazing fast 4x background upscaling.
- **Granular Controls:** Added `AUTO_ENHANCE`, `UPSCALE`, and `RESTORE_FACE` modes to give users fine-grained control over the enhancement pipeline.
- **Performance:** Drastic size reduction! Our previous GFPGAN (167 MB) and Real-ESRGAN (69 MB) models took up ~236 MB. Our new custom architecture is under **9 MB total** while delivering superior quality and much faster inference speed.
- **Quality Fixes:** Eliminated color distortion and "white blowout" artifacts in the upscaling pipeline by utilizing correct YCbCr space mapping and dynamic output buffer allocation.

### v1.0.5 — June 2026
- **Fix:** Internal SDK error messages (e.g. license/network diagnostics) no longer leak to end users as visible toasts or error text. All user-facing errors are now clean, friendly strings.
- **Fix:** Adaptive icon background updated to dark theme on sample app.

### v1.0.4 and earlier
- Initial public releases with GFPGAN + Real-ESRGAN integration, headless API, and full Compose theming support.

---

## ❓ FAQ

<details>
<summary><b>Do I need a Firebase or AWS account?</b></summary>
<br/>
No! The SDK handles its own internal security and model delivery. You don't need any <code>google-services.json</code> or cloud infrastructure.
</details>

<details>
<summary><b>How big is the SDK?</b></summary>
<br/>
The core SDK code is extremely lightweight (< 2MB). The AI models (~8.3MB total) are downloaded dynamically on the user's first interaction and stored in the app's private local storage, keeping your initial Play Store download size small.
</details>

<details>
<summary><b>Can I use this in a free app with ads?</b></summary>
<br/>
Yes. You can monetize your app however you want. The end-user never pays us—only you maintain the active developer license.
</details>

---

<div align="center">

**Built with ❤️ by [NS Enterprise](https://github.com/nsenterprise9865-stack)**

*Bangladesh 🇧🇩 • Powering beautiful Android apps with on-device AI*

[Contact Us](mailto:nsenterprise9865@gmail.com) • [Report an Issue](https://github.com/nsenterprisesdk/android-photo-enhancer-sdk/issues)

</div>
