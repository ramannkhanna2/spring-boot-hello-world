pipeline {
    environment {
        namespace = 'raman' // OpenShift namespace
    }

    agent any

    stages {
        stage('Install OpenShift CLI') {
            steps {
                script {
                    // Download and install the OpenShift CLI
                    sh '''
                    apt-get update && apt-get install -y wget
                    wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-linux.tar.gz
                    tar -xvf openshift-client-linux.tar.gz
                    mv oc /usr/local/bin/
                    chmod +x /usr/local/bin/oc
                    oc version  # Verify installation
                    '''
                }
            }
        }

        
        
        stage('Deploy to OpenShift') {
            steps {
                script {
                    sh '''
                    oc login --token=sha256~pyXV_CWSm8k1mRMVqwr5VINx8TBDdxZmyzZPO0pLvH4 --server=https://api.natwest.priartw.com:6443 --insecure-skip-tls-verify
                    oc project ${namespace}
                    oc start-build hello2
                    '''
                }
            }
        }
    }
}
