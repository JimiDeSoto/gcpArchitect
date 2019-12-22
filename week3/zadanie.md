
## Utworzenie bucket "ag-week3"
gsutil mb -c standard -l europe-west3 gs://ag-week3

## Kopiowanie obrazu apliakcji do stworzonego bucket
gsutil cp gs://mountkirk-games-image/mountkirk-games.vmdk gs://ag-week3/

## imprort obrazu do repozytorium obrazow projektu
gcloud compute images import mountkirk-test01 \
--os=debian-9 \
--source-file=gs://ag-week3/mountkirk-games.vmdk
### uruchomienie aplikacji w wybranych regionach
gcloud compute instances create vm-mountkirk-euw --zone=europe-west6-a --machine-type=n1-standard-1 --tags=http-server,https-server --image=mountkirk-test01


gcloud beta compute instances create vm-mountkirk-01 \
--zone=europe-west6-a --machine-type=n1-standard-1 \
--tags=http-server,https-server --image=mountkirk-test01



gcloud compute firewall-rules create default-allow-https \
--direction=INGRESS \
--priority=1000 \
--network=default \
--action=ALLOW \
--rules=tcp:443 \
--source-ranges=0.0.0.0/0 \
--target-tags=https-server