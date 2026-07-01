<div align="center">

# GlassUi SDK

**High-Performance, Real-Time Glassmorphism & Blur Engine for Android**

<img src="https://img.shields.io/badge/Version-2.0-blue.svg" alt="Version 2.0" /> <img src="https://img.shields.io/badge/API-21%2B-brightgreen.svg" alt="API 21+" /> <img src="https://img.shields.io/badge/Build-Passing-brightgreen.svg" alt="Build Status" /> <img src="https://img.shields.io/badge/License-Apache%202.0-orange.svg" alt="License" />

</div>

---

## Overview

**GlassUi** is an enterprise-grade Glassmorphism and Blur Engine tailored for modern Android applications. Powered by a highly optimized native C++ ultra-fast box blur algorithm, it delivers 60fps seamless rendering with multi-stop cubic fading, noise texturing, and dynamic bounce effects without compromising main thread performance.

## Core Capabilities

* **Real-Time Native Blur:** C++ powered blur engine for zero-lag rendering.
* **Multi-Stop Cubic Fade:** Eliminates harsh cut-lines for seamless shadow integration.
* **Dynamic Noise Engine:** Built-in grain texture generation for an authentic frosted glass look.
* **Interactive Bounce:** Optional fluid scale animations triggered on touch events.
* **Gradient Borders:** High-fidelity rim lighting around the glass boundaries.
* **Fully Customizable:** Comprehensive control over blur radius, corner radius, overlays, and noise via XML or Code.

---

## Installation

GlassUi is distributed as a proprietary, closed-source `.aar` binary. Follow these steps to integrate it into your Android project.

### 1. Place the Binary
Download `GlassUi-2.0.aar` from the releases section and place it inside your project's `app/libs/` directory. Create the `libs` folder if it does not exist.

### 2. Configure Dependencies
Add the following to your `app` level `build.gradle` or `build.gradle.kts` file:

**Kotlin DSL (build.gradle.kts):**
```kotlin
dependencies {
    // Core GlassUi SDK
    implementation(files("libs/GlassUi-2.0.aar"))
    
    // Required standard dependencies
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.appcompat:appcompat:1.6.1")
}
```

**Groovy (build.gradle):**
```groovy
dependencies {
    // Core GlassUi SDK
    implementation files('libs/GlassUi-2.0.aar')
}
```

> **Note:** Sync your project with Gradle files after adding the dependency.

---

## Implementation Guide

### 1. XML Layout Setup

Utilize `GlassUi` as a standard `FrameLayout`. Embed your child views directly inside it.

```xml
<com.glass.ui.GlassUi
    android:id="@+id/glassContainer"
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:layout_margin="16dp"
    app:blurRadius="40"
    app:glassCornerRadius="24dp"
    app:overlayColor="#33FFFFFF"
    app:drawBorder="true"
    app:enableNoise="true"
    app:enableBounce="true"
    app:topEdgeFadeColor="@android:color/transparent">

    <TextView 
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center" 
        android:text="Glassmorphism UI" 
        android:textColor="@android:color/white" 
        android:textSize="20sp" 
        android:textStyle="bold"/>

</com.glass.ui.GlassUi>
```

### 2. View Target Registration (Required)

The SDK requires a target background view to apply the blur calculations. 

**Method A: XML Attribute (Recommended)**
Assign an ID to your root background layout (e.g., an `ImageView` or `ConstraintLayout`) and link it directly in your XML:
```xml
app:targetViewId="@+id/mainBackgroundView"
```

**Method B: Programmatic Binding**
```java
GlassUi glassView = findViewById(R.id.glassContainer);
View backgroundView = findViewById(R.id.mainBackgroundView);

// Bind the background view to the glass rendering engine
glassView.setTargetView(backgroundView);
```

### 3. Runtime Property Management

Properties can be mutated dynamically at runtime for responsive UI updates:

```java
GlassUi glassView = findViewById(R.id.glassContainer);

glassView.setBlurRadius(50);
glassView.setGlassCornerRadius(60f);
glassView.setOverlayColor(Color.parseColor("#4D000000"));
glassView.setEnableNoise(false);
glassView.setDrawBorder(true);
glassView.setEnableBounce(true);
```

---

## XML Attributes Reference

| Attribute | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `app:targetViewId` | reference | `View.NO_ID` | Binds the target background view ID for blur processing. |
| `app:blurRadius` | integer | `30` | Intensity of the native C++ box blur algorithm. |
| `app:glassCornerRadius` | dimension | `0dp` | Corner rounding radius of the glass component. |
| `app:overlayColor` | color | `#33FFFFFF` | Color tint applied over the blurred background. |
| `app:drawBorder` | boolean | `true` | Enables dynamic gradient rim lighting border. |
| `app:enableNoise` | boolean | `true` | Overlays a hardware-accelerated grain texture. |
| `app:enableBounce` | boolean | `false` | Enables physical spring-scale animation on touch. |
| `app:topEdgeFadeColor`| color | `transparent`| Applies a seamless multi-stop cubic gradient fade. |
| `app:glassEnabled` | boolean | `true` | Master toggle to enable or disable rendering operations. |

---

## Security and Minification

This SDK binary is pre-processed and obfuscated. No additional ProGuard or R8 rules are required on the consumer module. The public API remains preserved and safe for production-grade shrinking.
