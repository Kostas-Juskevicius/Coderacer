pipeline {
    agent { label 'agent-1' }

    environment {
        MAVEN_HOME = tool 'maven'
        SONARQUBE_SCANNER_HOME = tool 'sonar-scanner'
        JAVA_HOME = tool 'jdk-17'
        SONARQUBE_ENV = 'local-sonarqube'
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Kostas-Juskevicius/Coderacer', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat '''
                    set JAVA_HOME=%JAVA_HOME%
                    set PATH=%JAVA_HOME%\\bin;%PATH%
                    call "%MAVEN_HOME%\\bin\\mvn" clean compile -DskipTests
                '''
            }
        }

        // stage('Unit Test') {
        //     steps {
        //         bat '''
        //             set JAVA_HOME=%JAVA_HOME%
        //             set PATH=%JAVA_HOME%\\bin;%PATH%
        //             call "%MAVEN_HOME%\\bin\\mvn" test
        //         '''
        //     }
        // }

        // stage('Integration Test') {
        //     steps {
        //         bat '''
        //             set JAVA_HOME=%JAVA_HOME%
        //             set PATH=%JAVA_HOME%\\bin;%PATH%
        //             call "%MAVEN_HOME%\\bin\\mvn" verify -DskipUnitTests=true
        //         '''
        //     }
        // }

        stage('Static Analysis') {
            steps {
                withSonarQubeEnv('local-sonarqube') {
                    bat '''
                        set JAVA_HOME=%JAVA_HOME%
                        set PATH=%JAVA_HOME%\\bin;%PATH%
                        call "%MAVEN_HOME%\\bin\\mvn" sonar:sonar ^
                        -Dsonar.projectKey=Kostas-Jusk_WebGoat ^
                        -Dsonar.host.url=%SONAR_HOST_URL%
                    '''
                }
            }
        }

        // stage('Package') {
        //     steps {
        //         bat '''
        //             set JAVA_HOME=%JAVA_HOME%
        //             set PATH=%JAVA_HOME%\\bin;%PATH%
        //             call "%MAVEN_HOME%\\bin\\mvn" package -DskipTests
        //         '''
        //     }
        // }

        // stage('Dependency Updates (Renovate)') {
        //     steps {
        //         withCredentials([string(credentialsId: '72423783-530c-4723-8815-ec9f0461e727', variable: 'RENOVATE_TOKEN')]) {
        //             // Note: generating a report in a file is apparently an experimental feature.
        //             // Also, if no report type is set, it isn't generated and may be pieced together from logs.
        //             bat '''
        //                 set "NODE_HOME=%WORKSPACE%\\..\\..\\..\\..\\node-v22.20.0-win-x64"
        //                 set "PATH=%NODE_HOME%;%PATH%"
        //                 set "LOG_LEVEL=info"
        //                 set "RENOVATE_REPORT_TYPE=file"
        //                 set "RENOVATE_REPORT_PATH=renovate_summary.json"

        //                 npx renovate --require-config=false --platform=github --token=%RENOVATE_TOKEN% Kostas-Jusk/WebGoat
        //             '''
        //         }
        //     }
        // }
    }
}
