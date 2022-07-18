# Apache Airflow Ansible role
This ansible role installs a Apache Airflow 2.x server in a Debian/Ubuntu environment.

The original auther of the implementation is idealista/airflow-role https://github.com/idealista/airflow-role


**The original implementation did not work with latest Ubuntu version (22.04).**

That is because several python dependancies have been left out and Ubuntu 22.04 adapt to Python 3 that comes out-of-box. 


This implementation has been tested with the following specifications:
* Cloud platform: AWS
* OS: Ubuntu 22.04
* Instance Type: t2.micro (This is sufficient only for testing and verification of the installation)
* Airflow version tested: 2.3.2
* Python version: 3.10 (This is the default Python version comes with Ubuntu 22.04)
* Ansible version: 2.10 (This should be 2.0 or higher)

## Installation Steps

1. If you are using a cloud service provider (eg: AWS) create an VM instace according to your requriements
2. Make sure your VM instance could receive HTTP traffic from port 8080 (eg: in AWS, configure Security Groups)
3. Log in to the VM instance and switch to super-user
4. Clone this repository `$ git clone https://github.com/Buddhima/ansible-airflow`
5. Access the directory `$ cd ansible-airflow`
6. Install Ansible `$ apt-get update && apt-get install ansible -y`
7. Execute the Ansible playbook `$ ansible-playbook play.yml`
8. Access the web UI via port 8080

## Customizing the Installation

__`airflow-role/defaults/main/main.yml`__

This contains parameters for installation and configuring other config files.

* `airflow_version` - to change the airflow version
* `airflow_python_version` - Python version use for the installation. Needs to match with OS python version
* `airflow_default_required_libs` - Left with `python3-pip` only compared to original imeplementation
* `airflow_admin_users` - Admin user credentials
* `airflow_user_home` - Home directory of the `airflow`user creating as a result
* `airflow_app_home` - Home directory of Airflow installation
* `airflow_conf_path` - Some Airflow configurations will be placed here

Refer to the original implementation documentation for more information: https://github.com/idealista/airflow-role/blob/master/README.md

__`airflow-role/defaults/main/airflow-cfg.yml`__

This contains configurations that will reflect at `airflow.cfg` file. 
Based on the configurations here, the template file `airflow-role/templates/airflow2.cfg.j2` will be populated.

* `airflow_dags_folder` - Location where the Airflow DAGs are placed

Refer to official documentation for more information: https://airflow.apache.org/docs/apache-airflow/stable/howto/set-config.html

__`airflow-role/defaults/main/webserver-config-py.yml`__

This contains configurations that will reflect at `webserver.config` file. 
Based on the configurations here, the template file `airflow-role/templates/webserver_config.j2` will be populated.

Configurations at here is for the webserver component of Airflow. So you will find configurations for webserver authentication there.

## Limitations

* Only tested with Ubuntu 22.04, in future need to tryout with other linux versions
* Since using the OS Python installation, you need to explicitly specify that in `airflow_python_version`. Otherwise there could be issues with dependancy resolving.
* Currently tested with the __SequentialExecutor__. Need to test with advanced deployments. Reference : https://airflow.apache.org/docs/apache-airflow/stable/executor/index.html#executor-types


