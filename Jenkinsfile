pipeline {
    agent {
        node {
            label "MyNode"
        }
    }
    stages {
        stage('Take User Input') {
            steps {
                script {
                    properties([
                        parameters([
                            choice(
                                choices: ['Dev', 'Stage', 'Prod'], 
                                name: 'DeployEnv',
                                description: "Select the environment"
                            ),
                            choice(
                                choices: ['ws-1', 'ws-1', 'worker-1'], 
                                name: 'ArtifactId', 
                                description: "Which artifact",
                            ),
                            string(
                                defaultValue: 'version of build', 
                                name: 'Version', 
                                description: "Write the version of build",
                                trim: true
                            )
                        ])
                    ])
                }
            }
        }
        stage('Run deployer') {
            steps {
                echo 'Deploying Artifacts to Kubernetes Env...'

                withCredentials([
                    [$class: 'UsernamePasswordMultiBinding', 
                    credentialsId:"MY_CRED_ID",
                        usernameVariable: 'AZURE_SERVICE_USERNAME', 
                        passwordVariable: 'AZURE_SERVICE_SECRET'],
                    [$class: 'UsernamePasswordMultiBinding', credentialsId:"MY_API_KEY",
                        usernameVariable: 'ARTIFACTORY_USERNAME', 
                        passwordVariable: 'ARTIFACTORY_PASSWORD']
                ]) {
                    sh """
                        # installing kubectl
                        sudo curl -LO "https://dl.k8s.io/release/v1.25.2/bin/linux/amd64/kubectl"
                        sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
                        kubectl version --client

                        echo "deploy to env=${params.DeployEnv}, artifact=${params.ArtifactId}, version=${params.Version}"
                        
                        echo "Preparing runtime env..."
                        python3.8 -m pip install virtualenv
                        python3.8 -m venv python_env
                        source python_env/bin/activate
                        python3.8 -m pip install --upgrade pip
                        python3.8 -m pip install -r requirements.txt -i https://${ARTIFACTORY_USERNAME}:${ARTIFACTORY_PASSWORD}@artifactory.myorg.com/artifactory/api/pypi/pypi-myorg-release/simple

                        echo "Ready to run deployment..."
                        python3.8 deploy.py "${params.DeployEnv}" "${params.ArtifactId}" "${params.Version}"

                        deactivate
                    """
                }
            }
        }
    }
}
