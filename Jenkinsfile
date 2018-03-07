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
          keyStoreId: "a364b1be-c6c1-4578-aac5-83ef1ab509a4",
          keyAlias: "key0",
          apksToSign: "**/*-unsigned.apk",
          
        )
    
  }
  }     
        
}
}
