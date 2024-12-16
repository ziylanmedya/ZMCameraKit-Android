# ZMCKit

ZMCKit is an Android library designed to simplify camera functionalities in your applications. With support for full-screen camera activities and programmatically configurable layouts, it provides a seamless experience for integrating Snap-like camera features.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
  - [Using Full-Screen Camera Activities](#using-full-screen-camera-activities)
  - [Using ZMCameraLayout Programmatically](#using-zmcameralayout-programmatically)
  - [Handling Previews](#handling-previews)
- [License](#license)

---

## Installation

### Step 1: Add the Repository

Add the following Maven repository to your project-level `build.gradle` file:

```groovy
allprojects {
    repositories {
        google()
        mavenCentral()
        maven {
            url "https://raw.githubusercontent.com/ziylanmedya/ZMCameraKit-Android/main/"
        }
    }
}
```

### Step 2: Add the Dependency

In your app-level `build.gradle` file, add the following dependency:

```groovy
dependencies {
    implementation 'com.ziylanmedya:zmckit:1.0.2' // Update version as necessary
}
```

---

## Usage

### Using Full-Screen Camera Activities

#### 1. **Show Single Product Camera Activity**

To launch a camera in a single product mode:

```kotlin
import com.ziylanmedya.zmckit.ZMCKitManager

ZMCKitManager.showProductActivity(
    context = this, 
    snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN, 
    partnerGroupId = BuildConfig.LENS_GROUP_ID, 
    lensId = BuildConfig.LENS_ID,
    cameraListener = object : ZMCKitManager.ZMCameraListener {
        override fun onImageCaptured(imageUri: Uri) {
            // Handle the captured image
        }

        override fun onLensChange(lensId: String) {
            // Handle lens change
        }

        override fun shouldShowDefaultPreview(): Boolean {
            return true // Default implementation
        }
    },
)
```

#### 2. **Show Group Camera Activity**

To launch a camera in group mode:

```kotlin
ZMCKitManager.showGroupActivity(
    context = this,
    snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
    partnerGroupId = BuildConfig.LENS_GROUP_ID,
    cameraListener = object : ZMCKitManager.ZMCameraListener {
        override fun onImageCaptured(imageUri: Uri) {
            // Handle the captured image
        }

        override fun onLensChange(lensId: String) {
            // Handle lens change
        }
    },
)
```

---

### Using ZMCameraLayout Programmatically

You can embed `ZMCameraLayout` in your own activity or fragment for more flexibility.

#### 1. **Single Product View Layout**

```kotlin
val cameraLayout = ZMCKitManager.createProductCameraLayout(
    context = this,
    snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
    partnerGroupId = BuildConfig.LENS_GROUP_ID,
    lensId = BuildConfig.LENS_ID,
    cameraListener = object : ZMCKitManager.ZMCameraListener {
        override fun onImageCaptured(imageUri: Uri) {
            // Handle the captured image
        }

        override fun onLensChange(lensId: String) {
            // Handle lens change
        }
    }
)
// Add the camera layout to your view hierarchy
findViewById<FrameLayout>(R.id.camera_container).addView(cameraLayout)
```

#### 2. **Group View Layout**

```kotlin
val cameraLayout = ZMCKitManager.createGroupCameraLayout(
    context = this,
    snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
    partnerGroupId = BuildConfig.LENS_GROUP_ID,
    cameraListener = object : ZMCKitManager.ZMCameraListener {
        override fun onImageCaptured(imageUri: Uri) {
            // Handle the captured image
        }

        override fun onLensChange(lensId: String) {
            // Handle lens change
        }
    }
)
// Add the camera layout to your view hierarchy
findViewById<FrameLayout>(R.id.camera_container).addView(cameraLayout)
```

---

### Handling Previews

If the `ZMCameraListener.shouldShowDefaultPreview()` method returns `true`, the preview is automatically displayed after capturing an image.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
