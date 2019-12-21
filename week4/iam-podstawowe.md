## Podstawowe operacje na uprawnieniach i userach
# Dodanie uzytkownika z uprawnieniami do przegladania projektu
gcloud projects add-iam-policy-binding [projectid] --member user:user@example.com --role roles/viewer

# Odebranie uprawnien
gcloud projects remove-iam-policy-binding [projectid] --member user:user@example.com --role roles/viewer

# export p[olicy do jsona
gcloud projects get-iam-policy [projectid] --format json > ~/policy.json
# export do yamla 
gcloud projects get-iam-policy [projectid] --format yaml > ~/policy.yaml

# tworzenie konta servisowego
cloud iam service-accounts create rk1console --description "test consola" --display-name "rk console test"

# wyswietlenie kont servisowych.
gcloud iam service-accounts list #--format yaml

# dodanie klucza do konta
cloud iam service-accounts keys create ~/key.json --iam-account rk1console@szkolachmury-258710.iam.gserviceaccount.com

# tworzenie custome roli
gcloud iam roles create rkvivwer --project szkolachmury-258710 --file role.yml

# wyswietl
gcloud iam roles list
gcloud iam roles describe rkvivwer --project szkolachmury-258710

