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
            https://github.com/sravan-github/ansible-role.git
            ls -l
            pwd
            ansible-playbook -i inventory/mariadb.hosts --private-key=$ANSIBLE_PRIVATE_KEY install-book.yml
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
