[![Build Status](https://travis-ci.org/mohsenSy/ansible-role-prometheus.svg?branch=master)](https://travis-ci.org/mohsenSy/ansible-role-prometheus)
Prometheus
=========

This role can be used to install prometheus monitoring solution and configure it easily using variables.
It supports all ubuntu versions, debian 8 and centos 7.

Requirements
------------

This role does not include any special requirements.

Role Variables
--------------

This role uses three variables all of them has default values, these variables are:

* **prometheus_version**: The version of prometheus to install default is **2.4.2**
* **prometheus_scrape_interval**: The interval at which targets are scarped default is 15s
* **prometheus_evaluation_interval**: The interval at which rules are evaluated default is 15s
* **prometheus_jobs**: This variable is an array, it defines the jobs used by prometheus and their respective instances
  default value is:
    ```
    - name: prometheus
      targets:
        - localhost:9090
    ```
  This means that prometheus will only monitor it self, to add more jobs and instances use this syntax:
    ```
    - name: node
      targets:
        - "server1:9100"
        - "server2:9100"
    - name: mysql
      targets:
        - "dbserver1:9104"
        - "dbserver2:9104"
    ```
    Adding new jobs and instances is super easy just add them to prometheus_jobs and run the role again

    For more information about prometheus jobs and instances visit [this page](https://prometheus.io/docs/concepts/jobs_instances/)

Dependencies
------------

This role does not depend on any other roles to work.

Example Playbook
----------------


    - hosts: prom_server
      vars:
        - prometheus_version: 2.4.2
        - prometheus_jobs:
          - name: prometheus
            targets:
              - "prom_server:9090"
          - name: node
            targets:
              - "server1:9100"
              - "server2:9100"
              - "server3:9100"
          - name: mysql
            targets:
              - "db1:9104"
              - "db2:9104"
              - "db3:9104"
              - "db4:9104"
      roles:
         - mohsenSy.prometheus

License
-------

BSD

Author Information
------------------

If you have any question please contact me on

[twitter](https://twitter.com/mouhsen_ibrahim)

[linkedin](https://linkedin.com/in/mohsen-ibrahim-670b13112/)

email mohsen47@hotmail.co.uk
