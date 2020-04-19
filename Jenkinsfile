node {

    checkout changelog: false, poll: false, scm: [
        $class: 'GitSCM',
        branches: [
            [name: '*/master']
        ], doGenerateSubmoduleConfigurations: false, extensions: [
            [$class: 'WipeWorkspace']
        ], submoduleCfg: [], userRemoteConfigs: [
            [credentialsId: 'jenkins-github-ssh',
            url: 'git@github.com:figaw/configuration-as-code-jenkins-k8s-pipeline.git']
        ]
    ]

    try {
        stage('Sanity') {
            sh 'echo Hello, World!'
        }
        stage('Setup') {
            configFileProvider([configFile(fileId: 'auth-json', targetLocation: 'auth.json')]) {

                echo "this is where I would authenticate my session using my file"
                sh "cat ${WORKSPACE}/auth.json"

            }

            sh 'gcloud --version'
        }
        stage('Create instance') {
            echo "Do something on gcloud, create machines etc."
        }
        stage('Build my project') {
            sh './build.sh'
        }
    } catch (err) {
        echo "Failed: ${err}"
        throw err
    } finally {
        echo "Clean up VMs that I've used for building."
    }
}
