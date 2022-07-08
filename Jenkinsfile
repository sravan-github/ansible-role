pipeline {
  //agent any
  agent {
  docker { 
            image 'sravangcpdocker/terraform:7'
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
            git clone https://github.com/sravan-github/ansible-role.git
            ls -l
            pwd
            #ansible-playbook -i inventory/mariadb.hosts --private-key=$ANSIBLE_PRIVATE_KEY install-book.yml
            '''
         ansiblePlaybook credentialsId: 'ansible-key1', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory/mariadb.hosts', playbook: 'install-book.yml'
      }
    }
  }
  post {
        always {
        	cleanWs deleteDirs: true
        }
    }
}
