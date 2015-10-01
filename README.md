# DevOps Milestone 1

    Divya Jain (djain2)
    Shrenik Gala (sngala)
    Prashant Gupta (pgupta7)

We have used a simple NodeJs application for this stage of the project which just responds with a simple message when hit with a request. A test case checks for the string returned, and fails if the string is different than the one in the test case.

###Build section

####Triggered Build

We used a local git repository, and we have added a post-commit hook to each of the developer and release branches to build a corresponding job on Jenkins. This is done through the following code:


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


    
