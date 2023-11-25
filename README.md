<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>

# Setup Web Server and Database Server with Ansible

<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

**Laravel Starter** is a Laravel 10.x based simple starter project. Most of the commonly needed features of an application like `Authentication`, `Authorisation`, `User` and `Role management`, `Application Backend`, `Backup`, `Log viewer` are available here. It is modular, so you may use this project as a base and build your own modules. A module can be used in any `Laravel Starter` based projects.
[Github](https://github.com/nasirkhan/laravel-starter) or source code for Laravel Starter.

## Build with

* [![Ansible][Ansible-image]][Ansible-url]

<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

* Set up two servers using [Ubuntu Server 22.04.3 LTS](https://ubuntu.com/download/server) for the Web Server and Database Server by deploying Virtual Machines (VMs) on a laptop, utilizing platforms such as [VirtualBox](https://www.virtualbox.org/) or a Cloud Provider
* Virtual Machine (VM) specifications are as follows:
  * [Ubuntu Server 22.04.3 LTS](https://ubuntu.com/download/server)
  * At least 1 vCPU
  * Minimum of 2GB RAM
  * Minimum storage capacity of 10GB

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Setup Virtual Machine (VM)

1. After the Virtual Machine is prepared, proceed to [generate an SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) on your local computer or your computer. Then, copy the public key from the generated SSH key and paste it into the `authorized_keys` file located at the path `~/.ssh/authorized_keys` on each server within the Virtual Machine (VM).

2. Implemented a script to eliminate the need for password entry when executing sudo. Refer to the instructions [here](https://www.cyberciti.biz/faq/linux-unix-running-sudo-command-without-a-password/) for adding the script.

3. Configure a static IP address to ensure its stability. Refer to [the provided instructions](https://www.ardanisite.com/cara-setting-ip-address-ubuntu-server/) for a step-by-step guide on setting up a static IP.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Installation and Usage

1. Clone this repository

   ```sh
    git clone https://github.com/titan2903/setup-server-with-ansible.git
   ```

2. Go to the directory of the cloned repository

3. Copy the file `.env.example` to a file named `.env`

   ```sh
    cp roles/web-server/secrets/.env.example roles/web-server/secrets/.env
   ```

4. To set up the MariaDB Server, you can execute the following command

   ```sh
    ansible-playbook -i inventory.ini setup-mariadb-server.yaml
   ```

5. To set up the Web Server, you can execute the following command

   ```sh
    ansible-playbook -i inventory.ini web-server-playbook.yaml
   ```

6. Go to the server or operating system configured as a web server or has been setup as Web Server, and Change to directory `html`. You can execute the following command

   ```sh
    cd /var/www/laravelsandbox.com/html/
   ```

7. Execute this command within the `html` directory

   ```sh
    sudo composer install
   ```

8. Execute the command to perform the database migration

   ```sh
    sudo php artisan migrate --seed
   ```

9. Run the command  Link storage directory

    ```sh
     sudo php artisan storage:link
    ```

10. If you want to test the application on your local machine with additional demo data you may use the following command and select `Yes`

    ```sh
     sudo php artisan starter:insert-demo-data --fresh
    ```

    ![image](https://ik.imagekit.io/ckb21lc9cd/Screenshot/Screenshot%20from%202023-11-25%2007-49-22_Ak66tOrTs.png?updatedAt=1700873378499)

11. After everything has been installed and set up for the database and web server, proceed to access the website by copying the server hostname or IP address from your web server to the web browser.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Fixing issues or bugs

* If you encounter an error during registration or login, such as `stream: Permission denied The exception occurred while attempting to log: The stream or file "/var/www/laravelsandbox.com/html/storage/logs/laravel-2023-11-24.log" could not be opened in append mode: Failed to open`. Please execute the following command:

    ```sh
     sudo chown -R www-data:www-data /var/www/laravelsandbox.com/html/storage/logs/
    ```

* If you encounter an error during login, such as `file_put_contents(/var/www/laravelsandbox.com/html/storage/framework/cache/data/85/5f/855f92484c8c414d36c1b25cb24876e30229cbbf): Failed to open stream: Permission denied`. Please execute the following command:
  
    ```sh
     sudo chown -R www-data:www-data /var/www/laravelsandbox.com/html/storage/framework/cache/data/85
    ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[Ansible-url]: https://www.ansible.com/
[Ansible-image]: https://img.shields.io/badge/ansible-FFFFF0?style=for-the-badge&logo=ansible&logoColor=black
[product-screenshot]: https://ik.imagekit.io/ckb21lc9cd/Screenshot/Screenshot%20from%202023-11-25%2008-11-17_GzDHKSIaY.png?updatedAt=1700874692938
