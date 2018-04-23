
node{
    checkout scm
    
    def myrepos = readJSON file: "repos.json";
    def repos_list = myrepos['repos']
    
    repos_list.each{
        def gitUrl = "https://api.github.com/repos/ManikyaVinay/${it.name}/commits"
        println "gitURl , ${gitUrl}"

        // Reading projects from GitLab REST API
        def projectURL = new URL("${gitUrl}")
        println "projecturl, ${projectURL}"
        def commits = new groovy.json.JsonSlurper().parse(projectURL.newReader())
        def lastestcommitid = commits[0].sha
        if( (${it.lastcommit} != lastestcommitid) || !${it.lastcommit}?.trim() ) {
            println "commits are different/lastcommit is empty(first time build), so should call shared process lib"
            //here we should call shared process lib function
        }
        else{
            println "no need of shared process lib as lastcommit is not empty or commits are same"
        }
        
        it.lastcommit = latestcommitid
        println 'after updating lastcommit'
        println it
    }
}
