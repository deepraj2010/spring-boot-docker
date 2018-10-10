node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        echo 'kalpesh'
        checkout scm
    }
    stage('Test Image'){
        sh 'mvn test'
    }
    stage('Building Jarfile'){
        sh 'mvn package'
    }
    stage('Create docker image'){
        sh 'docker build -t spring-boot-docker .'
    }
    stage('Pushing docker image'){
        sh "docker login --username=${env.dockerHub_user_name} --password=${env.dockerHub_password}"
        echo 'login successfully'
        sh 'docker tag spring-boot-docker ksaubhri/spring-boot-docker'
        sh 'docker push ksaubhri/spring-boot-docker'
        echo 'push successfull'
    }
    stage('Deploy docker image'){
        sh 'chmod 400 /home/deep/Practice/aws/aws_ec2.pem'
        sh "ssh -o StrictHostKeyChecking=no  -i /home/deep/Practice/aws/aws_ec2.pem ubuntu@ec2-54-235-32-169.compute-1.amazonaws.com 'bash -s' < docker_run_aws_script.sh"
    }

}
