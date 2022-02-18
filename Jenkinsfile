pipeline {
  //agent any
  agent {
  docker { 
            image 'sravangcpdocker/toolkit:3'
            args '-u root:root'
        }
        }
  environment {
   ANSIBLE_PRIVATE_KEY=credentials('ansible-key') 
  }
  stages {
    stage('Hello') {
      steps {
        sh '''
            git clone https://github.com/sravan-github/jenkins-example-ansible.git
            ls -l
            pwd
            ansible-playbook -i inventory/mariadb.hosts --private-key=$ANSIBLE_PRIVATE_KEY play.yml
            '''
      }
    }
  }
  post {
        always {
        	cleanWs deleteDirs: true
        }
    }
}
