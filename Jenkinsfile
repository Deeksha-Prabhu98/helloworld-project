pipeline {
    agent { label "Agent_1" }
    
    triggers {
        pollSCM('* * * * *')
    }    

    stages {
        stage('clone_project_A') {
            steps {
                echo 'clone project A'
                git 'https://github.com/Yogish1235/Helloworld-latest.git'
            }
        }
        stage('build_project_A') {
            steps {
                echo 'build_projectA'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        } 
        stage('Docker_build') {
            steps {
                echo 'Docker build_projecta'
                sh 'docker build -t projecta .' 
            }
        }
        stage('login to dockerhub') {
            steps {
                echo 'login to dockerhub'
                sh 'docker login -u yogish1235 -p Yogi@docker1998'
            }
        } 
        stage('Tag the Image') {
            steps {
                echo 'Tag the Image'
                sh 'docker tag  projecta yogish1235/projecta'
            }
        } 
        stage('Deploy to dockerhub') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker push yogish1235/projecta'
            }
        }
        stage('Remove Docker container') {
            steps {
                echo 'Remove Docker container'
                sh 'docker stop projectA_container || true'
                sh 'docker rm projectA_container || true'
            }
        }
              
        stage('Run docker image') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker run --name projectA_container -d -p 8181:8080 yogish1235/projecta'
            }
        }        
    }
}
