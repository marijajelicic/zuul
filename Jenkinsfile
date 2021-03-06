pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "zuul:latest"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/marijajelicic/zuul'
            }
        }
        stage ('Docker') {
            when {
                branch 'master'
            }
            steps{
                script{
                    sh '''
                            docker image build -t zuul:latest .
                        '''
                }
            }
            post {
                failure {
                    emailext (
                        subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER} ",
                        body: """CI/CD pipeline greska u "Docker" fazi. Log fajl se moze videti na: href=${env.BUILD_URL} """,
                        to: "marija.jelicic@netcast.rs",
                        from: "jenkins@jenkins.netcast.rs"
                    )
                }
            }
        }

        stage ('StopPrevious') {
            when {
                branch 'master'
            }
            steps{
                script{
                    sh '''
                            docker container stop zuul
                            docker container rm zuul
                        '''
                }
            }
            post {
                failure {
                    emailext (
                        subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER} ",
                        body: """CI/CD pipeline greska u "Build" fazi. Log fajl se moze videti na: href=${env.BUILD_URL} """,
                        to: "marija.jelicic@netcast.rs",
                        from: "jenkins@jenkins.netcast.rs"
                    )
                }
            }
        }

        stage ('Deploy') {
            when {
                branch 'master'
            }
            steps{
                script{
                    sh '''
                            docker run -d --name zuul -p 8080:8080 zuul:latest
                        '''
                }
            }
            post {
                failure {
                    emailext (
                        subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER} ",
                        body: """CI/CD pipeline greska u "Build" fazi. Log fajl se moze videti na: href=${env.BUILD_URL} """,
                        to: "marija.jelicic@netcast.rs",
                        from: "jenkins@jenkins.netcast.rs"
                    )
                }
            }
        }
    }
}

