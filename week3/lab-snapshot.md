
# Configuracja srodowiska

gcloud config configurations create <>

gcloud config set project <>

gcloud compute regions list

gcloud config set account <>

gcloud config set compute/region us-cetral1

## Budowa VM
gcloud compute instances create vm1a --machine-type=f1-micro --zone=us-central1-a

## Dysk utworzenie nowego dodatkowego
gcloud compute disks create vmdisk1a --size=50GB --zone=us-central1-a

gcloud compute disks list

## Podpiecie dysku do maszyny
gcloud compute instances attach-disk vm1a --disk=vmdisk1a --zone=us-central1-a

#uwaga dysk trzeba sformatowac i zamontowac w sytemie

#  Konfiguracja VM1a (Dysk)
lsblk
## Formatowanie
mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb

## Montowanie
mkdir -p /disk2
mount -o discard,defaults /dev/sdb /disk2
chmod a+w /disk2/

## Snapshot dysku
gcloud compute disks snapshot vmdisk1a --snapshot-names vmdisk1a-snapshot-1 --zone=us-central1-a
gcloud compute snapshots list


## Utworzenie vm w innej zonie
gcloud compute instances create vm1c --machine-type=f1-micro --zone=us-central1-c

## Utworzenie dodatkowego dysku na podstawie snapshota (poprzedniego)
gcloud compute disks create vmdisk1c --source-snapshot=vmdisk1a-snapshot-1 --zone=us-central1-c
gcloud compute instances attach-disk vm1c --disk=vmdisk1c --zone=us-central1-c

#  Konfiguracja VM1c (Dysk)
## Zamontowanie dysku
mkdir -p /disk2
mount -o discard,defaults /dev/sdb /disk2
chmod a+w /disk2/

# Usuwanie dowiska
## odpiecie dyskow
gcloud compute instances detach-disk vm1a --disk=vmdisk1a --zone=us-central1-a
gcloud compute instances detach-disk vm1c --disk=vmdisk1c --zone=us-central1-c

## usuniecie vm
gcloud compute instances delete vm1a --zone=us-central1-a
gcloud compute instances delete vm1c --zone=us-central1-c

## usuniecie dyskow
gcloud compute disks delete vmdisk1a --zone=us-central1-a
gcloud compute disks delete vmdisk1c --zone=us-central1-c

## usuniecie snapshota
gcloud compute snapshots delete vmdisk1a-snapshot-1