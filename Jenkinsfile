pipeline {
    agent any

    stages {
    
        stage('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/sumijenkins/line_follower.git', credentialsId: 'githubpat1'
            }
        }

        stage('Build') {
            steps {
                echo 'STM32 projesi Makefile ile build ediliyor...'
                bat '"C:/Users/simay/CTOOLS/bin/make.exe" -C "%WORKSPACE%/Debug"'
            }
        }

        stage('Archive') {
            steps {
                echo 'Build artifactlari arşivleniyor...'
                archiveArtifacts artifacts: 'Debug/*.elf, Debug/*.bin', allowEmptyArchive: true
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
