# Transactions Operator
<h1 align="center">
  <br>
 
  <br>
      Mongorest operator for Openshift
  <br>
  <br>
</h1>

<h4 align="center">Powered by Openshift and OperatorSDK</h4>

<p align="center">
  <a>
    <img src="https://img.shields.io/travis/keppel/lotion/master.svg"
         alt="Travis Build">
  </a>
</p>
<br>
Allows you to develop mongo microservices just by defining the yamls on a openshift cluster 

## Install Operator on Openshift

1. clone the repo
```
$ git clone https://github.com/IntelliBankVi/microservice-transactions.git
```
2. install ***serviceaccount***, ***rolebinding***, ***role***, ***crd***, and ***operator***
```
$ oc apply -f deploy/service_account.yaml
$ oc apply -f deploy/role.yaml
$ oc apply -f deploy/role_binding.yaml
$ oc apply -f deploy/operator.yaml
$ oc apply -f deploy/crds/mongorest_v1alpha1_mongorest_crd.yaml
```
## Creat your first MongoDB CRUD Microservice in minutes!
1. create mongorest yaml, example reservation microservice. This is a reservation microservice which performs crud operations on mongodb database to store firstname,  lastname, and uid. 
``` YAML
apiVersion: mongorest.ibm.com/v1alpha1
kind: Mongorest
metadata:
  name: transactionmicroservice
spec:
  replicaCount: 3 #number of replica needed
  namespace: "anchal"
  metadata:
    name: transaction-microservice
  mongodb: 
    host: "mongodb.anchal" # connection info of mongodb
    username: "YWRtaW4="
    password: "YWRtaW4="
    endpoint: "transaction"
    db: "sampledb"
    schema: "Transaction"
    model: "{'creditcardnumber':'Number','transactiondate':'String','transactiontime':'String','vendor':'String','vendortype':'String' ,'totalprice':'Number'}" # model of your mongo schema
  buildconfig: 
    imagename: "transaction-microservice:latest"
  routes:
    host: "transaction-microservice-anchal.apps.192.168.64.21.nip.io"  # application route
```
4. Apply these YAML configuration
