pipeline {
    agent any

    environment {
        VER = getGitVersion()
    }

    stages {
        stage('Hello') {
            steps {
                script {
                    X = 123
                }
                echo "Hello World $VER"
                sh 'echo s expand $VER'
                sh "echo j expand $VER"
            }
        }

        stage('verify') {
            steps {
                sh 'env'
            }
        }
    }
}

def getGitVersion() {
    script {
        gitVersion = sh(returnStdout: true, script: "git describe --tag --always | head -n 1 | tr -d 'release_'").trim()
        if ('nope' ==~ /(release.*)/) {
            return gitVersion;
        } else {
            timestamp = new Date().format("yyyyMMddHHmmss", TimeZone.getTimeZone('UTC'))
            return "0.${timestamp}-r${gitVersion}"
        }

    }
}
