## Create JSON file on your computer called lifecycleman.json:

{
"lifecycle": {
    "rule": [
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 30,
      "isLive": true
    }
    },
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 10,
      "isLive": false
    }
    }
    ]
    }
}   

{
"lifecycle": {
    "rule": [
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 30,
      "isLive": true
    }
    },
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 10,
      "isLive": false
    }
    }
    ]
    }
}   

## aplikacja 

gsutil lifecycle set lifecycleman.json gs://gcp-bucket-week6-01/ 
### c zasem polityki wejda po 24 godzinach
gsutil lifecycle get gs://gcp-bucket-week6-01/


#Case 1
## ustawiamy inteligentny storage do wymiany plikow
## po 30 dniach pliki usuwany automatycznie, jesli ktos nie zdarzy to jeszcz 10 dni pozosyal w archiwum
## 30+10 usuwamy cakowicie.


### sprawdzenie wersji
gsutil versioning get gs://week-6


### ustaw wersionowanie
gsutil versioning set on  gs://week-6

### 
{
"lifecycle": {
    "rule": [
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 30,
      "isLive": true
    }
    },
    ### po usunieciu zostanie utworzona wersja pliku
    {
    "action": {"type": "Delete"},
    "condition": {
      "age": 10,
      "isLive": false
    }
    }
    ]
    }
    ### za dziala na plik z wersja
}   

### aplikacja
gsutil lifecycle set deletepolicy.json gs://week-6/

### Versionowanie

gsutil cp deletepolicy.json gs://week-6/policy/deletepolicy.json
gsutil rm  gs://week-6/policy/deletepolicy.json

### pokaz wersje zapisana po usunieciu

gsutil ls -a gs://week-6/policy

### odtworz wersje
gsutil cp gs://week-6/policy/deletepolicy.json#1578149843382863 gs://week-6/policy/policy-restor.json
gsutil ls -a gs://week-6/policy









