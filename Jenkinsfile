	pipeline
	{
		agent { label 'MAVEN_JDK8'}
        triggers { cron ('H/15 * * * *') }
        parameters 
        {
            string(name: 'MAVEN_GOAL',defaultValue: 'package')
        }
		stages
		{
			stage('vcs')
			{
				steps
				{
					git url: 'https://github.com/Sujata-Joshi/game-of-life.git',
					branch: 'declarative'
				}
			}
			stage('package')
			{
                tools { jdk 'JDK_8' }
				steps
				{
					sh "mvn ${params.MAVEN_GOAL}"
				}
			}
			stage('post build')
			{
				steps
				{
					archiveArtifacts artifacts: '**/target/gameoflife.war',
									 onlyIfSuccessful: true
					junit testResults: '**/surefire-reports/TEST-*.xml'                 
				}
			}
		}
	}