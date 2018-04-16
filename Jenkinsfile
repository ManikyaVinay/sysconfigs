
node {
    def reposlist = []
    echo 'Checkout is in progress..'
    
    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
    doGenerateSubmoduleConfigurations: false, 
    submoduleCfg: [], 
    userRemoteConfigs: [[credentialsId: 
    'aafadd97-6037-457e-9ea5-3f20b7c61e02', 
    url: 'https://github.com/ManikyaVinay/sysconfigs.git']]])
    
    echo 'Checkout is completed..'
    
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
