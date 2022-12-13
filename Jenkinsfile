node {
  // Start Stages
  stage('Clone') {
      dir('.') {
          git branch: 'main', credentialsId: 'github_com', url: 'git@github.com:jvalentino/example-java-gradle-jenkins-scripted.git'
      }    
      sh 'ls -la'
  }       
}