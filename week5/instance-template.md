CM->IT

#docizanie instancji
dd if=/dev/zero of=/dev/null


zmina ilosci maszyn w grupie
gcloud compute instance-groups managed set-autoscaling <GROUP_NAME> --min-num-replicas 5 --max-num-replicas 10 --zone <ZONE>