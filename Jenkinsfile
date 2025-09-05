pipeline {
    agent any

    stages {
    
        stage('SCM') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/sumijenkins/line_follower.git',
                        credentialsId: 'githubpat1'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                echo 'STM32 projesi Makefile ile build ediliyor...'
                withEnv(["PATH=C:\\Users\\simay\\CTOOLS-ARM\\bin;C:\\Users\\simay\\CTOOLS\\bin;${env.PATH}"]) {
                    bat 'make -f "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\line_follower_master\\makefile" all'
                }

            }
        }

        stage('Archive') {
            steps {
                echo 'Build artifactlari arşivleniyor...'
                archiveArtifacts artifacts: 'LineFollower.*', fingerprint: true
            }
        
        }
    }
    post {
        success {
            emailext(
                subject: "[SUCCESS] ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                Build başarılı!
                - Proje: ${env.JOB_NAME}
                - Build No: ${env.BUILD_NUMBER}
                - Son commit: ${env.GIT_COMMIT}

                Artefaktlar Jenkins'te arşivlendi.
                """,
                to: "smyysavas@gmail.com",
                attachLog: true
            )
        }
        failure {
            echo 'Build failured!'
        }
    }
}
