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
        
        
        
  stage ("After Build") {
    steps {
    
    sh "echo 'after build'"
       
    }
    }
        
        
        
}
}
