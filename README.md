# DevOps Milestone 1

    Divya Jain (djain2)
    Shrenik Gala (sngala)
    Prashant Gupta (pgupta7)

We have used a simple **NodeJs** application for this stage of the project which just responds with a simple message when hit with a request. A test case checks for the string returned, and fails if the string is different than the one in the test case. We have configured **Jenkins** on our machine as our build server.

##Build section

####Triggered Build

We used a local git repository, and we have added a post-commit hook to each of the developer and release branches to build a corresponding job on Jenkins. This is done through the following code in post-commit hook:


    if [ `git rev-parse --abbrev-ref HEAD` = "dev" ]; then
        curl http://localhost:8080/job/dev-build-job/build
    elif [ `git rev-parse --abbrev-ref HEAD` = "release" ]; then
         curl http://localhost:8080/job/release-build-job/build
    fi

Depending on the branch on which the commit happened, the curl command sends a build job notification to Jenkins.

####Dependency Management + Build Script Execution

For this section, we have executed some commands while the job is being executed on Jenkins:

     cd $WORKSPACE
     npm clean
     npm install
     ./script/test

####Build Status + External Post-Build Job Triggers

- The build status can be seen on the Jenkins page, as shown below:

- We have triggered post-build job triggers through emails. We are sending an email on both success and failure of build jobs.

####Multiple Branches, Multiple Jobs

This is done through the Git hooks present in the post-commit file. The code is:

    if [ `git rev-parse --abbrev-ref HEAD` = "dev" ]; then
        curl http://localhost:8080/job/dev-build-job/build
    elif [ `git rev-parse --abbrev-ref HEAD` = "release" ]; then
         curl http://localhost:8080/job/release-build-job/build
    fi

So if we are in the dev branch, it will trigger the dev build job, and if we are in the release branch, it will trigger the release branch.

####Build History and Display over HTTP
    
We can see the build history on our Jenkins server running on: http://localhost:8080
