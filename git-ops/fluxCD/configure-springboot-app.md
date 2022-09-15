## Create a spring boot app source from git repo 

flux create source git springboot-app \
    --url https://github.com/lerndevops/sprintboot-app \
    --branch main \
    --interval 30s \
    --export \
    | tee springboot-app-repo-sync.yaml

## Create a flux kustomization with a kustomization.yaml path from a GitRepository source

## Staging 

flux create kustomization springboot-app-kustomize-stage \
    --source springboot-app \
    --path "./kustomize/overlays/staging/" \
    --prune true \
    --interval 10m \
    --export \
    | tee springboot-app-kustomization.yaml


## Production 

flux create kustomization springboot-app-kustomize-prod \
    --source springboot-app \
    --path "./kustomize/overlays/production/" \
    --prune true \
    --interval 10m \
    --export \
    | tee springboot-app-kustomization-prod.yaml