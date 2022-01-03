# Kubernetes in 4 Hours

## Watch the recording
[learning.oreilly.com](https://learning.oreilly.com/live-events/-/0636920056367/0636920063030/)

## Presentation
1. [Slides](https://on24static.akamaized.net/event/33/76/93/8/rt/1/documents/resourceList1637596422229/kubernetes61637596421664.pdf)
	1. [[kubernetes61637596421664.pdf|Local Copy of Slides]]
2. This course is presented by Sander van Vugt
	1. mail@sandervanvugt.com
	2. www.sandervanvugt.com
3. Course resources are available at https://github.com/sandervanvugt/kubernetes
4. Recommendation: Install Kubernetes on top of Ubuntu workstation.
5. Pods are the essential components of Kubernetes.
6. We're not going to use the Kubernetes dashboard in this class.
7. Cloud Native Computing, explaining the notion of it.
	1. There's a cloud.
	2. You have an app running in the cloud.
		1. It should be decoupled from other resources stored in the cloud.
		2. Storage -> Volumes
		3. Configuration
		4. Variables
		5. Each of the above resources are stored and replicated in the nodes in the cloud.
		6. Services that make your app accessible.
		7. Store in cloud vs. localhost.
	3. There are server nodes running in the cloud.
	4. Kubernetes is part of Cloud Native.
	5. Kubernetes has an API.
		1. Defines resources in a cloud environment.
	6. Pod Deployments
	7. ![[Pasted image 20211202102302.png]]
8. Google created Kubernetes to the world.
	1. There is no substitute for container orchestration (in his opinion).
9. Are there other container management solutions?
	1. Not really.
	2. Most are just Kubernetes distributions.
	3. Docker Swarm.
	4. Docker started the container revolution.
	5. Kubernetes made Docker Swarm irrelevant.
	6. Docker eventually supported Kubernetes.
	7. Few companies running Docker Swarm.
	8. Docker Swarm was the most relevant alternative to Kubernetes.
	9. Rancher.
	10. Now it's a Kubernetes distro, part of SUSE.
	11. RedHat OpenShift.
	12. It's their own Kubernetes distro.
	13. Google Anthos is a Kubernetes distro.
10. See "What are Containers" slide.
11. kubeadm utility
12. Run Kubernetes in AWS, Azure, Google Cloud
	1. VMs are providing cloud instances.
13. minikube is a small version of all of Kubernetes.
	1. Not meant to be used in production.
	2. All in One (AiO)
	3. You can run it as a VM or a container on top of Windows, Mac, or Linux.
	4. This is what he's going to demonstrate today.
	5. Run minicube as a container on top of Ubuntu.
	6. He's using macOS and VMware Fusion.
	7. Ubuntu VM in Fusion.
	8. minikube container on top of Ubuntu VM.
	9. App + Cluster
	10. _==minikube is the best platform for learning!==_
	11. ![[Pasted image 20211202103907.png]]
14. CNCF: Cloud Native Computing Foundation
	1. Governing body, part of Linux Foundation
	2. Standardization of K8s.
15. He's showing how to use Google Cloud to deploy Kubernetes clusters.
16. Go to oreilly.com, Sandboxes, there is a Kubernetes sandbox.
	1. Do not use the asio one.
	2. This is the solution if you cannot install anything anywhere to try Kubernetes.
	3. 