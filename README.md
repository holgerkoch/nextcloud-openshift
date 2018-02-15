# Nextcloud for OpenShift 3

This repository contains an OpenShift 3 template to easily deploy Nextcloud on OpenShift.
With this template it's possible that your customer can create one or more nextcloud instances in her namespace.

## Installation

* oc login to your cluster with clusteradmin permissions
* oc create -f nextcloud.yaml -n openshift

after this, you should see a nextcloud template in you catalog in every namespace

### Files

To backup files, a simple solution would be to run f.e. [restic](http://restic.readthedocs.io/) in a Pod
as a `CronJob` and mount the PVCs as volumes. Then use an S3 endpoint for restic
to backup data to.

## Notes

* Nextcloud Cronjob is called from a `CronJob` object every 15 minutes
* The Dockerfile just add the `nginx.conf` to the Alpine Nginx container

To use the `occ` CLI, you can use `oc exec`:

```
oc get pods
oc exec NEXTCLOUDPOD -c nextcloud -ti php occ
```

## Ideas

* Use sclorg Nginx instead of Alpine Nginx for better OpenShift compatibility
* Autoconfigure Nextcloud using `autoconfig.php`
* Provide restic Backup example

## Contributions

Very welcome!

1. Fork it (https://github.com/tobru/nextcloud-openshift/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
