# Creating regional MIG
1. All managed instance groups require an instance template. Create template using command:
gcloud compute instance-templates create example-template
2. Next, use the instance-groups managed create subcommand with the --region flag. For example, this command creates a regional managed instance group in three zones within the us-east1 region:
gcloud compute instance-groups managed create example-rmig --template example-template --base-instance-name example-instances --size 3 --region us-east1
3. If you want to select the specific zones the group should use, provide the --zones flag:
gcloud compute instance-groups managed create example-rmig --template example-template --base-instance-name example-instances --size 3 --zones us-east1-b,us-east1-c
4. If you want to disable proactive instance redistribution, set the --instance-redistribution-type flag to NONE. Because this feature is in Beta, you must use the gcloud beta tool. You cannot disable proactive instance redistribution if autoscaling is enabled:
gcloud beta compute instance-groups managed create example-rmig --template example-template --base-instance-name example-instances --size 3 --instance-redistribution-type NONE