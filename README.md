Getting Started with Docker on GCE
==============

1. go to [Google Cloud Console](https://cloud.google.com/console) and create new Cloud Project with billing enabled.

1. download and configure the [Google Cloud SDK](https://developers.google.com/cloud/sdk/) to use your project with the following commands:

```
$ curl https://dl.google.com/dl/cloudsdk/release/install_google_cloud_sdk.bash | bash
$ gcloud auth login
<insert project id configuration blurp here>
```

1. start a new instance, select the a zone close to you and the desired instance size:

```
$ gcutil addinstance docker-playground  --image=backports-debian-7
<insert instance selection blurp here>
```

1. enable IP forwarding:

```
docker-playground:~$ echo net.ipv4.ip_forward=1 | sudo tee /etc/sysctl.d/99-docker.conf 
docker-playground:~$ sudo sysctl --system
```

1. Install docker latest release and configure it to start when the instance boot:

```
docker-playground:~$ curl get.docker.io | bash
docker-playground:~$ sudo update-rc.d docker defaults
```

1. start docker daemon in the background:

```
docker-playground:~$ sudo nohup docker -d &
```

1. start a new container:

```
docker-playground:~$ sudo docker run busybox echo 'docker on compute \o/'
docker on compute \o/
```

If you are looking for a managed solution for running Docker on Compute take a look at [CoreOS](http://coreos.com/docs/google-compute-engine/).
