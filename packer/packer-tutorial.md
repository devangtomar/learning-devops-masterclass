## Steps

* Making packer hcl file (eg. docker-ubuntu.pkr.hcl file in our case)..
* Initialize Packer configuration.. run the following :
  * ```packer init .```
* Format and validate your Packer template.. run the following :
  * ```packer fmt .```
* For validating :
  * ```packer validate .```
* Build Packer image :
  * ```packer build docker-ubuntu.pkr.hcl```

Post that you can verify the image using the following command ..

```docker
docker images
```
