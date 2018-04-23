
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
        println "lastestcommitid, ${lastestcommitid}"
        if( (it.lastcommit != lastestcommitid) || !it.lastcommit?.trim() ) {
            println "commits are different/lastcommit is empty(first time build), so should call shared process lib"
            //here we should call shared process lib function
        }
        else{
            println "no need of shared process lib as lastcommit is not empty or commits are same"
        }
        
        it.lastcommit = lastestcommitid
        println 'after updating lastcommit'
        println it
    }
    println "final list after updations"
    println repos_list

    def jsonBuilder = new groovy.json.JsonBuilder()

    println("jsonBuilder")
    def root = jsonBuilder repos: repos_list

    print json.toString()
}
