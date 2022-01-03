## The surprisingly easy way to set up Docker on macOS or Windows without requiring Docker Desktop

Original Link: [Replacing Docker Desktop with Multipass, to avoid Docker Desktop fees | by David Herron | Nov, 2021 | ITNEXT](https://itnext.io/replacing-docker-desktop-with-multipass-to-avoid-docker-desktop-fees-8cbe57b9037f)

![David Herron](https://miro.medium.com/fit/c/96/96/1*LluZujATfWWdeJNVoaShvA.jpeg)

![](https://miro.medium.com/max/1400/0*7iSohO2EY9hB3MNz.jpg)

**Docker is open source software, and Docker Desktop is a spiffy GUI application to simplify installing Docker on a macOS or Windows machine. It’s worth using, because of how easy it makes to use Docker. However, Docker Inc has switched to a freemium model for the Docker Desktop application, which will lead some to avoid using it and instead seek an alternative to avoid paying the fee. What we’ll discuss is using Multipass, or other virtual machine, to avoid those fees.**

In the old days of Docker, getting it installed on a macOS or Windows machine was a major feat. Since Docker runs natively on Linux, a Linux virtual machine can be installed and install on it Docker Engine for Linux. In the olden days that meant using VirtualBox, which is a heavy-weight virtual machine system. Using Docker Desktop was a huge simplification, since everything for Docker is installed as a normal application. It comes with a nice GUI for managing the local Docker instance with mouse clicks.

Throughout its history, Docker Desktop has been free, but in August 2021 Docker Inc announced the new freemium model. For details, see: [Docker Inc squeezing money from Docker Desktop and other Docker tools](https://techsparx.com/software-development/docker/docker-desktop/not-free.html). The short story is that organizations above a certain size are expected to pay $5 (or so) per month per developer. The fees also include services on Docker Hub.

Some of us might shy away from paying $5 per month (or so) for Docker Desktop. Since Docker provides excellent business value, there’s a good argument to be made for paying the fee. But, there are those of us who wonder what they can use instead of Docker Desktop.

It’s important to note that Docker is not no longer free. Docker is still free, but parts of the Docker ecosystem requires a fee.

Choosing to use Docker Desktop is affected by another fact. Where it used to be difficult to set up Docker on macOS or Windows using a virtual machine, it is now very easy. In other words, there is a worthwhile alternative to Docker Desktop, which is worth exploring.

Inside the Docker Desktop product is a lightweight hypervisor running a virtual Linux instance. Inside that Linux is the Linux version of Docker Engine. The magic of Docker Desktop is that the hypervisor is invisible to us. We’re sitting at the command line typing `docker pull` or `docker build` and not knowing that every command is reaching inside a virtual Linux instance to do everything.

To avoid using Docker Desktop, we need to return to the basics of installing a virtual machine running Linux for installing Docker Engine, then somehow work some magic. Fortunately it’s all simpler now than it used to be. For example, Multipass is lightweight virtual machine platform, with which we can easily set up and run Ubuntu instances. We can then install Docker, and we can even configure multiple Linux VM’s, each with a Docker instance, so we can implement a multi-node cluster to experiment with Docker Swarm or Kubernetes.

Our plan is to this:

-   Use _Multipass_, a lightweight virtual machine system from Canonical, and install Docker Engine inside an Ubuntu instance.
-   For macOS, install the `docker` CLI through either MacPorts, or HomeBrew.
-   For Windows, install the `docker` CLI through ...? It seems that the Chocolatey package manager is the choice.
-   Configure a Docker Context to communicate with the Docker Engine hosted inside the Multipass instance.
-   If we want to implement a Docker Swarm, or a Kubernetes Cluster, that is accomplished by launching multiple Multipass instances.

In other words, this plan relies on an explicit Linux hypervisor hosting a Docker instance. It is simpler this time around because of the Docker Context feature, and how Multipass makes it easy to launch a lightweight Linux virtual machine.

To install Multipass, go to `https://multipass.run` and download the installer for your operating system. Run the installer, and you will have a new command, `multipass,` available. The Multipass website has a few command examples to familiarize yourself with its use.

I’ve written an article about setting up multiple Docker instances using Multipass, see: [Creating a Docker Swarm using Multipass and Ubuntu 20.04 on your laptop](https://techsparx.com/software-development/docker/swarm/multipass.html) … What we’ll do here is a trimmed down version of that process.

Create `setup-instance.sh` containing:

```
sudo apt-get update   
sudo apt-get upgrade -y   
sudo apt-get -y install \\   
       apt-transport-https \\   
       ca-certificates \\   
       curl \\   
       gnupg-agent \\   
       software-properties-common curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \\  
       sudo apt-key add - sudo apt-key fingerprint 0EBFCD88 sudo add-apt-repository \\   
     "deb \[arch=amd64\] https://download.docker.com/linux/ubuntu $(lsb\_release -cs) stable" sudo apt-get update   
sudo apt-get upgrade -y   
sudo apt-get install -y docker-ce docker-ce-cli containerd.io sudo groupadd docker   
sudo usermod -aG docker ubuntu   
sudo systemctl enable docker
```

This script is derived from the official instructions for installing Docker on Ubuntu Linux.

Next, create a shell script named `init-instance.sh` containing:

```
NM=$1 multipass launch --name ${NM} focal   
multipass transfer setup-instance.sh ${NM}:/home/ubuntu/setup-instance.sh   
multipass exec ${NM} -- sh -x /home/ubuntu/setup-instance.sh
```

This script launches a new Ubuntu instance on Multipass. It then executes `setup-instance.sh` inside the new instance.

Run the script as so: `./init-instance.sh docker1`

That sets up the Multipass instance, and initializes Docker. To verify that Docker is running, type this command:

```
multipass exec NAME -- docker run hello-world
```

This gives you a Docker instance. We can run Docker commands inside the Ubuntu instance, but to be the same as Docker Desktop requires running Docker commands at the command-line of our host system. To do that we need to have password-less SSH access to the Multipass instance, and to then setup a Docker Context.

The next step is to enable password-less SSH access to the Multipass instance. We need this in order to setup a Context to control the Docker instance. See: [How to enable passwordless SSH login on Ubuntu 20.04 that’s inside Multipass](https://techsparx.com/linux/multipass/enable-ssh.html) If you have setup remote SSH access the steps are straight-forward. Simply copy your SSH key from `~/.ssh` (e.g. `~/.ssh/id_rsa.pub`) into the `~/.ssh/authorized_keys` files inside the Ubuntu instance.

Once those steps are accomplished you should be able to run `ssh -l ubuntu IP-ADDRESS` to get a shell prompt inside the Ubuntu instance. And, you should be able to run this:

$ ssh -l ubuntu  192.168.64.21 docker run hello-world

To learn the IP address, run `multipass list.` We’re now ready to set up a Docker Context to simplify this, but first we need the open source Docker commands to be installed on your host computer.

How many of us use the Docker Desktop GUI? I rarely use it, and would not miss it. The command-line `docker` command is sufficient for my needs.

Installing Docker Desktop gives you the command-line `docker` commands. You may, therefore, already have them installed. But what we're exploring is installing the `docker` commands without being reliant on Docker Desktop.

The `docker` command is open source, and will always remain open source. This means packages are available from package management systems like MacPorts, and HomeBrew, supplying the `docker` command.

With MacPorts:

port search docker   
...   
docker @20.10.9 (devel)  
    The open-source application container engine docker-compose @1.29.2 (python, devel)  
   Define and run multi-container applications with Docker   
... $ sudo port install docker   
Password:   
\---> Fetching archive for docker   
\---> Attempting to fetch docker-20.10.9\_0.darwin\_19.x86\_64.tbz2 from https://packages.macports.org/docker   
\---> Attempting to fetch docker-20.10.9\_0.darwin\_19.x86\_64.tbz2.rmd160 from https://packages.macports.org/docker Installing docker @20.10.9\_0   
\---> Activating docker @20.10.9\_0   
\---> Cleaning docker   
\---> Updating database of binaries   
\---> Scanning binaries for linking errors   
\---> No broken files found.   
\---> No broken ports found.$ which docker   
/opt/local/bin/docker   
$ docker container ls   
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?  
$ /Applications/Docker.app/Contents/Resources/bin/docker --version  
Docker version 20.10.8, build 3967b7d   
$ /Applications/Docker.app/Contents/Resources/bin/docker container ls   
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

The `docker` command is installed in `/opt/local/bin` just as for other commands managed by MacPorts. For comparison, we located the `docker` command installed as part of Docker Desktop, and learned the current version is 20.10.8, while MacPorts installed version 20.10.9.

When using HomeBrew it’s largely the same:

$ brew install docker   
\==> Pouring docker--20.10.10.catalina.bottle.tar.gz   
Error: The \`brew link\` step did not complete successfully The formula built, but is not symlinked into /usr/local   
Could not symlink bin/docker   
Target /usr/local/bin/docker  
already exists. You may want to remove it:  
  rm '/usr/local/bin/docker'To force the link and overwrite all conflicting files: brew link --overwrite docker   
...   
\==> Summary   
🍺 /usr/local/Cellar/docker/20.10.10: 12 files, 56.8MB   
...  
$ /usr/local/Cellar/docker/20.10.10/bin/docker --version  
Docker version 20.10.10, build b485636f4b   
$ /usr/local/Cellar/docker/20.10.10/bin/docker container ls   
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

The Homebrew install failed because of the existing `/usr/local/bin/docker` installed by Docker Desktop. However, it was still installed in the Cellar at the named location. This is approximately as up-to-date as the MacPorts version. And, notice that this installed version 20.10.10, meaning all three sources are fairly up-to-date.

On Windows, there should be a comparable package available via the WinGet command. WinGet is the Windows equivalent to the macOS package management systems we just examined. But, there doesn’t seem to be a suitable `docker` package available through WinGet. However, both Docker Desktop and Multipass both are managed via WinGet.

There appears to be a `docker` package available in the Chocolatey repository. You can learn more at [https://chocolatey.org/](https://chocolatey.org/)

Another option on Windows is to fire up a WSL2 instance, and install the `docker` command there.

We can now get to the point of this article, which is to connect the `docker` command running on the host system with the Docker instance inside the Ubuntu instance set up earlier.

In 2019, the Docker team added a new feature, _Docker Context_. This is the simplest and most secure way to set up remote control of a Docker instance. The historical method is to publicly expose the Docker TCP point then set up some TLS certificates and other complex steps. Using a Docker Context we can connect with the remote Docker instance using a password-less SSH connection.

By default, the `docker` command tries to connect to a Docker engine running on the local host. But, unless you have an active Docker Desktop running on your host, the following will fail:

$ docker ps   
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

The `docker` command supports a set of environment variables for connecting to a remote Docker instance. The typical way to connect with a remote Docker instance is to expose the Docker TCP port from the remote host. But that seems like a large security problem.

The Docker Context feature is a much better approach. With Docker Context we can configure connections to any of dozens or hundreds of remote Docker instances, and can even connect to Docker deployments on AWS or Azure. You can learn more about using this with AWS in my book [_Deploying Docker Containers to AWS using Terraform: Run Docker on EC2 or ECS the easy way_](https://www.amazon.com/Deploying-Docker-Containers-using-Terraform-ebook/dp/B08WG578L1?pd_rd_w=c2QA4&pf_rd_p=c0296674-5a83-4ad6-b035-0702d2b359df&pf_rd_r=RQGPEJ2N7GT6TGRY6ZBA&pd_rd_r=cd10488f-7d6d-4818-9199-9f3dbca9eb7e&pd_rd_wg=BCIlw&pd_rd_i=B08WG578L1&psc=1&linkCode=ll1&tag=thereikipage&linkId=c30a8498d230dfe9af0c9e8f84146512&language=en_US&ref_=as_li_ss_tl) (sponsored).

To set up a Context for the Ubuntu running inside Multipass, run this:

$ docker context create docker1 \\   
     --docker "host=ssh://ubuntu@192.168.64.21"  
docker1   
Successfully created context "docker1"

We’ve created a context named `docker1` that connects using the SSH URL shown here. This is why we set up password-less SSH access, is so that Docker could use this SSH URL.

$ docker context list   
NAME       DESCRIPTION                               DOCKER  
default \*  Current DOCKER\_HOST based configuration   unix:///var/run/docker.sock  
docker1                                           ssh://ubuntu@192.168.64.21

This command lists the Docker Context’s currently available on your system. The `*` marker indicates which context is currently active.

$ docker context use docker1   
docker1   
Current context is now "docker1"   
$ docker ps   
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES   
$ docker run -it alpine sh   
/ # uname -a  
Linux a139bc7ff4f4 5.4.0-89-generic   
/ #

This demonstrates we have Docker running inside Ubuntu inside Multipass, and that we can control the Docker instance using the `docker` command on our desktop/laptop computer.

We did this while the `docker` command is connected to the `docker1` context. To understand what difference this makes let's change which context we're using.

$ docker context use default   
default   
Current context is now "default"   
$ docker ps   
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

The `docker context use` command is how we switch from one context to another. The `default` context is meant to be on the host machine. In my case, I have Docker Desktop installed, but it is currently not running. The `default` context in this case refers to the Docker Engine that would be running if Docker Desktop were active.

It’s possible to create other Docker context’s. For example, I have a virtual private server (VPS) at a web hosting provider on which I’ve installed Docker. Interacting with that Docker instance looks like this:

$ docker context use host001   
host001   
Current context is now "host001"

My context named `host001` gives remote control of a VPS on which I host a few production websites. The sites are managed using Docker Swarm. Which means I can run this command:

$ docker stack ls   
NAME            SERVICES   ORCHESTRATOR   
backups         1          Swarm   
db              1          Swarm   
proxyman        2          Swarm   
wordpress-ltp   1          Swarm   
...

I can easily use this to run Docker commands on that server, even though it is located hundreds of miles away. Even at this distance, the response time is excellent.

If you prefer to always explicitly select the context, run you commands like this:

$ docker --context CONTEXT-NAME ps

Then, if you want to shut down your Docker service (that’s inside Multipass) simply run this:

$ multipass stop docker1

To start it up again, use `multipass start docker1`.

We’ve learned a simple way to run Docker on a macOS or Windows machine without having to install Docker Desktop. The Docker command being used is as up-to-date as the one supplied by the Docker Desktop product. The command line user experience is identical between using the Multipass-based Docker instance, versus the one managed by Docker Desktop.

As we said earlier, Multipass can be used to implement a multi-node Docker setup, such as to experiment with Docker Swarm or with Kubernetes. To see instructions for setting up a Swarm Cluster, follow the rest of the instructions in [Creating a Docker Swarm using Multipass and Ubuntu 20.04 on your laptop](https://techsparx.com/software-development/docker/swarm/multipass.html)

The instructions used earlier resulted in installing Ubuntu 20.04 inside Multipass. Other operating system images are available and you can list them using this command:

$ multipass find   
Image                  Aliases    Version   Description   
18.04                  bionic     20211021  Ubuntu 18.04 LTS   
20.04                  focal,lts  20211021  Ubuntu 20.04 LTS   
21.04                  hirsute    20211025  Ubuntu 21.04   
21.10                  impish     20211014  Ubuntu 21.10   
anbox-cloud-appliance             latest    Anbox Cloud Appliance   
minikube                          latest    minikube is local Kubernetes

Notice that Minikube is avaliable. That is a tool for simplifying running Kubernetes on your desktop/laptop.

[**_David Herron_**](https://techsparx.com/about.html)_: David Herron is a writer and software engineer focusing on the wise use of technology. He is especially interested in clean energy technologies like solar power, wind power, and electric cars. David worked for nearly 30 years in Silicon Valley on software ranging from electronic mail systems, to video streaming, to the Java programming language, and has published several books on Node.js programming and electric vehicles._