
node {
    checkout scm
    def reposlist = []
       
    def myrepos = readJSON file: "repos.json";
    def repos_list = myrepos['repos']

    echo "environment variables:"
    println env
    println env.getEnvironment()
    println GIT_COMMIT 
    println GIT_URL 
    println GIT_BRANCH
    
    reposlist = ['repo1','repo2']
    repos_list.each{
        echo "triggers a build for scan of repo, ${it.url}\n"
        dir("${it.name}"){
            ///def response = httpRequest "http://localhost:8080/job/autosys-pipeline/buildWithParameters?token=autosys&repo_url=${it.url}"
            //println('Status: '+response.status)
            //println('Response: '+response.content)
            build job: 'autosys-pipeline', parameters: [[$class: 'StringParameterValue', name: 'repo_url', value: it.url]]
        }
        echo "completed\n"
    }

}
