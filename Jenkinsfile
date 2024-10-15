@Library('sym-pipeline@PRD') _

node("build-directory-jenkins-agent") {

    String project = 'directory-scimple'
    String projectOrg = 'SymphonyOSF'
    withEnv([
            "GIT_REPO=${project}",
            "GIT_ORG=${projectOrg}",
            "GIT_BRANCH=${env.BRANCH_NAME}",
    ]) {

        stage('Build and test jar') {
            gitCheckout()
            mvn('clean package -DskipIts')
        }

        stage("Publish the packages") {
             sh"ls -a"
        }
    }
}

def mvn(String cmd) {
    withCredentials([file(credentialsId: 'maven-settings', variable: 'settings_xml')]) {
        sh 'mkdir -p /home/jenkins/.m2'
        sh 'base64 -d \$settings_xml > /home/jenkins/.m2/settings.xml'
        sh "mvn -B ${cmd}"
    }
}
