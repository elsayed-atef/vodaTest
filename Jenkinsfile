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
          keyStoreId: "207cbd6a-f7c7-4178-b1ab-ee8b0533675e",
          keyAlias: "key0",
          apksToSign: "**/*-unsigned.apk",
          
        )
    
  }
  }     
        
}
}
