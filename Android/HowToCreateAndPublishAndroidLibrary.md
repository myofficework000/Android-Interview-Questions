
# Steps to Create and Publish a Library Remotely

This guide outlines the steps to create an Android library and publish it to a remote Maven repository (e.g., GitHub Packages, Maven Central, or a private repository).

---

## 1. **Create a New Android Library Module**

1. Open your Android project in Android Studio.
2. Go to `File > New > New Module`.
3. Select `Android Library` and click `Next`.
4. Provide a name for your library (e.g., `StylishSnackbar`).
5. Click `Finish` to create the library module.

---

## 2. **Write Your Library Code**

1. Navigate to the newly created module (`StylishSnackbar`).
2. Write your library code in the `src/main/java` or `src/main/kotlin` directory.
3. Add any necessary dependencies in the `build.gradle` file of the library module.

Example `build.gradle` for the library:

```kotlin
plugins {
    id("com.android.library")
    id("org.jetbrains.kotlin.android")
    id("maven-publish") // Add this plugin for publishing
}

android {
    namespace = "com.example.stylishsnackbar"
    compileSdk = 34

    defaultConfig {
        minSdk = 24
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = false
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }
    kotlinOptions {
        jvmTarget = "17"
    }
}

dependencies {
    implementation("androidx.compose.ui:ui:1.5.4")
    implementation("androidx.compose.material:material:1.5.4")
    implementation("androidx.compose.foundation:foundation:1.5.4")
    implementation("androidx.compose.ui:ui-tooling-preview:1.5.4")
}

publishing {
    publications {
        register<MavenPublication>("release") {
            groupId = "com.example"
            artifactId = "stylishsnackbar"
            version = "1.0.0"

            afterEvaluate {
                from(components["release"])
            }
        }
    }
}

Step 3: Configure Publishing
Add the maven-publish plugin to your library's build.gradle file (as shown above).

Configure the publishing block with your library's groupId, artifactId, and version.

Step 4: Publish to a Remote Repository
Option 1: Publish to GitHub Packages
Generate a GitHub Personal Access Token (PAT) with the write:packages scope.

Add the following to your build.gradle file:

publishing {
    repositories {
        maven {
            name = "GitHubPackages"
            url = uri("https://maven.pkg.github.com/OWNER/REPOSITORY")
            credentials {
                username = project.findProperty("gpr.user") ?: System.getenv("GITHUB_USERNAME")
                password = project.findProperty("gpr.key") ?: System.getenv("GITHUB_TOKEN")
            }
        }
    }
}


Replace OWNER with your GitHub username and REPOSITORY with your repository name.

Add your GitHub credentials to your gradle.properties file or environment variables:

gpr.user=your_github_username
gpr.key=your_github_token

Run the following command to publish:

./gradlew publish
