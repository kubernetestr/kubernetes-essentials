```bash
#cluster-info
gcloud container clusters describe meetup --project=inspired-bus-194216 --zone=us-central1-c --format="json"  | grep service
gcloud container clusters describe meetup --project=inspired-bus-194216 --zone=us-central1-c --format="json"  | grep Ip
```
