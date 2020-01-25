### preq
gcloud components install app-engine-python
wget https://github.com/GoogleCloudPlatform/python-docs-samples/archive/master.zip

### teraform mySQL
terraform apply -auto-approve

### prep python app
set FLASK_APP=mysql-test.py
python -m flask run

### import danych do bazy
gsutil mb gs://sql-dump-rk01/
gcloud sql instances list
gcloud sql instances describe rk-my-sql

gsutil acl ch -u p777753131068-obcg5d@gcp-sa-cloud-sql.iam.gserviceaccount.com:W gs://sql-dump-rk01/

gsutil cp load_employees.dump gs://sql-dump-rk01/load_employees.dump

gsutil acl ch -u p777753131068-obcg5d@gcp-sa-cloud-sql.iam.gserviceaccount.com:R gs://sql-dump-rk01/load_employees.dump

gcloud sql import sql rk-my-sql gs://sql-dump-rk01/load_employees.dump \
    --database=rkdb


### II
gcloud sql connect rk-my-sql --user=root


