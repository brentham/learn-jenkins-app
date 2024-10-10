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




// pipeline {
//     agent any

//     environment {
//         REACT_APP_DIR = 'src' // Your React app directory
//         SONARQUBE_SERVER = 'https://sonarqube.techworldplus.xyz/' // Jenkins SonarQube server name
//         SONAR_PROJECT_KEY = 'brentham_learn-jenkins-app_29b39040-c647-428e-bc72-16ef946b7c83'
//         SONAR_PROJECT_NAME = 'learn-jenkins-app'
//         SONAR_PROJECT_VERSION = '1.0'
//         DOCKER_IMAGE = 'brent/learn-jenkins-app:latest'
//     }

//     stages {
//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     // Use Node.js Docker container to install dependencies
//                     docker.image('node:16-alpine').inside {
//                         dir(REACT_APP_DIR) {
//                             sh 'npm install'
//                         }
//                     }
//                 }
//             }
//         }

//         stage('Run Tests') {
//             steps {
//                 script {
//                     // Run tests in Node.js container
//                     docker.image('node:16-alpine').inside {
//                         dir(REACT_APP_DIR) {
//                             sh 'npm test -- --watchAll=false'  // No interactive watch mode
//                         }
//                     }
//                 }
//             }
//         }

//         stage('SonarQube Scan') {
//             steps {
//                 script {
//                     // Use SonarQube container for the scan
//                     // withSonarQubeEnv(SONARQUBE_SERVER) {
//                     withSonarQubeEnv('jenkins-sonar') {
//                         docker.image('sonarsource/sonar-scanner-cli').inside {
//                             dir(REACT_APP_DIR) {
//                                 sh """
//                                 sonar-scanner -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
//                                     -Dsonar.projectName=${SONAR_PROJECT_NAME} \
//                                     -Dsonar.projectVersion=${SONAR_PROJECT_VERSION} \
//                                     -Dsonar.sources=./src \
//                                     -Dsonar.working.directory=.scannerwork

//                                 """
//                             }
//                         }
//                     }
//                 }
//             }
//         }

    //     stage('Build React App') {
    //         steps {
    //             script {
    //                 // Build the React app inside a Node.js Docker container
    //                 docker.image('node:16-alpine').inside {
    //                     dir(REACT_APP_DIR) {
    //                         sh 'npm run build'
    //                     }
    //                 }
    //             }
    //         }
    //     }

    //     stage('Dockerize React App') {
    //         steps {
    //             script {
    //                 // Use Docker to build the image and push it
    //                 docker.build("${DOCKER_IMAGE}", "${REACT_APP_DIR}").push()
    //             }
    //         }
    //     }
    // }

    // post {
    //     always {
    //         // Clean up workspace after the build
    //         cleanWs()
    //     }
//     }
// }














// pipeline {
//     agent any

//     environment {
//         // REACT_APP_DIR = 'your-react-app' // Your React app directory
//         // SONARQUBE_SERVER = 'SonarQubeServer' // Jenkins SonarQube server name
//         // SONAR_PROJECT_KEY = 'react-app'
//         // SONAR_PROJECT_NAME = 'React App'
//         // SONAR_PROJECT_VERSION = '1.0'
//         // DOCKER_IMAGE = 'your-dockerhub-username/react-app:latest'
//         NEXUS_URL = 'http://your-nexus-server.com'
//         NEXUS_REPO = 'sonarqube-reports'
//         NEXUS_CREDENTIALS_ID = 'nexus-credentials'


//         REACT_APP_DIR = 'src' // Your React app directory
//         SONARQUBE_SERVER = 'https://sonarqube.techworldplus.xyz/' // Jenkins SonarQube server name
//         SONAR_PROJECT_KEY = 'brentham_learn-jenkins-app_29b39040-c647-428e-bc72-16ef946b7c83'
//         SONAR_PROJECT_NAME = 'learn-jenkins-app'
//         SONAR_PROJECT_VERSION = '1.0'
//         DOCKER_IMAGE = 'brent/learn-jenkins-app:latest'
//     }

//     stages {
//         stage('Install Dependencies') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 dir(REACT_APP_DIR) {
//                     sh '''
//                         ls -la
//                         npm ci
//                         ls -la
//                     '''
//                 }
//             }
//         }

//         stage('Run Tests') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 dir(REACT_APP_DIR) {
//                     sh '''
//                         npm test -- --watchAll=false
//                     '''
//                 }
//             }
//         }

//         stage('SonarQube Scan') {
//             agent {
//                 docker {
//                     image 'sonarsource/sonar-scanner-cli'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 withSonarQubeEnv(SONARQUBE_SERVER) {
//                     dir(REACT_APP_DIR) {
//                         sh '''
//                             sonar-scanner \
//                                 -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
//                                 -Dsonar.projectName=${SONAR_PROJECT_NAME} \
//                                 -Dsonar.projectVersion=${SONAR_PROJECT_VERSION} \
//                                 -Dsonar.sources=. \
//                                 -Dsonar.working.directory=.scannerwork \
//                                 -Dsonar.sourceEncoding=UTF-8
//                         '''
//                     }
//                 }
//             }
//         }

//         stage('Build React App') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 dir(REACT_APP_DIR) {
//                     sh '''
//                         npm run build
//                     '''
//                 }
//             }
//         }

//         stage('Dockerize React App') {
//             steps {
//                 script {
//                     docker.build("${DOCKER_IMAGE}", "${REACT_APP_DIR}").push()
//                 }
//             }
//         }

//         stage('Publish SonarQube Artifacts to Nexus') {
//             steps {
//                 script {
//                     // Archive the SonarQube scan artifacts
//                     archiveArtifacts artifacts: '**/.scannerwork/**', allowEmptyArchive: true

//                     // Publish the scan reports to Nexus
//                     nexusArtifactUploader(
//                         nexusVersion: 'nexus3',
//                         protocol: 'http',
//                         nexusUrl: "${NEXUS_URL}",
//                         groupId: 'com.yourcompany.reactapp',
//                         version: "${SONAR_PROJECT_VERSION}",
//                         repository: "${NEXUS_REPO}",
//                         credentialsId: "${NEXUS_CREDENTIALS_ID}",
//                         artifacts: [
//                             [
//                                 artifactId: 'sonarqube-report',
//                                 classifier: '',
//                                 file: "${REACT_APP_DIR}/.scannerwork/report-task.txt",
//                                 type: 'txt'
//                             ],
//                             [
//                                 artifactId: 'sonarqube-metrics',
//                                 classifier: '',
//                                 file: "${REACT_APP_DIR}/.scannerwork/sonar-report.json",
//                                 type: 'json'
//                             ]
//                         ]
//                     )
//                 }
//             }
//         }
//     }

//     post {
//         always {
//             cleanWs() // Clean workspace after the build
//         }
//     }
// }







pipeline {
    agent any

    environment {
        // REACT_APP_DIR = 'your-react-app' // Your React app directory
        // SONARQUBE_SERVER = 'SonarQubeServer' // Jenkins SonarQube server name
        // SONAR_PROJECT_KEY = 'react-app'
        // SONAR_PROJECT_NAME = 'React App'
        // SONAR_PROJECT_VERSION = '1.0'
        // DOCKER_IMAGE = 'your-dockerhub-username/react-app:latest'
        NEXUS_URL = 'http://your-nexus-server.com'
        NEXUS_REPO = 'sonarqube-reports'
        NEXUS_CREDENTIALS_ID = 'nexus-credentials'


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
            steps {
                sh '''
                    ls -la
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Run Tests') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                // dir(REACT_APP_DIR) {
                    sh '''
                        npm test -- --watchAll=false
                        ls -la
                    '''
                // }
            }
        }


        stage('SonarQube Scan') {
            agent {
                docker {
                    image 'sonarsource/sonar-scanner-cli'
                    reuseNode true
                }
            }
            steps {
                withSonarQubeEnv(SONARQUBE_SERVER) {
                    // dir(REACT_APP_DIR) {
                        sh '''
                            sonar-scanner -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                                -Dsonar.projectName=${SONAR_PROJECT_NAME} \
                                -Dsonar.projectVersion=${SONAR_PROJECT_VERSION} \
                                -Dsonar.sources=./src \
                                -Dsonar.working.directory=.scannerwork
                            ls -la
                        '''
                    // }
                }
            }
        }

        stage('Build React App') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                // dir(REACT_APP_DIR) {
                    sh '''
                        npm run build
                    '''
                // }
            }
        }

    //     stage('Dockerize React App') {
    //         steps {
    //             script {
    //                 docker.build("${DOCKER_IMAGE}", "${REACT_APP_DIR}").push()
    //             }
    //         }
    //     }

    //     stage('Publish SonarQube Artifacts to Nexus') {
    //         steps {
    //             script {
    //                 // Archive the SonarQube scan artifacts
    //                 archiveArtifacts artifacts: '**/.scannerwork/**', allowEmptyArchive: true

    //                 // Publish the scan reports to Nexus
    //                 nexusArtifactUploader(
    //                     nexusVersion: 'nexus3',
    //                     protocol: 'http',
    //                     nexusUrl: "${NEXUS_URL}",
    //                     groupId: 'com.yourcompany.reactapp',
    //                     version: "${SONAR_PROJECT_VERSION}",
    //                     repository: "${NEXUS_REPO}",
    //                     credentialsId: "${NEXUS_CREDENTIALS_ID}",
    //                     artifacts: [
    //                         [
    //                             artifactId: 'sonarqube-report',
    //                             classifier: '',
    //                             file: "${REACT_APP_DIR}/.scannerwork/report-task.txt",
    //                             type: 'txt'
    //                         ],
    //                         [
    //                             artifactId: 'sonarqube-metrics',
    //                             classifier: '',
    //                             file: "${REACT_APP_DIR}/.scannerwork/sonar-report.json",
    //                             type: 'json'
    //                         ]
    //                     ]
    //                 )
    //             }
    //         }
    //     }
    }

    post {
        always {
            cleanWs() // Clean workspace after the build
        }
    }
}