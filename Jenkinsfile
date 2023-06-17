pipeline{
    agent label { 'Ansible-node' } 
    stages{
        stage('VCS'){
            steps{
                sh '''
                if [ -d "game-of-life" ] 
                then
                    cd game-of-life
                    git pull
                    mvn package
                else
                    git clone https://github.com/March2023Sujata/game-of-life.git
                    cd game-of-life
                    mvn package
                    cd ..
                fi
                '''         
            }
        }          
    }
}