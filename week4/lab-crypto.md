# Prep
## utworrzenie bucketa
gsutil mb gs://gcp-kms-bucket

## pobranie przykdowych danych do szyfrowania
git clone https://github.com/lasekg/sample-data

## szyfrowanie przez endp[oint KMS wymaga aby dane byy w formacie base64
TEXT$=(cat file01.txt | base64 -w0)

# KMS 
## uruchomienie usugi KMS
gcloud services enable cloudkms.googleapis.com

## Utworzenie key ring
gcloud kms keyrings create mykeyring --location global

## tworzenie klucza szyfrownia
gcloud kms keys create mykey --location global --keyring mykeyring --purpose encryption


## Pobranie credetials do print-access-token na stacje

gcloud auth application-default

## Wywoniew API do szyfrowania danych
```
curl -v "https://cloudkms.googleapis.com/v1/projects/szkola-chmury-agcp/locations/global/keyRings/mykeyring/cryptoKeys/mykey:encrypt" -d "{\"plaintext\":\"$TEXT\"}" -H "Authorization:Bearer $(gcloud auth application-default print-access-token)" -H "Content-Type: application/json" | jq .ciphertext -r > <file1.enc>
```
## Wywołanie API do odszyfrowania danych
```
curl -v "https://cloudkms.googleapis.com/v1/projects/szkola-chmury-agcp/locations/global/keyRings/mykeyring/cryptoKeys/mykey:decrypt" -d "{\"ciphertext\":\"$(cat file1.enc)\"}" -H "Authorization:Bearer $(gcloud auth application-default print-access-token)" -H "Content-Type: application/json"
```

## Skopiowanie
gsutil cp file01.enc  gs://gcp-kms-buckeet
