# What is QloApps?
QloApps is a free, fully customizable open-source hotel management and reservation system. It enables users to launch a user-friendly hotel booking website and manage both online and offline bookings. Suitable for small independent hotels as well as large hotel chains, QloApps serves as a comprehensive solution for all hotel business needs.

# How to Deploy QloApps with Docker
## Prerequisites
Before proceeding, ensure you have the latest version of Docker installed along with its dependencies, as per your operating system. For detailed instructions, refer to the Docker installation guide.

## The QloApps Docker image architecture includes:

Ubuntu 20.04
MySQL Server 8.0
PHP 7.4
Additionally, verify that your user has the necessary privileges to run Docker commands.

## Important Note
The MySQL root password, database name, and SSH user password are not preset. Users must provide these details as arguments when running the Docker image.

The default SSH user created during the image build is 'qloapps.' You can modify the user argument in the Dockerfile and rebuild the image to suit your requirements.

# Procedure
# Step 1: Pull the Docker Image
Begin by pulling the Docker image from Docker Hub with the following command:
```
docker pull webkul/qloapps_docker:latest
```

# Step 2: Run the Container
After pulling the image, run the container, specifying the required ports and arguments:

```
docker run -tidp 80:80 -p 3306:3306 -p 2222:22 --name qloappsv161 -e USER_PASSWORD=qloappsuserpassword -e MYSQL_ROOT_PASSWORD=myrootpassword -e MYSQL_DATABASE=qlo161 webkul/qloapps_docker:latest
```
**Note:** Ensure that no other services are using ports 80, 2222, and 3306. If these ports are occupied, specify alternative ports as needed.

In this command:

Host port 80 is mapped to Docker port 80 (Apache).
Host port 3306 is mapped to Docker port 3306 (MySQL).
SSH port 2222 is mapped to Docker port 22 (SSH server).
Please make sure that no other services are running on these host ports.

## Important: Replace MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, and USER_PASSWORD with your own values in the command.

# Step 3: Verify the Running Container
To check if your container is running, use the command:

```
docker ps
```

You should see the container named 'qloappsv161'.

Next, open your browser and navigate to your server's IP address or domain name to initiate the QloApps installation process.

After completing the installation, remove the '/install' directory from the server root directory inside the container by executing:

```
docker exec -i qloappsv161 rm -rf /home/qloapps/www/QloApps/install
```

# Step 4: Rename the Admin Directory
Upon accessing the back office URL, you will be prompted to rename your admin directory. You can do this by entering the running container and renaming the directory as needed, for example, to "adminhtml":

```
docker exec -i qloappsv161 mv /home/qloapps/www/QloApps/admin /home/qloapps/www/QloApps/adminhtml
```

# Step 5: Access QloApps via SSH
To access your QloApps files and directories, SSH into your Docker container with the following command:

```
ssh qloapps@your_ip -p 2222
```

# --For Older Versions (>=1.6.0)--

To deploy older versions, replace qloappsv161 with the desired version, such as qloappsv160 or qloappsv159. The document root path will be /home/qloapps/www/hotelcommerce/.

## Example
To pull a specific version, select the version from Docker Hub tags and use:

```
docker pull webkul/qloapps_docker:[Version]
```

After pulling the image, run the container by specifying the version in the command:

```
docker run -tidp 80:80 -p 3306:3306 -p 2222:22 --name qloappsv161 -e USER_PASSWORD=qloappsuserpassword -e MYSQL_ROOT_PASSWORD=myrootpassword -e MYSQL_DATABASE=qlo161 webkul/qloapps_docker:[Version]
```

Then, follow the installation process as outlined previously.

After installation, remove the '/install' directory:

```
docker exec -i [Your_container_name] rm -rf /home/qloapps/www/hotelcommerce/install
```

Rename the admin directory as needed:

```
docker exec -i [Your_container_name] mv /home/qloapps/www/QloApps/admin /home/qloapps/www/QloApps/adminhtml
```
And rest remain the same as previous.
 
# Getting Support
If you encounter any issues or have questions, please contact us at support@qloapps.com or raise a ticket at QloApps Support.

Thank you.
