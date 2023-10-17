// node {
//     def myGradleContainer = docker.image('gradle:jdk8-alpine')
//     myGradleContainer.pull()

//     stage('prep') {
//         git url: 'https://github.com/kri-sh27/gs-gradle.git'
//         sh 'docker --version'
//     }

//     stage('build') {
//       myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
//         sh 'cd complete && /opt/gradle/bin/gradle build'
//       }
//     }

//     stage('sonar-scanner') {
//       def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
//       withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
//         sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=gs-gradle -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=complete/src/main/ -Dsonar.tests=complete/src/test/ -Dsonar.language=java -Dsonar.java.binaries=."
//       }
//     }
// }

// node {
//     def myGradleContainer = docker.image('gradle:jdk8-alpine')
//     myGradleContainer.pull()

//     stage('prep') {
//         git url: 'https://github.com/kri-sh27/gs-gradle.git'
        
//         // Check Docker version
//         docker.withTool('Docker') {
//             sh 'docker --version'
//         }
//     }

//     stage('build') {
//         myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
//             sh 'cd complete && /opt/gradle/bin/gradle build'
//         }
//     }

//     stage('sonar-scanner') {
//         def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
//         withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
//             sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=gs-gradle -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=complete/src/main/ -Dsonar.tests=complete/src/test/ -Dsonar.language=java -Dsonar.java.binaries=."
//         }
//     }
// }

node {
    stage('prep') {
    // Install Docker without superuser privileges
    sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
    sh 'sh get-docker.sh'
    sh 'docker --version'

    def myGradleContainer = docker.image('gradle:jdk8-alpine')
    myGradleContainer.pull()

    git url: 'https://github.com/kri-sh27/gs-gradle.git'
}


    stage('build') {
        myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
            sh 'cd complete && /opt/gradle/bin/gradle build'
        }
    }

    stage('sonar-scanner') {
        def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
            sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=gs-gradle -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=complete/src/main/ -Dsonar.tests=complete/src/test/ -Dsonar.language=java -Dsonar.java.binaries=."
        }
    }
}
