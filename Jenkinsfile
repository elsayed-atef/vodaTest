pipeline {
    agent any
stages {
// stage ("Checkout") {
//    steps {
//    checkout scm
//    sh "chmod a+x ./gradlew"
//    }
//  }


stage ("Build clean") {
    steps {
   sh "chmod a+x ./gradlew"
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
        
        
 // stage ("Stage Archive") {
 //  steps {
    
     
  //tell Jenkins to archive the apks
  //archiveArtifacts artifacts: '**/*.apk', fingerprint: true
             
  //  }
  //  }
        
   stage("Sign"){
  steps {
    
        signAndroidApks (
          keyStoreId: "ee4398c7-62e0-4d8b-b4ae-e4bed74c1458",
          keyAlias: "key0",
          apksToSign: "**/*-unsigned.apk",
          
        )
    
  }
  }     
        
}
}
