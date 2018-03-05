pipeline {
    agent any
    stages {
stage ("Checkout") {
    steps {
    checkout scm
    sh "chmod a+x ./gradlew"
    }
  }


stage ("Build") {
    steps {
    // Common build arguments
   // env.COMMON_BUILD_ARGS = " -PBUILD_NUMBER=${env.BUILD_NUMBER} -PBRANCH_NAME=${env.BRANCH_NAME}" +
     // " -PversionName=${props.versionName} -PversionCode=${props.versionCode}"

    // Build the app
    sh "./gradlew --refresh-dependencies clean assemble"
       
    }
    }
}
}
