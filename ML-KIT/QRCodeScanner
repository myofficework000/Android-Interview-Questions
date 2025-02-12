1. Add the dependencies for camerax and ml-kit
  dependencies {
    implementation("com.google.mlkit:barcode-scanning:17.2.0")
    implementation("androidx.camera:camera-core:1.3.0")
    implementation("androidx.camera:camera-camera2:1.3.0")
    implementation("androidx.camera:camera-lifecycle:1.3.0")
    implementation("androidx.camera:camera-view:1.3.0")
  }
------------------------------------------------------------
2. Add camera permissions in manifest
  
  <uses-feature
          android:name="android.hardware.camera"
          android:required="false" />
  <uses-permission android:name="android.permission.CAMERA" />
------------------------------------------------------------
3. Declare camerax usage in manifest and create the path file under res

  <provider
      android:name="androidx.core.content.FileProvider"
      android:authorities="${applicationId}.fileprovider"
      android:grantUriPermissions="true"
      android:exported="false">
      <meta-data
          android:name="android.support.FILE_PROVIDER_PATHS"
          android:resource="@xml/file_paths" />
  </provider>
  
  <?xml version="1.0" encoding="utf-8"?>
  <paths xmlns:android="http://schemas.android.com/apk/res/android">
      <external-path
          name="external_files"
          path="." />
  </paths>
------------------------------------------------------------
4. Create a camera preview in the screen
------------------------------------------------------------
5. Modify the camera setup to include ML Kit's BarcodeScanner
  implement the BarCodeScanner composable function with android view
  implement the processImageProxy method
------------------------------------------------------------
6. Display the scanned result in UI
------------------------------------------------------------
7. Use the screen in mainactivity, also ensure the run time permission of camera
  
