# seal-and-unseal
Two basic scripts for Kubernetes for when you want to seal and unseal a file secret with sealed-secrets in a gitops workflow.

Pretty useful if the sealed-secret you're interested in isn't on the cluster, and it makes for a clean offline-ish workflow for sealing/unsealing secrets for development.

A much nicer way to use sealed-secrets until the kubeseal CLI experience is improved.

## Usage
1. Copy the `seal.sh` and `unseal.sh` scripts to your gitops workspace
2. Edit the scripts to point to the correct file name for your sensitive file, 
the correct sealed-secret controller name and namespace, 
and the destination secret name and namespace.

Then just run `./seal.sh` to create a sealed-secret manifest and `./unseal.sh` to recreate the sensitive file! 

## Important notes

### .gitignore
Make sure your file is in the .gitignore so that you only commit the new secret manifest, not the original sensitive file!

### File clobbering
Note that if your kubeconfig context is not connected to the correct cluster when you unseal the secret, 
it will clobber your local copy of the sensitive file, so commit your sealed-secrets often,
or use an IDE that can track changes to files not in git, like Jetbrains' Pycharm.
