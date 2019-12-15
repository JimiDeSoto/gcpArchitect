## Przygotowanie portal
# wyklikanie z portalu maszyny wordpres szk1
# wylikanie backetu storage labimagerk01

## Tworzenie image z istniejacej maszyny
gcloud compute disks list
gcloud compute images create my-image --source-disk=szk1-vm --source-disk-zone=us-central1-a

//trzeba zgodzic sie na API u uprawnienia, uprawnienia moga synchronizowac sie dluzszy czas
gcloud compute images export --destination-uri gs://labimagerk01/wpimage1.tar.gz --image my-image
