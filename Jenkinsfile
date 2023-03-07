pipeline{
	agent{
		label{
			label "built-in"
			customWorkspace "/mnt/project"
			}
		}
	environment{
				url = "https://github.com/KetanSP25/game-of-life.git"
				qaip = "172.31.38.122"
				}
	stages{
		stage("copy project"){
			steps{
				sh "rm -rf *"
				sh "git clone ${url}"
			}
		}
		stage("Build-project"){
			steps{
				sh "rm -rf /home/ketan/.m2"
				sh "cd game-of-life && mvn clean install"
			}
		}
		stage("copy wars"){
			steps{
				sh "cp game-of-life/gameoflife-web/target/gameoflife.war /mnt/wars"
			}
		}
		stage("deploy on slave"){
			steps{
				sh "scp -r /mnt/wars/gameoflife.war ketan@${qaip}:/mnt/wars"
			}
		}
	}
	

}
