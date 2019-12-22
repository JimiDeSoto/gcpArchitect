# prep
## user musi miec uprawnienia Organization Policy Administartor
proj2="tokyo-dream-262809"

# Polityka dotyczca image, wymusic zaufane
gcloud projects list

cloud beta resource-manager org-policies describe compute.trustedImageProjects --effective  --project $proj2

# zrzut poltyki do pliku
gcloud beta resource-manager org-policies describe compute.trustedImageProjects --effective  --project $proj2 > tokyo-policy.yaml

# lista dostepnych obrazow, wybiermay debian-cloud
gcloud compute images list

# edycja yaml

deniedValues:
    - projects/debian-cloud


# aplikacja policy
gcloud beta resource-manager org-policies set-policy --project=$proj2 tokyo-policy.yaml
