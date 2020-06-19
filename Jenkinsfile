pipeline {
    agent none
    options {
        // ansiColor('xterm')
        timeout (time: 1, unit: 'HOURS')
    }
    tools {
        maven 'maven-latest'
        nodejs 'nodejs'
        }
    stages {
        stage('build') {
                stage('java'){
                    agent {
                        label 'master'
                    }
                steps {
                    checkout scm: [$class: 'GitSCM', branches: [[name: 'master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: "maven-samples"]], userRemoteConfigs: [[url: "https://github.com/gabrielf/maven-samples.git"]]]
                    dir('maven-samples') {
                         sh """ls
                        mvn clean install
                        """
                        }
            }
            post {
                success {
                    echo "\033[1m\033[32mBuild is success! \033[0m"
                    cleanWs()
                }
                unsuccessful {
                    echo "\033[1m\033[34mBuild Failed! \033[0m"
                    cleanWs()
                }
            }
        }

            stage('node'){
                    agent {
                        label 'master'
                    }
                steps {
                    checkout scm: [$class: 'GitSCM', branches: [[name: 'master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: "the-example-app.nodejs"]], userRemoteConfigs: [[url: "https://github.com/contentful/the-example-app.nodejs"]]]
                    dir('the-example-app.nodejs') {
                         sh """ls
                            npm install
                            """
                        }
            }
            post {
                success {
                    echo "\033[1m\033[32mBuild is success! \033[0m"
                    cleanWs()
                }
                unsuccessful {
                    echo "\033[1m\033[34mBuild Failed! \033[0m"
                    cleanWs()
                }
            }

        }
}

}

}




//sequential
// stages {
//   stage('java') {
//     stages {
//       // One or more stages need to be included within the stages block.
//     }
//   }

//   stage('node') {
//     stages {
//       // One or more stages need to be included within the stages block.
//     }
//   }

// }


// Parellel

// stages {
//   stage('java') {
//     parallel {
//       // One or more stages need to be included within the parallel block.
//     }
//   }

//   stage('node') {
//     parallel {
//       // One or more stages need to be included within the parallel block.
//     }
//   }

// }
