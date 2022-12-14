node {
  
  stage('Clone') {
      dir('.') {
          git branch: 'main', credentialsId: 'github_com', url: 'git@github.com:jvalentino/example-java-gradle-jenkins-scripted.git'
      }    
  }       

  stage('Build') {
      withGradle {
        sh './gradlew clean build --stacktrace -i'
      }  
  }   

  stage('Publish') {
     withCredentials([usernamePassword(
        credentialsId: 'github-publish-maven', 
        passwordVariable: 'MVN_USERNAME', 
        usernameVariable: 'MVN_PASSWORD')]) {

        withGradle {
          sh """
            ./gradlew -i --stacktrace publish \
                -PMVN_USERNAME=${MVN_USERNAME} \
                -PMVN_PASSWORD=${MVN_PASSWORD} \
                -PMVN_VERSION=1.${BUILD_NUMBER}
          """
        }  
     }
  }  
  
}