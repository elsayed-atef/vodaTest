stage ("Build") {
    // Check environment (We define ANDROID_HOME in node settings)
    if (env.ANDROID_HOME == null || env.ANDROID_HOME == "") error "ANDROID_HOME not defined"
    if (env.JAVA_HOME == null || env.JAVA_HOME == "") error "JAVA_HOME not defined"

    // Default parameters (In case file is unreadable or missing)
    def d = [versionName: 'unversioned', versionCode: '1']
    // Read properties from file (Right now we only keep versionName and VersionCode there)
    HashMap<String, Object> props = readProperties defaults: d, file: 'gradle.properties'
    // Optional user input to override parameters
    def userInput
    try {
      timeout(time: 60, unit: 'SECONDS') {
        userInput = input( id:'userInput', message: 'Override build parameters?', parameters: [
          string(defaultValue: props.versionName, description: 'App version (without build number)', name: 'versionName'),
          string(defaultValue: props.versionCode, description: 'Version code (for GooglePlay Store)', name: 'versionCode')
        ])
        logOverrides(userInput, props, "manual_override.log")
        props.putAll(userInput)
        echo("Parameters entered : ${userInput.toString()}")
      }
    } catch (Exception e) {
      echo "User input timed out or cancelled, continue with default values"
    }
    // Change build name to current app version
    currentBuild.displayName = "${props.versionName}.${env.BUILD_NUMBER}"
    // Common build arguments
    env.COMMON_BUILD_ARGS = " -PBUILD_NUMBER=${env.BUILD_NUMBER} -PBRANCH_NAME=${env.BRANCH_NAME}" +
      " -PversionName=${props.versionName} -PversionCode=${props.versionCode}"

    // Build the app
    sh "./gradlew clean"
        sh """./gradlew assembleDebug ${env.COMMON_BUILD_ARGS}
              ./gradlew assembleRelease ${env.COMMON_BUILD_ARGS}
           """
    }

    stage('Save artifacts and publish') {
      // Save build results
      step([$class: 'ArtifactArchiver', artifacts: "**/*.apk", excludes: "**/*unaligned.apk", fingerprint: true])
      // Push changes and tag
      gitLib.pushSSH(commitMsg: "Jenkins build #${env.BUILD_NUMBER} from ${env.BRANCH_NAME}", 
        tagName: "build/${env.BRANCH_NAME}/${env.BUILD_NUMBER}", files: ".", config: true);
      sendEmails();
    }

  stage ('Crashlytics register') {
    sh """./gradlew crashlyticsUploadDistributionDebug ${env.COMMON_BUILD_ARGS}
          ./gradlew crashlyticsUploadDistributionRelease ${env.COMMON_BUILD_ARGS}
       """
  }
}

stage ('Release') {
  try {
    input 'Do we release this build?'
    node {
      echo "Push Release tag"
      def date  = sh(returnStdout: true, script: 'date -u +%Y%m%d').trim()// = new Date().format('yyyyMMdd') // apparently we can't use Date here, not a problem
      gitLib.pushSSH(tagName: "release-${date}", commitMsg: "Jenkins promoted");
      // Do your release stuff
    }
  } catch (Exception e) {
    echo "Release cancelled"
  }
}

