pipeline {
    agent jenkins-andriod-slave1
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
   // sh "./gradlew clean --info "
       
    }
    }
        
 stage ("Build package") {
    steps {
        // Build the app
    sh "./gradlew -Dhttps.proxyHost=10.102.0.3 -Dhttps.proxyPort=3128 assembleDebug"
       
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
          keyStoreId: "testSign",
          keyAlias: "key0",
          apksToSign: "**/*-unsigned.apk",
          
        )
    
  }
  }     
        
}
}
