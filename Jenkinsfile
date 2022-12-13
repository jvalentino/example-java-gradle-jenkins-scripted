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
  
}