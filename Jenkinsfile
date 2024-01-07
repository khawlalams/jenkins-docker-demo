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
                echo 'Deploying Artifacts Env...'
               
            }
        }
    }
}
