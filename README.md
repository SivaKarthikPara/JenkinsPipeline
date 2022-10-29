### Adding connector and sending build notifications to MS Teams or Slack

#### Setup directly using job config or can setup in global config
![image](https://user-images.githubusercontent.com/56120741/198828711-3c06391f-b90e-4b28-a3e9-a3d567652c7f.png)

#### or through pipeline jenkins DSL

![image](https://user-images.githubusercontent.com/56120741/198829158-eeb04239-27bd-4879-bfe3-1808e1f4bd0c.png)

```
pipeline {
    agent any

	options {
		office365ConnectorWebhooks([[
			name: 'Teams webhook',
			startNotification: true,
			notifySuccess: true,
            notifyAborted: false,
            notifyNotBuilt: false,
            notifyUnstable: true,
            notifyFailure: true,
            notifyBackToNormal: true,
            notifyRepeatedFailure: false,
            url: 'https://outlook.office.com/webhookb2/8ff57ab6-2eec-4907-b356-5813fa0db0ba@76a2ae5a-9f00-4f6b-95ed-5d33d77c4d61/JenkinsCI/1d8243cb319540a3b3e170a3c210ce9b/7d63f7cd-7240-4234-988d-9b535cc6451d'
		]])
	}

    stages {
		stage('Build') {
            steps {
                    echo 'A pipeline is a group of events or jobs which are interlinked with one another in a sequence. In this scenario the code is compiled, tested and test-results are published in a sequence.'
                	echo 'Starting to build pipeline to display vowels of a sentence in upper case'
				// 	sh 'mvn clean compile'

			}
		}
		stage('Test') {
            steps {
            	
                	echo 'Compiled the code and no errors were encountered and moved to Testing stage....'
				// 	sh 'mvn test'

			}
		}
	}
    post {
        always {
            echo 'Post-Build Publishing test results and your test Results can be tracked'
			// junit 'target/surefire-reports/*.xml'
		}
	}
}
```


![image](https://user-images.githubusercontent.com/56120741/198828636-8bc09da2-9b98-42c1-847b-1ce3f8a4d03b.png)

![image](https://user-images.githubusercontent.com/56120741/198828723-94afab00-06fe-4d8e-81dc-93dd1fc5b8c7.png)
