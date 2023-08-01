pipeline {
    agent { label 'MAVEN_JDK' }
    triggers { pollSCM('H/30 * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/2023August/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('package') {
            tools { jdk 'JAVA_8_UBUNTU'}
            steps {
                sh 'mvn package'
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/TEST-*.xml'                 
            }
        }
    }
}