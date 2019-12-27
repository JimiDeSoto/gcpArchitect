# Canary updates

https://martinfowler.com/bliki/CanaryRelease.html
## Create template - template1

gcloud compute instance-templates create template1 \
    --image-family debian-9 \
    --image-project debian-cloud \
    --tags=http-server \
    --machine-type=f1-micro \
    --metadata=startup-script=\#\!/bin/bash$'\n'sudo\ apt-get\ update\ $'\n'sudo\ apt-get\ install\ -y\ nginx\ $'\n'sudo\ service\ nginx\ start\ $'\n'sudo\ sed\ -i\ --\ \"s/Welcome\ to\ nginx/Version:1\ -\ Welcome\ to\ \$HOSTNAME/g\"\ /var/www/html/index.nginx-debian.html

## Create template - template2

gcloud compute instance-templates create template2 \
    --image-family debian-9 \
    --image-project debian-cloud \
    --tags=http-server \
    --machine-type=f1-micro \
    --metadata=startup-script=\#\!/bin/bash$'\n'sudo\ apt-get\ update\ $'\n'sudo\ apt-get\ install\ -y\ nginx\ $'\n'sudo\ service\ nginx\ start\ $'\n'sudo\ sed\ -i\ --\ \"s/Welcome\ to\ nginx/Version:2\ -\ Welcome\ to\ \$HOSTNAME/g\"\ /var/www/html/index.nginx-debian.html

## Create Managed Instance Group

gcloud compute instance-groups managed create my-group --base-instance-name=my-group --template=template1 --size=4 --zone us-central1-a

## Create canary update for half of instances

gcloud compute instance-groups managed rolling-action start-update my-group --version template=current-template1 --canary-version template=template2,target-size=50% --zone us-central1-a


## Update rest of instance with new template

gcloud compute instance-groups managed rolling-action start-update my-group --version template=current-template2 --max-unavailable 100% --zone us-central1-a


gcloud compute firewall-rules create default-allow-http \
    --direction=INGRESS \
    --priority=1000 \
    --network=default \
    --action=ALLOW \
    --rules=tcp:80 \
    --source-ranges=0.0.0.0/0 \
    --target-tags=http-server