node {
    checkout(scm)
    loadEnvironmentVariables("parameters/NONPROD.properties") 
    // withCredentials([usernamePassword(credentialsId: 'vault', passwordVariable: 'VAULT_PASSWORD', usernameVariable: 'VAULT_USER')]) {
       
        stage ('CF Templates Build'){
            sh 'export ANSIBLE_ASK_SUDO_PASS=true'
            sh 'ansible-playbook site.yml -e "env=$BRANCH_NAME"  --tags "prepare"'
            // sh "ansible-playbook site.yml --extra-vars="BRANCH_NAME=$(BRANCH_NAME)" --tags "prepare""
        }

        // stage ('CF Templates Validation'){
        //     sh "make BRANCH='${BRANCH_NAME}' validate-CF"
        // }

        // stage ('CF Templates Deployment'){
        //     sh "make BRANCH='${BRANCH_NAME}' deploy-CF" 
        // }

        // stage ('Instance Validation'){
        //     sh "make BRANCH='${BRANCH_NAME}' validate-instance" 
        // }

        // stage ('Meduawiki Installation'){
        //     sh "make BRANCH='${BRANCH_NAME}' install-mediawiki"
        // }

        // stage ('Validate Validatation'){
        //     sh "make BRANCH='${BRANCH_NAME}' validate-mediawiki"
        // }
    // } 
}    

def loadEnvironmentVariables(path){ 
    def props = readProperties  file: path
    keys= props.keySet()
    for(key in keys) {
        value = props["${key}"]
    }
}