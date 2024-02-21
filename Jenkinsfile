pipeline {

    agent any
    parameters {
        string(name: 'JSON_DATA', defaultValue: '{"hosts": ["host@IP1"]}', description: 'Enter JSON data containing list of IP addresses')
}
    stages {
 stage('Execute Ansible Playbook') {
            steps {
                script {
                    def jsonData = readJSON text: params.JSON_DATA
                    def hosts = jsonData.hosts.collect { it }
                    def inventoryPath = "${WORKSPACE}/inventory"
                    writeFile file: inventoryPath, text: "[nodes]\n" + hosts.join('\n')
                    sh "ansible-playbook -i ${inventoryPath} /var/lib/jenkins/workspace/playbook.yml"
                }
            }
        }
    }

    }
