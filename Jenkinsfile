pipeline {
    agent any
stages {
stage ("Checkout") {
    steps {
    checkout scm
    sh "chmod a+x ./gradlew"
    }
  }


stage ("Build clean") {
    steps {
   
    // Build the app
    sh "./gradlew clean"
       
    }
    }
        
 stage ("Build package") {
    steps {
        // Build the app
    sh "./gradlew assembleDebug"
       
    }
    }
        stage ("Build release package") {
    steps {
        // Build the app
    sh "./gradlew assembleRelease"
       
    }
    }
        
        
  stage ("Stage Archive") {
    steps {
    
     
  //tell Jenkins to archive the apks
  archiveArtifacts artifacts: '**/*.apk', fingerprint: true
             
    }
    }
        
   stage("Sign"){
  steps {
    
        signAndroidApks (
          keyStoreId: "androidtest.jks",
          keyAlias: "key0",
          apksToSign: "**/*-unsigned.apk",
          // uncomment the following line to output the signed APK to a
          separate directory as described above
          // signedApkMapping: [ $class: UnsignedApkBuilderDirMapping ],
        )
    
  }
  }     
        
}
}
