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
        passwordVariable: 'MVN_PASSWORD', 
        usernameVariable: 'MVN_USERNAME')]) {

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

  stage('Post') {
    jacoco()
    junit 'lib/build/test-results/test/*.xml'
    def pmd = scanForIssues tool: [$class: 'Pmd'], pattern: 'lib/build/reports/pmd/*.xml'
    publishIssues issues: [pmd]
  }
  
}