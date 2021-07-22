pipeline {
  agent any
    stages {
        stage('Build Parameters') {
            steps {
                script {
                    properties([
                        parameters([
                            string(
                                defaultValue: '',
                                name: 'ansibleuser',
                                trim: true
                            ),
                            string(
                                defaultValue: '',
                                name: 'password',
                                trim: true
                            ),
                            string(
                                defaultValue: '',
                                name: 'windowshost',
                                trim: true
                            )
                        ])
                    ])
                }
            }
        }
        stage ('Windows VM Update') {
            steps {
                  sh '''
                  ansible-playbook -i ${windowshost}, playbook.yaml --extra-vars "ansible_user=${ansibleuser} ansible_password=\"${password}\" ansible_port=5986 ansible_connection=winrm ansible_winrm_server_cert_validation=ignore"
                  '''
            }
        }

    }
 }
