pipeline {
	agent any
	tools {
		maven 'maven 3.9.9'
	}

	parameters {
		choice(name: 'DEPLOY_ENVIRONMENT', choices: ['tomcat1', 'tomcat2'], description: 'Ambiente de despliegue')
	}

	stages {
		stage('PackageDocker') {
			steps {
				bat 'mvn -B -q -P docker-build clean package'
			}
		}
		/*stage('Deploy') {
			steps {
				sh 'docker build -t ' + params.DEPLOY_ENVIRONMENT + ' .'
				sh 'cd ' + env.ENVS_DIR + ' && docker compose down ' + params.DEPLOY_ENVIRONMENT + ' && docker compose up -d ' + params.DEPLOY_ENVIRONMENT
			}
		}*/

		stage('Deploy') {
            		when {
               		 not {
                    		equals expected: 'ninguno', actual: params.DEPLOY_ENVIRONMENT
               		 }
            		}
            		steps {
                		//bat 'D:\\devenv\\JENKINS_CURSO\\AMBIENTES\\tomcat1\\bin\\shutdown.bat'
               			 bat 'copy target\\ROOT.war D:\\devenv\\ambientes\\' + params.DEPLOY_ENVIRONMENT + '\\apache-tomcat-9.0.96\\webapps'
                		//bat 'D:\\devenv\\JENKINS_CURSO\\AMBIENTES\\tomcat1\\bin\\startup.bat'
            		}
        	}		
	}
}
