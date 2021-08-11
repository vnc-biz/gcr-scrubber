![alt text](https://github.com/vnc-biz/gcr-scrubber/blob/main/GCRscrubber.png?raw=true)

# gcr-scrubber
A Gitlab CI Pipeline which deletes any images older than defined number of tags from GCR(Google Container Registry)

### The Problem?

Unfortunately unlike ECR and ACR (Amazon's and Azure's respective PaaS container registry offerings) GCP still don't offer a way to do image retention/deletion.

At VNC we've produced this little gitlab pipeline to ensure our google container registries only keep the last 10 images so that we're not needlessly paying for images we're never going to need to deploy again

## Usage

There are a few variables and modifications that you'll need to fit your purposes, this pipeline assumes you have 2 projects you're looking to cleanup images from and that you tag your images accordingly (development/production) ((you will need to change the grep to match your images if different))

Variables

|VARIABLE                | DESCRIPTION|
|------------------------|------------------------------------------------------------|
| GOOGLE_PROJECT_ID      | Name of your google project|
| GOOGLE_PROJECT_ID_PROD | Name of your other google project|
| GOOGLE_COMPUTE_ZONE    | Name of the region your GCR is deployed into|
| SA_ACCOUNT_DEV         | Project A's Service account|
| SA_ACCOUNT_PROD        | Project B's Service account(can be consolidated if required) |
| GCR_DEV                | Project A's GCR                                 |
| GCR_PROD               | Project B's GCR                                  |
| IMAGE_RETENTION        | Number of images you'd like to retain, this is queried by timestamp so it will always keep the newest X amount of images|
