
# Generating APK and AAB for an Android App

This guide provides step-by-step instructions for generating an APK and AAB for an Android project and pushing it to GitHub.

## Prerequisites

Ensure you have the following installed:
- Android Studio (latest version)
- Java Development Kit (JDK)
- Android SDK
- Git

## Step 1: Open Your Project in Android Studio

1. Launch **Android Studio**.
2. Open your Android project.
3. Ensure your project is synchronized by selecting **File > Sync Project with Gradle Files**.

## Step 2: Generate APK

1. Click on **Build** in the top menu.
2. Select **Build Bundle(s) / APK(s) > Build APK(s)**.
3. Wait for the build process to complete.
4. Navigate to **`app/build/outputs/apk/debug/`** or **`app/build/outputs/apk/release/`**.
5. You will find the generated APK file.

### Generate Signed APK (For Production)

1. Go to **Build > Generate Signed Bundle/APK**.
2. Select **APK** and click **Next**.
3. Create or select an existing **Key Store**.
4. Enter the required credentials and select the build variant (**release** or **debug**).
5. Click **Finish** to generate the signed APK.
6. The APK will be found in `app/build/outputs/apk/release/`.

## Step 3: Generate AAB (Android App Bundle)

1. Click on **Build** in the top menu.
2. Select **Build Bundle(s) / APK(s) > Build Bundle(s)**.
3. Wait for the build process to complete.
4. Navigate to **`app/build/outputs/bundle/release/`**.
5. You will find the generated `.aab` file.

## Step 4: Push to GitHub

### Initialize Git (if not already done)

```sh
cd /path/to/your/project
git init
git remote add origin https://github.com/yourusername/your-repository.git
```

### Add APK and AAB to GitHub

```sh
git add app/build/outputs/apk/release/*.apk
git add app/build/outputs/bundle/release/*.aab
git commit -m "Added APK and AAB files"
git push origin main
```

## Step 5: Add `.gitignore` to Exclude Unnecessary Files

Create a `.gitignore` file in the root directory and add the following lines:

```
/app/build/
*.apk
*.aab
```

This ensures that only the necessary files are committed.

## Step 6: Verify the Commit on GitHub

1. Open GitHub and navigate to your repository.
2. Check that the APK and AAB files are successfully pushed.

## Step 7: Share the APK

1. Go to the repository on GitHub.
2. Click on **Releases** (if you want to create a new release for distribution).
3. Attach the APK and AAB files.
4. Share the download link.

---

Now, your APK and AAB are successfully generated and pushed to GitHub! 🎉

