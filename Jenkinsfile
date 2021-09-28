pipeline{
		agent{
			
			kubernetes {
    
    yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: bc16-helm
            image: alpine/helm
            command:
            - cat
            tty: true
        '''
    
    }
		}
    environment {
        MY_KUBECONFIG = credentials('config-file')
    }
		stages{
				
                stage("add Repo") {
                        steps {
                            container('bc16-helm'){
                               sh "helm repo add  bc16 https://venkatarishmithaaita.github.io/jenkins-dashboard-bc16/ "
                            }
                            
                        }
                    }
                    
                stage("Build") {
                        steps {
                            container('bc15-helm'){
                               sh """
                                  export KUBECONFIG=\${MY_KUBECONFIG}
                                  helm repo update 
                                  helm install bc16 bc16/bc16-gc -n bc16                              
                                  """
                            //     sh "export KUBECONFIG=\${config} helm repo update --kubeconfig=$MY_KUBECONFIG"
                            //   sh "export KUBECONFIG=\${config} helm install voting myvoteapp --kubeconfig=$MY_KUBECONFIG"
                            }
                            
                        }
                    }
                    
                    
				
                
            }
        }
