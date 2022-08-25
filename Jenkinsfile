node {
    def WORKSPACE = "/home/ubuntu/download/jenkins_workspace/workspace/springboot-deploy"
    def dockerImageTag = "springboot-deploy${env.BUILD_NUMBER}"
    def buildNumber = "${env.BUILD_NUMBER}"

    try {
        stage('Clone Repo') {
            //for display purposes
            //Get some code from a GitHub repository
            git url: 'https://github.com/kwantke/Test4.git',
                branch: 'master'
        }
        stage('Build docker') {
            //build npm
            //sh "sudo npm install"
            //sh "sudo npm run build"
            dockerImage = docker.build("springboot-deploy:${env.BUILD_NUMBER}")
            //sh 'docker build -t springboot-deploy:${buildNumber} .'
        }
        stage('Deploy docker') {
            echo "Docker Image Tag Name: ${dockerImageTag}"
            sh "docker stop springboot-deploy || true && docker rm springboot-deploy || true"
            sh "docker run --name springboot-deploy -d -p 9040:8080 springboot-deploy:${env.BUILD_NUMBER}"
        }
    } catch(e){
        throw e
    }
}