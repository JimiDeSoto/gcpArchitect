# Przygotowanie template dla PoC
## Utworzenie maszyny z Joomla (marketplace).
## Utworzenie template z instancji Joomla

gcloud compute instance-templates create mountkirk-tmpl-1 \
    --source-instance=joomla-1-vm \
    --source-instance-zone=europe-west1-d
 

## Utworzenie maszyny z WordPress (marketplace)
## Utworzenie template z instancji Wordpress.


gcloud compute instance-templates create mountkirk-tmpl-2 \
    --source-instance=wordpress-1-vm\
    --source-instance-zone=europe-west1-b

## Wynik
$ gcloud compute instance-templates list
NAME                 MACHINE_TYPE  PREEMPTIBLE  CREATION_TIMESTAMP
mountkirk-tmpl-1     g1-small                   2019-12-29T09:19:27.514-08:00
mountkirk-tmpl-2     g1-small                   2019-12-29T09:16:22.075-08:00

## Utworzenie MIGs regionalnego dla EU
gcloud compute instance-groups managed create mountkirk-mig-eu-west1 \
    --template mountkirk-tmpl-1 --base-instance-name mountkirk-eu-v1 \
    --size 3 --region europe-west1

## Ustawienie autoscalowania
gcloud compute instance-groups managed set-autoscaling mountkirk-mig-eu-west1 \
    --cool-down-period=90 \
    --target-cpu-utilization 0.2 \
    --max-num-replicas 6 \
    --region europe-west1

## Monitoring
gcloud beta compute instance-groups managed wait-until mountkirk-mig-eu-west1 \
    --stable \
    --region europe-west1


## canary testing w regionie eu, aktualizacja 30% instancji.
gcloud compute instance-groups managed rolling-action start-update mountkirk-mig-eu-west1 \
    --version template=mountkirk-tmpl-1 \
    --canary-version template=mountkirk-tmpl-2,target-size=30% \
    --max-surge=3 --max-unavailable=0 --region europe-west1


## aktualizacja pozosatych instancji maszyn
gcloud compute instance-groups managed rolling-action start-update mountkirk-mig-eu-west1 \
    --version template=mountkirk-tmpl-2 \
    --max-surge=3 --max-unavailable=0 --region europe-west1


## Utworzenie MIGs regionalnego dla US
gcloud compute instance-groups managed create mountkirk-mig-us-east1 \
    --template mountkirk-tmpl-1 --base-instance-name mountkirk-us-v1 \
    --size 3 --region us-east1

## Ustawienie autoscalowania
gcloud compute instance-groups managed set-autoscaling mountkirk-mig-us-east1 \
    --cool-down-period=90 \
    --target-cpu-utilization 0.2 \
    --max-num-replicas 3 \
    --region us-east1


