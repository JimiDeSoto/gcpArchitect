# Przygotowanie template dla PoC
1. Utworzenie maszyny z Joomla (marketplace).
2. Utworzenie template z instancji Joomla
''''
gcloud compute instance-templates create mountkirk-tmpl-1  \
    --source-instance joomla-1-vm \
    --configure-disk=device-name=joomla-1-vm,instantiate-from=joomla-v20190923,auto-delete=true\
    --source-instance-zone=europe-west1-d
''''
''''
gcloud compute instance-templates create mountkirk-tmpl-1 \
    --source-instance=joomla-1-vm \
    --source-instance-zone=europe-west1-d \
    --configure-disk= \
        device-name=joomla-1-vm, \
        instantiate-from=joomla-v20190923, \
        auto-delete=true
''''


