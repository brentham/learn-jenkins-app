// pipeline {
//     agent any

//     stages {
//         stage('w/ docker') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 sh '''
//                     ls -la
//                     npm ci
//                     npm run build
//                     ls -la
//                 '''
//             }
//         }

//         stage('Test') {
//             steps{
//                 echo 'Test Stage'
                
//             }
//         }
//     }
// }



pipeline {
    agent any

    environment {
        NEXUS_URL = 'https://nexus.techworldplus.xyz'
        NEXUS_REPO = 'nexus-postboard-client'
        NEXUS_CREDENTIALS_ID = 'nexusCreds2'


        REACT_APP_DIR = 'src' // Your React app directory
        // SONARQUBE_SERVER = 'https://sonarqube.techworldplus.xyz/' // Jenkins SonarQube server name
        SONARQUBE_SERVER = 'jenkins-sonar' // Jenkins SonarQube server name
        SONAR_PROJECT_KEY = 'brentham_learn-jenkins-app_29b39040-c647-428e-bc72-16ef946b7c83'
        SONAR_PROJECT_NAME = 'learn-jenkins-app'
        SONAR_PROJECT_VERSION = '1.0'
        DOCKER_IMAGE = 'brent/learn-jenkins-app:latest'
    }

    stages {
        stage('Install Dependencies') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
        //     steps {
        //         sh '''
        //             ls -la
        //             npm ci
        //             ls -la
        //         '''
        //     }
        // }

        // stage('Run Tests') {
        //     agent {
        //         docker {
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             npm test -- --watchAll=false
        //         '''
        //     }
        // }


        stage('SonarQube Scan') {
            agent {
                docker {
                    image 'sonarsource/sonar-scanner-cli'
                    reuseNode true
                }
            }
            steps {
                withSonarQubeEnv(SONARQUBE_SERVER) {
                        sh '''
                            sonar-scanner -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                                -Dsonar.projectName=${SONAR_PROJECT_NAME} \
                                -Dsonar.projectVersion=${SONAR_PROJECT_VERSION} \
                                -Dsonar.sources=./src \
                                -Dsonar.working.directory=.scannerwork
                            ls -la
                            ls -la .scannerwork
                        '''
                }
            }
        }

        // stage('Build React App') {
        //     agent {
        //         docker {
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             npm run build
        //         '''
        //     }
        // }

    //     stage('Dockerize React App') {
    //         steps {
    //             script {
    //                 docker.build("${DOCKER_IMAGE}", "${REACT_APP_DIR}").push()
    //             }
    //         }
    //     }

        stage('Publish SonarQube Artifacts to Nexus') {
            steps {
                script {
                    // Archive the SonarQube scan artifacts
                    archiveArtifacts artifacts: '**/.scannerwork/**', allowEmptyArchive: true

                    // Publish the scan reports to Nexus
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'https',
                        nexusUrl: "${NEXUS_URL}",
                        groupId: 'com.yourcompany.reactapp',
                        version: "${SONAR_PROJECT_VERSION}",
                        repository: "${NEXUS_REPO}",
                        credentialsId: "${NEXUS_CREDENTIALS_ID}",
                        artifacts: [
                            [
                                artifactId: 'sonarqube-report',
                                classifier: '',
                                file: ".scannerwork/report-task.txt",
                                type: 'txt'
                            ]
                        ]
                    )
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after the build
        }
    }
}