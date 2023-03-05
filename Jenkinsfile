pipeline{
		agent{
			label{
					label 'built-in'
					customWorkspace '/mnt/project'
			}
			enviornment{
						qaip= "172.31.38.122"
			}
		}
		stages{
			stage('clone GOL on master'){
					steps{
							sh "rm -rf *"
							sh "git clone https://github.com/KetanSP25/game-of-life.git"
					}
			}
			stage('Build on master'){
					steps{
							sh "cd /mnt/project/game-of-life && mvn clean install"
					}
			}
			stage('deploy GOL on master'){
					steps{
							sh "cp /mnt/project/game-of-life/gameoflife-web/target/gameoflife.war /mnt/server/apache-tomcat-9.0.71/webapps"
					}
			}
			stage('copy on slave'){
					steps{
							sh "scp -r /mnt/project/game-of-life/gameoflife-web/target/gameoflife.war ketan@${qaip}:/mnt/wars/"
					}
			}
			stage('deploy on slave'){
					agent{
						label{
								label 'qa'
						}
					}
					steps{
							sh "cp /mnt/wars/gameoflife.war /mnt/server/apache-tomcat-9.0.71/webapps"
					}
			}
		}
}
