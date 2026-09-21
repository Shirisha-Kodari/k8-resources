## EBS (elatsic block storage ):
 # 2 tyeps :
 # 1. ebs statis provisioning 
 # 2. ebs dynamic provisiong 
# EFS 
# 1. efs static provisioning 
# 2. efs dynamic provisioning 

# ebs static provisiong:

* steps:
before that 
create cluster 

-> pv ,pvc ,sc wrappers in k8 
-> crate disk manually 
-> disk shoulb be cteated in the same az in same ec2 
 ebs disk shloud be in the same az in ec2 
->install drivers ( beacuase k8 connect aws)
->retain means if pod deleted eventhough date will be there 
-> pvc requesi for stoarge 
->pv repsernation of volume in k8 
-> give volume name newly created voulme through manually 
->create role and attcah to workernode 
that role shloud have ebscsidriver policy 
because it used for the volume attch to worketnode 

* kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.62"

1.43 ->version 
-> ec2 node shloud have perimssion to connect EBS 
-> create pv and pvc with automate 

->pv->pvc->pod 
we define pvc inside pod and give conatiner path ot host path 
login to nginx conatiner and -> cd /usr/share/nginx/html->echo "<h1> hi iam from ebs statis</h1>" > index.html

# ebs dynamic proisioning :

steps:
create storage class 
sc creates the disk and pv , so no need create disk and pv
add permisriion ebscsidriver to node 

# EFS Static: 

kubectl kustomize \
    "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/ecr/?ref=release-2.1" > private-ecr-driver.yaml
    -> vim private-ecr-driver.yaml
    -> kubectl apply private-ecr-driver.yaml 
    ->go to node and then click security ->iam role click on that ->add permission->efscsidriver policy 
    here create nfs and eksctl create own vpc and sg 
    -> here created one sg we allow the source node sg and open the port nfs 2049 form ec2 sg 
    ->create pv,pvc and mount to pod 

# reasons:
check drivers installed or not 
check permsiion whether policy attch to node or not 
pvc bound to pv or not 
volume and node in the same az 
each project has own file syatem we can create file sytem for each service like cart,user 
and here created access points 