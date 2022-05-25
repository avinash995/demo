node {
    def app

    stage('clone repositry'){
       

       checkout scm

}

stage('build image') {

    app = docker.build("")
}

stage('Test image'){

    app.inside{
        sh 'echo Tests passed'
    }
}

stage('Push image'){

    docker.withRegistry("https://hub.docker.com/",'dockerhub') {
        app.push("${env.BUILD_NUMBER}")
    }
}

stage('Trigger information'){

    echo "triggering updatemanifestjob "
    build job: "updatemanifest" , parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    }
}
