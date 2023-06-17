pipeline{
    agent { label 'Ansible-node' } 
    triggers {
       pollSCM('*/30 * * * *')
    }
    stages{
        stage('VCS'){
            steps{
                sh '''
                if [ -d "game-of-life" ] 
                then
                    cd game-of-life
                    git pull   
                else
                    git clone https://github.com/March2023Sujata/game-of-life.git
                    cd game-of-life
                fi
                '''
            }
        } 
        stage('Build package'){
            tools { jdk 'Java_8' }
            steps{
                sh 'mvn package'
            }
        }   
        stage('Ansible-Playbook-Role'){
            steps{
                sh '''
                if [-d "Jenkins-Ansible-Gol"]
                then
                    cd Jenkins-Ansible-Gol
                    git pull
                else
                    git clone https://github.com/March2023Sujata/Jenkins-Ansible-Gol.git
                    cd Jenkins-Ansible-Gol/GOL_ROLE
                fi
                '''
            }
        }
        stage('Run-Role-Playbook'){
            steps{
                sh 'ansible-playbook -i hosts gol.yml'
            }
        }    
    }
}