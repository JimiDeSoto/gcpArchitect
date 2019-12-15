## Prep
# Utworzenie maszyny
gcloud compute instances create vm1a --machine-type=f1-micro --zone=us-central1-a
## Migracja maszyny
# Migracja miedzy zonami
gcloud compute instances move vm1a --zone us-central1-a --destination-zone us-central1-b
# Uwagi
#Maszyna jest zatrzymywana i przenoszona, zostaje stare pub IP.  

# Migarcaj miedzy regionami
gcloud compute instances list
gcloud compute disks list

# Wylacz autu delete dysku
gcloud compute instances set-disk-auto-delete vm1a --zone us-central1-b --disk vm1a --no-auto-delete
#kilak dyskow po spacji
# backup bezpieczenstwa
gcloud compute disks snapshot vm1a --snapshot-names backup-vm1asnapshot --zone us-central1-b
# backup do obrobki
gcloud compute disks snapshot vm1a --snapshot-names vm1asnapshot --zone us-central1-b

gcloud compute  snapshots list

gcloud compute instances describe vm1a --zone us-central1-b

# utworzenie dysku w nowym regione ze snapshot
gcloud compute disks create vm1eu --source-snapshot vm1asnapshot --zone europe-west6-b

# utworzenie vm w nowym regione z dyskiem zmigrowanym

gcloud compute instances create vm1eu --machine-type f1-micro --zone europe-west6-b --disk name=vm1eu,boot=yes,mode=rw

#todo uworzyc firewall rule

# czyszczenie satrej instancji
gcloud compute snapshots delete vm1asnapshot
gcloud compute snapshots delete backup-vm1asnapshot
gcloud compute instances delete vm1a --zone us-central1-b
gcloud compute disks delete vm1a --zone us-central1-b


# Dodajemy tag do Compute Engina dla firewalla:
gcloud compute instances add-tags myinstanceb --tags=nazwa_tagu