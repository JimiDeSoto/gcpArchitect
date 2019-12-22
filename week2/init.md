gcloud init

gcloud projects list --sort-by=projectId --limit=5
gcloud compute project-info add-metadata \
    --metadata google-compute-default-region=europe-west1,google-compute-default-zone=europe-west1-b

gcloud config list
