## I
### Utworzenie bucket
gsutil mb -c standard -l europe-west3 gs://gcp-bucket-week6-01/

### Kopiowanie plikow
gsutil -m cp * gs://gcp-bucket-week6-01/ //mozna doda -m mutli wiele plikow

### ilosc danych w bucket
gsutil du -s gs://gcp-bucket-week6-01/    // moze dugo trwa, przy duzych backetach stackdriver monitoring, raz dziennie                                             //mierzony rozmiar bucket i zapisywanty w logach


### uproszczenie 
bucket1="gs://gcp-bucket-week6-01/"

### metas daner bucketa
gsutil ls -L -b $bucket1

### drugi
gsutil mb -c standard -l europe-west3 gs://gcp-bucket-week6-02/

### kopiowanie miedzy buckwtami

gsutil cp gs://gcp-bucket-week6-01/** gs://gcp-bucket-week6-02/


### wyswietlenie zawartosci
gsutil ls -r gs://gcp-bucket-week6-01/

### zmiana klasy storage
gsutil defstorageclass set nearline gs://gcp-bucket-week6-02/
gsutil defstorageclass get gs://gcp-bucket-week6-02/

### skopiowanie pliku
gsutil cp plik.txt gs://gcp-bucket-week6-02/

### usuwanie
gsutil rm -r gs://gcp-bucket-week6-01/
gsutil rm -r gs://gcp-bucket-week6-02/


## II

### utworznie backeta
gsutil  mb gs://gcp-bucket-week6-01

gsutil -m cp * gs://gcp-bucket-week6-01

### ustawieni polityki retencji
gsutil retention set 60s gs://gcp-bucket-week6-01

### nadanie acl do publicznego dostepu do pliku
gsutil acl ch -u AllUsers:R gs://gcp-bucket-week6-01/serce.jpg


## generowanie podpisanego url
### instalacja pyopenssl
sudo pip3 install pyopenssl

### weryfikacja dostepnych konty serwisowych
gcloud iam service-accounts list

### generowanie klucza
gcloud iam service-accounts keys create key.json --iam-account 777753131068-compute@developer.gserviceaccount.com















