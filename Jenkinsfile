
node {
    def reposlist = []
       
    def myrepos = readJSON file: "repos.json";
    def repos_list = myrepos['repos']

    echo "repo1: ${myrepos.repos[0].url}"
    
    reposlist = ['repo1','repo2']
    repos_list.each{
        echo "triggers a build for scan of repo, ${it.url}\n"
        dir("${it.name}"){
            def response = httpRequest "http://localhost:8080/job/autosys-pipeline/buildWithParameters?token=autosys&repo_url=${it.url}"
            println('Status: '+response.status)
            println('Response: '+response.content)
        }
        echo "completed\n"
    }

}
