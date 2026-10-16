# building in GCP

```
. .\00-vars.ps1
```

```
gcloud projects create $PROJECT_ID `
    --name="$PROJECT_NAME"
gcloud config set project $PROJECT_ID
```

```
 gcloud billing projects link $PROJECT_ID `
   --billing-account=017E9A-A8E4DF-74D0A7
```

```
gcloud services enable `
    cloudbuild.googleapis.com `
    clouddeploy.googleapis.com `
    artifactregistry.googleapis.com `
    run.googleapis.com `
    iam.googleapis.com `
    secretmanager.googleapis.com `
    containeranalysis.googleapis.com `
    logging.googleapis.com
```

```
gcloud artifacts repositories create $REPO_NAME `
    --repository-format=docker `
    --location=$REGION `
    --description="JustNeverLift Containers"
gcloud artifacts repositories list
```

```
gcloud iam service-accounts create cloudbuild-deployer `
    --display-name "Cloud Build Deployment Service Account"
```


