pipeline {
    agent any
    stages {
        //Continuous Integration
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        //Continuous Delivery
        stage('Docker Build&Push') {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: "") {
                    sh 'docker build -t basmaoueslati/compare-appf25 .'
                    sh 'docker push basmaoueslati/compare-appf25'
                }
            }
        }
        //Continuous Deployment
       stage('Run Ansible Playbook') {
            steps {            
                sh 'ansible-playbook -i inventory.ini playbook.yml -e ansible_python_interpreter=/usr/bin/python3'
            
        }
    }

    }
}

