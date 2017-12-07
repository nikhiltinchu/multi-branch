properties([[$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/nikhiltinchu/multi-branch.git/'], pipelineTriggers([githubPush()])])
node {
 	// Clean workspace before doing anything
    deleteDir()
 parameters {
                            string(defaultValue: "default", description: 'Select Branch here ', name: 'Branch')
                           // choices are newline separated
                            choice(choices: 'Integration\nUnit', description: 'Used for posgress sh and codedeploy deployment group', name: 'Environment')
                            booleanParam(name: 'REBUILD DATABASE', defaultValue: true, description: 'Should we rebuild the database')
                            booleanParam(name: 'DEPLOY', defaultValue: true, description: 'should we deploy the application')
             }
    try {
        stage ('clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project nnn.....'"
		
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
