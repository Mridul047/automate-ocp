pipeline {
    agent any

    environment {
        // Define OpenShift server URL
        OPENSHIFT_SERVER = 'https://api.sandbox-m2.ll9k.p1.openshiftapps.com:6443'
        // Use Jenkins credentials to store OpenShift token
        // Replace 'openshift-token' with the actual ID of your stored credentials
        OPENSHIFT_CREDENTIALS_ID = credentials('openshift-token')
    }

    stages {
        stage('Login to OpenShift') {
            steps {
                script {
                    // Log into OpenShift using the OpenShift Client Plugin
                    withCredentials([string(credentialsId: "${env.OPENSHIFT_CREDENTIALS_ID}", variable: 'OPENSHIFT_TOKEN')]) {
                        // Using the OpenShift Client Plugin to log in
                        openshift.withCluster("${env.OPENSHIFT_SERVER}") {
                            openshift.withCredentials("${env.OPENSHIFT_TOKEN}") {
                                echo 'Logged into OpenShift successfully!'
                            }
                        }
                    }
                }
            }
        }
        
        // Add more stages here for your deployment or other tasks
        stage('Sample Stage') {
            steps {
                echo 'Performing operations in OpenShift...'
                // Example: List all projects
                script {
                    openshift.withCluster("${env.OPENSHIFT_SERVER}") {
                        openshift.withCredentials("${env.OPENSHIFT_TOKEN}") {
                            def projects = openshift.raw('oc', 'get', 'projects')
                            echo "Projects: ${projects}"
                        }
                    }
                }
            }
        }
    }
}
