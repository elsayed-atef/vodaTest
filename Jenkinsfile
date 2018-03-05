pipeline {
    stages {
stage ("Checkout") {
    checkout scm
    sh "chmod a+x ./gradlew"
  }


stage ("Build") {
    
    // Common build arguments
    env.COMMON_BUILD_ARGS = " -PBUILD_NUMBER=${env.BUILD_NUMBER} -PBRANCH_NAME=${env.BRANCH_NAME}" +
      " -PversionName=${props.versionName} -PversionCode=${props.versionCode}"

    // Build the app
    sh "./gradlew clean"
        sh """./gradlew assembleDebug ${env.COMMON_BUILD_ARGS}
              ./gradlew assembleRelease ${env.COMMON_BUILD_ARGS}
           """
    }
}
}
