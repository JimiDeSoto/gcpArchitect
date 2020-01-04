### pobranie plikow
wget https://storage.googleapis.com/testdatachm/sampledata/imagedata.tar.gz

### rozpakowanie

tar -xvf imagedata.tar.gz

### Utworzenie bucketu
gsutil mb -c standard -l EUR4 gs://rk-home-week6


### utworznie dedykowanego konta serwisowego
gcloud iam service-accounts create bucketowy-podgladacz --display-name="Podgladacz bucketow"

### dla usprawneinia przypisanie konta do zmiennej srodowiskowej
kontosv="bucketowy-podgladacz@szkola-chmury-agcp.iam.gserviceaccount.com"

### wygenerowanie prywatnego klucza na potrzeby udostepniania zawartosci bucket
gcloud iam service-accounts keys create priv-key.json \
  --iam-account $kontosv

gsutil signurl -d 100d priv-key.json gs://rk-home-week6/*
gsutil iam ch $kontosv:objectViewer gs://rk-home-week6/


### wygenerowanie signurl 


gsutil signurl -d 1m priv-key.json gs://rk-home-week6/pictures/*


### kopiowanie plikow.
 gsutil -m cp -r * gs://rk-home-week6/


gsutil signurl -d 7d  priv-key.json gs://rk-home-week6/fungs/*
gsutil signurl -d 7d  priv-key.json gs://rk-home-week6/garden/*
gsutil signurl -d 7d  priv-key.json gs://rk-home-week6/homeplants/*
gsutil signurl -d 7d  priv-key.json gs://rk-home-week6/rocks/*


gsutil versioning set on gs://rk-home-week6

gsutil lifecycle set policy1.json gs://rk-home-week6
 