1. Install WSL.
2. Install a Linux distro, e.g. Ubuntu.
	1. Install all applicable updates, e.g. `sudo apt-get upgrade`.
3. [Install the NFS 4.1 client]([Install NFS Server and Client on Ubuntu – VITUX](https://vitux.com/install-nfs-server-and-client-on-ubuntu/#:~:text=Configure%20NFS%20Client%20Machine%201%20Install%20NFS%20Common.,NFS%20host%20server.%20Now%2C%20open%20the...%20See%20More.)) into Ubuntu, i.e., if it's not installed by default.
	1. `sudo apt-get install nfs-common`
	2. `sudo mkdir -p /mnt/sharedfolder_client`
4. Log into your Azure subscription.
	1. You may be able to check one out from the Azure Storage team.
5. Create a storage account.
	1. Performance: Premium.
	2. Premium Account Type: File Shares.
	3. <mark style="background: #FFF3A3A6;">You will likely need to create a virtual network and a private endpoint for accessing this storage account via NFS 4.1.</mark> 
		1. You may instead [restrict access to your public endpoint](https://docs.microsoft.com/en-us/azure/storage/files/storage-files-networking-endpoints?tabs=azure-portal#restrict-public-endpoint-access).
6. Create an NFS 4.1 share.
7. Mount the shared directory on the client.
	1. `sudo mount serverIP:/exportFolder_server /mnt/mountfolder_client`
8. Upload a file to that share via the Ubuntu NFS 4.1 client (or via the Azure Portal).
9. Download that file from that share via the Ubuntu NFS 4.1 client (or via the Azure Portal).