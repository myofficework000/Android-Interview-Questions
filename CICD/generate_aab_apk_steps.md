//Define the workflow name, which appears in GitHub Actions.
name: Generated APK AAB (Upload - Create Artifact To Github Action)

//Environment variables that can later be used in artifact naming
env:
  # The name of the main module repository
  main_project_module: app

//Triggering conditions, we can trigger on push to the master branch
//or trigger manually from the Actions tab
on:

  push:
    branches:
      - 'master/**'

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

//Trigger events, we want to trigger some jobs,
//and in it we have the build job which runs on ubuntu(linux) and follows all the steps below
jobs:
  build:

    runs-on: ubuntu-latest

    steps:
//fetch latest code of the repository, specify this is for version 4
      - uses: actions/checkout@v4
      
//create a variable date_today and specify the format, then store this as an environment variable
      # Set Current Date As Env Variable
      - name: Set current date as env variable
        run: echo "date_today=$(date +'%Y-%m-%d')" >> $GITHUB_ENV

//extract the repo name from github.repository, and store this as an environment variable
//use an awk command that processes text using a field separator (-F '/')
//-F '/' → Specifies that fields in the input should be split using / as the delimiter.
//'{print $2}' → Extracts and prints the second field from the split input.
//the repo name on github returns a string like my-github-user/my-android-project
//we need to filter out the username only keep the repo name
      # Set Repository Name As Env Variable
      - name: Set repository name as env variable
        run: echo "repository_name=$(echo '${{ github.repository }}' | awk -F '/' '{print $2}')" >> $GITHUB_ENV

//Install Java 17 (Zulu) and enables Gradle caching to speed up builds.
      - name: Set Up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'zulu' # See 'Supported distributions' for available options
          java-version: '17'
          cache: 'gradle'

//give the permission to use gradlew
      - name: Change wrapper permissions
        run: chmod +x ./gradlew

//run all unit tests using gradlew command
      # Run Tests Build
      - name: Run gradle tests
        run: ./gradlew test

//compile the project
      # Run Build Project
      - name: Build gradle project
        run: ./gradlew build

//crate a bebug APK
      # Create APK Debug
      - name: Build apk debug project (APK) - ${{ env.main_project_module }} module
        run: ./gradlew assembleDebug
        
//create a release APK
      # Create APK Release
      - name: Build apk release project (APK) - ${{ env.main_project_module }} module
        run: ./gradlew assemble

//build an Android App Bundle(AAB) for play store deployment
      # Create Bundle AAB Release
      # Noted for main module build [main_project_module]:bundleRelease
      - name: Build app bundle release (AAB) - ${{ env.main_project_module }} module
        run: ./gradlew ${{ env.main_project_module }}:bundleRelease

//upload the three kind of generated files to Github Actions
      # Upload Artifact Build
      # Noted For Output [main_project_module]/build/outputs/apk/debug/

//store files generated(artifacts) during workflow exectuion, and specify where we wanna store it and what we wanna name it
//outer name is the step name, inner name is for this particular artifact,
//it dynamically generated with some exsiting environment variables,
//it will appear in the GithubActions "Artifacts" tab
      - name: Upload APK Debug - ${{ env.repository_name }}
        uses: actions/upload-artifact@v4
        with:
          name: ${{ env.date_today }} - ${{ env.playstore_name }} - ${{ env.repository_name }} - APK(s) debug generated
          path: ${{ env.main_project_module }}/build/outputs/apk/debug/

//similar store artifact process, just for release APK 
      # Noted For Output [main_project_module]/build/outputs/apk/release/
      - name: Upload APK Release - ${{ env.repository_name }}
        uses: actions/upload-artifact@v4
        with:
          name: ${{ env.date_today }} - ${{ env.playstore_name }} - ${{ env.repository_name }} - APK(s) release generated
          path: ${{ env.main_project_module }}/build/outputs/apk/release/

//similar store artifact process, just for AAB
      # Noted For Output [main_project_module]/build/outputs/bundle/release/
      - name: Upload AAB (App Bundle) Release - ${{ env.repository_name }}
        uses: actions/upload-artifact@v4
        with:
          name: ${{ env.date_today }} - ${{ env.playstore_name }} - ${{ env.repository_name }} - App bundle(s) AAB release generated
          path: ${{ env.main_project_module }}/build/outputs/bundle/release/

----------------------------------------------------------------------------
if we also wanna add sonarcube for coverage report and maven for packaging:

first, add this two env
SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
SONAR_HOST_URL: 'https://sonarcloud.io'  # Change if using a self-hosted SonarQube server

then add the steps below
      # Run Tests and Generate Coverage Report
      - name: Run gradle tests with coverage
        run: ./gradlew test jacocoTestReport

      # SonarQube Scan
      - name: SonarQube Analysis
        run: ./gradlew sonarqube -Dsonar.login=${{ secrets.SONAR_TOKEN }} -Dsonar.host.url=${{ env.SONAR_HOST_URL }}

      # Run Maven Package
      - name: Set up Maven
        uses: actions/setup-java@v4
        with:
          distribution: 'zulu'
          java-version: '17'
          cache: 'maven'

      - name: Build with Maven
        run: mvn clean package

So here instead of run test with gradlew directly, we run with jacocoTestReport, and integrate sonarqube analysis
It analyzes your source code for potential issues, including:
·Bugs (e.g., null pointer dereferences, memory leaks)
·Code smells (e.g., duplicated code, long methods)
·Vulnerabilities (e.g., security flaws like SQL injection)

instead of directly use build command, we set up maven and delegate maven to to handle the build and compilation process.
