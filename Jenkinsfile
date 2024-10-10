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
        REACT_APP_DIR = 'src' // Your React app directory
        SONARQUBE_SERVER = 'https://sonarqube.techworldplus.xyz/' // Jenkins SonarQube server name
        SONAR_PROJECT_KEY = 'brentham_learn-jenkins-app_29b39040-c647-428e-bc72-16ef946b7c83'
        SONAR_PROJECT_NAME = 'learn-jenkins-app'
        SONAR_PROJECT_VERSION = '1.0'
        DOCKER_IMAGE = 'brent/learn-jenkins-app:latest'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Use Node.js Docker container to install dependencies
                    docker.image('node:16-alpine').inside {
                        dir(REACT_APP_DIR) {
                              sh """
                                ls -la

                                """
                        }
                    }
                }
            }
        }

        // stage('Run Tests') {
        //     steps {
        //         script {
        //             // Run tests in Node.js container
        //             docker.image('node:16-alpine').inside {
        //                 dir(REACT_APP_DIR) {
        //                     sh 'npm test -- --watchAll=false'  // No interactive watch mode
        //                 }
        //             }
        //         }
        //     }
        // }

        // stage('SonarQube Scan') {
        //     steps {
        //         script {
        //             // Use SonarQube container for the scan
        //             // withSonarQubeEnv(SONARQUBE_SERVER) {
        //             withSonarQubeEnv('jenkins-sonar') {
        //                 docker.image('sonarsource/sonar-scanner-cli').inside {
        //                     dir(REACT_APP_DIR) {
        //                         sh """
        //                         ls -la

        //                         """
        //                     }
        //                 }
        //             }
        //         }
        //     }
        // }

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
    }
}
