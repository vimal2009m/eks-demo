
pipeline{

	agent any

	
	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t vimal2019/tomimag:4.0 .'
               
			}
		}
        
        stage('login') {

            steps {
        
		        withCredentials([string(credentialsId: 'vimal2019', variable: 'PASSWORD')]) {
                    sh 'sudo docker login -u vimal2019 -p $PASSWORD'
                }
            }
        }
		stage('Push') {

			steps {
				sh 'sudo docker push vimal2019/tomimag:4.0'
			}
		}

        stage('eks deploy') {

			steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f ingress.yaml'
			}
		}
	}

	post {
		always {

            		cleanWs()
			
            		echo "done"
		}
	}

}

