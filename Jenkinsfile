pipeline {
	agent any
	stages{
		stage('OC'){
			steps {
				sh 'oc login --token=AwFWoKk2-IynQ4FoxRkb-nDSnUL21ufUcWABZAPdzrI --server=https://api.us-east-1.starter.openshift-online.com:6443'
				sh 'oc projects'
			}
		}
	}
}
