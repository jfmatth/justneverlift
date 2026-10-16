```
$ProjectId = "glassy-rush-476214-j9"
$ProjectNumber = gcloud projects describe $ProjectId --format="value(projectNumber)"
$CloudBuildSA = "$ProjectNumber@cloudbuild.gserviceaccount.com"
$RunSA = "$ProjectNumber-compute@developer.gserviceaccount.com"

gcloud artifacts repositories create app-ar `
    --repository-format=docker `
    --location=us-central1 `
    --description="New clean AR repo for app-service"

```

**Choose NONE** when prompted

```
# Cloud Build → Artifact Registry (push)
gcloud artifacts repositories add-iam-policy-binding app-ar `
    --location=us-central1 `
    --member="serviceAccount:$CloudBuildSA" `
    --role="roles/artifactregistry.writer"

# Cloud Build → Cloud Run (deploy)
gcloud projects add-iam-policy-binding $ProjectId `
    --member="serviceAccount:$CloudBuildSA" `
    --role="roles/run.admin"

gcloud projects add-iam-policy-binding $ProjectId `
    --member="serviceAccount:$CloudBuildSA" `
    --role="roles/iam.serviceAccountUser"



gcloud artifacts repositories add-iam-policy-binding app-ar `
    --location=us-central1 `
    --member="serviceAccount:$RunSA" `
    --role="roles/artifactregistry.reader"



```