import groovy.transform.Field

podTemplate(label: 'bc16-gc', containers: [
	containerTemplate(name: 'bc16-helm', image: 'alpine/helm', command: 'cat', ttyEnabled: true)],
	volumes: [hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')]
) {

  node('bc16-gc'){
//   	environment {
// 		docker_image=""
// 		// MY_KUBECONFIG = credentials('config-file')
// 		MY_KUBECONFIG = credentials('master2-rishmita')
// 	}
	
properties([
            parameters([
                string(
                    defaultValue: 'latest',
                    description: '', 
                    name: 'fe_tag',
                    trim: true),
                string(
                    defaultValue: 'latest',
                    description: '', 
                    name: 'job_tag',
                    trim: true),
		string(
                    defaultValue: 'latest',
                    description: '', 
                    name: 'org_tag',
                    trim: true),
            ])
        ])
    
                stage("Helm install") {
                        git 'https://github.com/VenkataRishmithaAita/jenkins-dashboard-bc16'
                           container('bc16-helm'){
                               withCredentials([file(credentialsId: 'master2-rishmita', variable: 'config')]) {


                               sh """
                                  export KUBECONFIG=\${config}
                                  helm upgrade --install  bc16 . -n bc16  --set fetag=${fe_tag} --set jobtag=${job_tag} --set orgtag=${org_tag}                         
                                  """
                        }    
                    }
                    }
		

		
		
		}
	
// 	post{
// 	    always{
// 	        container('bc15-docker'){
// 	         sh 'docker logout'
// 	    }
// 	    }
// 	}
    

 

}




// pipeline{
// 		agent{
			
// 			kubernetes {
			    
// 			    yaml '''
//         apiVersion: v1
//         kind: Pod
//         spec:
//           containers:
//           - name: bc15-helm
//             image: alpine/helm
//             command:
//             - cat
//             tty: true
//         '''
    
//     }
// 		}
//     environment {
//         MY_KUBECONFIG = credentials('config-file')
//     }

// 		stages{
			

				
//                 stage('Checkout Source') {
// 		      steps {
// 			git 'https://github.com/PDhanrajnath/gc'
// 		      }   
//                         }
                   
                    
//                 stage("Build") {
//                         steps {
//                             container('bc15-helm'){
//                                sh """
//                                   export KUBECONFIG=\${MY_KUBECONFIG}
                                  
//                                   helm upgrade --install bc15 . -n bc15                              
//                                   """
//                             //     sh "export KUBECONFIG=\${config} helm repo update --kubeconfig=$MY_KUBECONFIG"
//                             //   sh "export KUBECONFIG=\${config} helm install voting myvoteapp --kubeconfig=$MY_KUBECONFIG"
//                             }
                            
//                         }
//                     }
 
                    
				
                
//             }
//         }
