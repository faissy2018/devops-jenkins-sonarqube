//START-OF-SCRIPT
node {
    def SONARQUBE_HOSTNAME = '3.16.76.211'

    def GRADLE_HOME = tool name: 'gradle-4.10.2', type: 'hudson.plugins.gradle.GradleInstallation'
    sh "${GRADLE_HOME}/bin/gradle tasks"

    stage('prep') {
        git url: 'https://github.com/cloudacademy/devops-webapp.git'                
    }

    stage('build') {
        sh "/opt/gradle/gradle-4.7/bin build"
    }

    stage('sonar-scanner') {
      def sonarqubeScannerHome = tool name: 'sonarqube4', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
      withCredentials([string(credentialsId: 'sonarqubw', variable: 'JenkinsSonarqube')]) {
        sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://${SONARQUBE_HOSTNAME}:9000 -Dsonar.login=${JenkinsSonarqube -Dsonar.projectName=WebApp -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=src/main/ -Dsonar.tests=src/test/ -Dsonar.java.binaries=build/**/* -Dsonar.language=java"
      }
    }

}
//END-OF-SCRIPT
