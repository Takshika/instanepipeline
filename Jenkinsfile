node {
    checkout(scm)
    loadEnvironmentVariables("parameters/NONPROD.properties") 
    withCredentials([usernamePassword(credentialsId: 'vault', passwordVariable: 'VAULT_PASSWORD', usernameVariable: 'VAULT_USER')]) {
       
        stage ('CF Templates Build'){
            sh 'ansible-playbook site.yml -e "env=$BRANCH_NAME"  --tags "prepare"'
        }

        stage ('CF Templates Validation'){
            sh 'ansible-playbook site.yml -e "env=$BRANCH_NAME"  --tags "validate"'
        }

        stage ('CF Templates Deployment'){
            sh 'ansible-playbook site.yml -e "env=$BRANCH_NAME"  --tags "deploy"'
        }

        stage ('Instance Validation'){
            sh 'python scripts/update_hosts.py --extra-vars "@vaults/secret.yml", region=us-east-1'
        }

        // stage ('Meduawiki Installation'){
        //     sh "make BRANCH='${BRANCH_NAME}' install-mediawiki"
        // }

        // stage ('Validate Validatation'){
        //     sh "make BRANCH='${BRANCH_NAME}' validate-mediawiki"
        // }
    } 
}    

def loadEnvironmentVariables(path){ 
    def props = readProperties  file: path
    keys= props.keySet()
    for(key in keys) {
        value = props["${key}"]
    }
}