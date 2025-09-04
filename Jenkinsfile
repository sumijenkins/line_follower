pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/sumijenkins/line_follower.git', credentialsId: 'sumijenkins/******'
            }
        }

        stage('Build') {
            steps {
                echo 'STM32 projesi Makefile ile build ediliyor...'
                bat 'mingw32-make -C "%WORKSPACE%"'
            }
        }

        stage('Archive') {
            steps {
                echo 'Build artifactları arşivleniyor...'
                archiveArtifacts artifacts: '**/Debug/*.elf, **/Debug/*.bin', allowEmptyArchive: true
            }
        
        }
    }
}
