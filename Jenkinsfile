// pipeline{
// 		agent{
			
// 			kubernetes {
    
//     yaml '''
//         apiVersion: v1
//         kind: Pod
//         spec:
//           containers:
//           - name: bc16-helm
//             image: alpine/helm
//             command:
//             - cat
//             tty: true
//         '''
    
//     }
// 		}
//     environment {
//         MY_KUBECONFIG = credentials('my-config')
//     }
// 		stages{
				
//                 stage("add Repo") {
//                         steps {
//                             container('bc16-helm'){
//                                sh "helm repo add  bc16 https://venkatarishmithaaita.github.io/jenkins-dashboard-bc16/ "
//                             }
                            
//                         }
//                     }
                    
//                 stage("Build") {
//                         steps {
//                             container('bc16-helm'){
//                                sh """
//                                   export KUBECONFIG=\${MY_KUBECONFIG}
//                                   helm repo update 
//                                   helm install bc16 bc16/helm1 -n bc16                              
//                                   """
                            
//                             //   sh "export KUBECONFIG=\${config} helm install voting myvoteapp --kubeconfig=$MY_KUBECONFIG"
//                             }
                            
//                         }
//                     }
                    
                    
				
                
//             }
//         }
import groovy.transform.Field

podTemplate(label: 'bc16', containers: [
	containerTemplate(name: 'helm', image: 'alpine/helm', command: 'cat', ttyEnabled: true)],
	volumes: [hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')]
) {

  node('bc16'){

    	stage('Checkout Source') {
      
        git 'https://github.com/VenkataRishmithaAita/jenkins-dashboard-bc16.git'
      
    }
                stage("Build") {
                        
                    container('helm'){
                        withCredentials([file(credentialsId: 'my-config', variable: 'config')]) {


                               sh """
                                  export KUBECONFIG=\${config}
                                  helm upgrade --install  bc16 . -n bc16                              
                                  """
                        }    
                    }       
                }	
		}
	
}
