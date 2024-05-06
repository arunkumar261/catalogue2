#!groovy
@Library('roboshop-shared-library') _

//responsibilt to pass wt type of appln and component is this to pipeline decision

def configMap = [
    application: "nodejsVM",
    component: "catalogue"

]

if( ! env.BRANCH_NAME.equalsIgnoreCase('main')){
    pipelineDecission.decidePipeline(configMap)

}else {
    echo "This is PRODUCTION, deal with CR Process"
}