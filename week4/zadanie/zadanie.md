# Zadnie 1
## Utworzenie maszyny
gcloud compute images list
gcloud compute instances create vm01 --machine-type=f1-micro --preemptible --zone=europe-west1-b

## Utworzenie bucket
gsutil mb gs://gcp-bucket-rk01

## Stworzenie i skopiowanie przykdowych plikow do bucket
gsutil cp *  gs://gcp-bucket-rk01



## Wyswietlenie zawartoci bucket
gsutil ls  gs://gcp-bucket-rk01

## Wyswietlenie zawartosci pliku
gsutil cat  gs://gcp-bucket-rk01/faktura2

## Usuniecie pliku
gsutil rm  gs://gcp-bucket-rk01/faktura1

# Zadanie 2

## Utworz keyring

gcloud kms keyrings create secure-doc --location global

## utworz pare kluczy
gcloud kms keys create key01-doc \
  --location global \
  --keyring secure-doc \
  --purpose asymmetric-encryption \
  --default-algorithm rsa-decrypt-oaep-2048-sha256 \
  --protection-level software






# utworzenie 2 maszyny

gcloud compute instances create vm01 \
    --machine-type=f1-micro --preemptible --zone=europe-west1-b \
    --service-account=crypto-bucket@szkola-chmury-agcp.iam.gserviceaccount.com \
    --scopes storage-rw,https://www.googleapis.com/auth/cloudkms

gcloud compute instances create vm02 \
    --machine-type=f1-micro --preemptible --zone=europe-west1-b \
    --service-account=crypto-bucket@szkola-chmury-agcp.iam.gserviceaccount.com \
    --scopes storage-rw,https://www.googleapis.com/auth/cloudkms


# Uprawnienia do bucket
gsutil iam ch serviceAccount:crypto-bucket@szkola-chmury-agcp.iam.gserviceaccount.com:roles/storage.legacyBucketWriter gs://gcp-bucket-rk01/



# temp
gcloud compute instances create vm02 --machine-type=f1-micro --preemptible --zone=europe-west1-b

# temp
#umozliwienie zapisu do bucket, zmiana scope
#utworzenie nowego service account
gcloud iam service-accounts create crypto-bucket --display-name=crypto-bucket
gcloud iam service-accounts list

gcloud compute instances stop vm01 vm02

gcloud compute instances set-service-account vm01 \
   --zone europe-west1-b \
   --service-account 777753131068-compute@developer.gserviceaccount.com \
   --scopes storage-rw, https://www.googleapis.com/auth/cloudkms,

gcloud compute instances set-service-account vm02 \
   --zone europe-west1-b \
   --service-account 777753131068-compute@developer.gserviceaccount.com \
   --scopes storage-rw, https://www.googleapis.com/auth/cloudkms
##

# umozliwienie korzystania z KMS, dopdanie scope



# temp
gcloud compute instances set-service-account vm01 \
   --zone europe-west1-b \
   --service-account 777753131068-compute@developer.gserviceaccount.com \
   --scopes=https://www.googleapis.com/auth/cloudkms
# temp
gcloud compute instances set-service-account vm02 \
   --zone europe-west1-b \
   --service-account 777753131068-compute@developer.gserviceaccount.com \
   --scopes=https://www.googleapis.com/auth/cloudkms



gcloud iam roles create gerwazy --project szkola-chmury-agcp --file role-crypt.yaml

gcloud projects add-iam-policy-binding szkola-chmury-agcp \
    --member serviceAccount:crypto-bucket@szkola-chmury-agcp.iam.gserviceaccount.com \
    --role projects/szkola-chmury-agcp/roles/gerwazy
# temp
gcloud projects add-iam-policy-binding szkola-chmury-agcp --member serviceAccount:777753131068-compute@developer.gserviceaccount.com --role projects/szkola-chmury-agcp/roles/gerwazy



gcloud compute instances start vm01 vm02

# Szyfrowanie pliku

# Asymetryczne
## pobranie klucza publicznego
gcloud kms keys versions \
  get-public-key 1 \
  --location global \
  --keyring secure-doc \
  --key key01-doc \
  --output-file ~/key01-doc.pub

echo "Tajna wiadomosc" > crypt-mini.md

openssl pkeyutl -in crypt-mini.md \
  -encrypt -pubin \
  -inkey ~/key01-doc.pub \
  -pkeyopt rsa_padding_mode:oaep \
  -pkeyopt rsa_oaep_md:sha256 \
  -pkeyopt rsa_mgf1_md:sha256 > crypt-mini.md.enc

gcloud kms asymmetric-decrypt \
  --location global \
  --version=1 \
  --keyring secure-doc \
  --key key01-doc \
  --ciphertext-file  crypt-mini.md.enc\
  --plaintext-file ~/crypt-mini.md.dec

# Symetryczne
gcloud kms keys create key02-sym-doc \
    --location global \
    --keyring secure-doc \
    --purpose encryption \
    --rotation-period=30d \
    --next-rotation-time=2020-01-22T20:00:00.000Z


gcloud kms encrypt \
  --location=global  \
  --keyring=secure-doc \
  --key=key02-sym-doc \
  --plaintext-file crypt.md \
  --ciphertext-file ~/crypt.md.enc

  gcloud kms encrypt \
  --location=global  \
  --keyring=secure-doc \
  --key=key02-sym-doc \
  --plaintext-file ~/crypt.md \
  --ciphertext-file ~/crypt.md.enc

gcloud kms decrypt \
  --location global \
  --keyring secure-doc \
  --key key02-sym-doc \
  --ciphertext-file  crypt.md.enc\
  --plaintext-file ~/crypt.md.dec



# temp
gcloud kms encrypt --location=global --keyring=secure-doc --key=key01-doc --plaintext-file=crypt.md --ciphertext-file=crypt.md.enc

# Tworzenie roli

gcloud iam roles create cryptoCSviewer --project szkola-chmury-agcp --file role-crypto-cs.yaml

gcloud projects add-iam-policy-binding szkola-chmury-agcp \
    --member user:testuser@overseer.eu \
    --role projects/szkola-chmury-agcp/roles/cryptoCSviewer
