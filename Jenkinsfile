pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/sumijenkins/line_follower.git', credentialsId: 'github-https'
            }
        }

        stage('Build') {
            steps {
                echo 'Building STM32 project...'
                bat '"C:\\ST\\STM32CubeIDE\\stm32cubeide.exe" -nosplash -application org.eclipse.cdt.managedbuilder.core.headlessbuild -data "%WORKSPACE%" -import "%WORKSPACE%" -build LineFollower'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/Debug/*.elf, **/Debug/*.bin', allowEmptyArchive: true
            }
        }
    }
}
