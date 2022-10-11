pipeline {
    agent {
        label 'hadolint'
    }
    stages {
        stage('Checkout') {
            steps {
                echo '-----------------------------CHECKOUT------------------------------'
                dir('pet') {
                    //git branch: '${BRANCH_NAME}', url: 'git@git.epam.com:mykola_serdiuk/spring-petclinic.git', credentialsId: 'git_epam'
                    echo 'Checkout'
                    ls -la
                }
            }
        }
        stage('Dockerlint') {
            steps {
                echo '-----------------------------Hadolint------------------------------'
                sh 'hadolint Dockerfile | tee -a hadolint_lint.txt'
                
            }
        }
    }
}
