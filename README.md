Prometheus
=========

This role can be used to install prometheus monitoring solution and configure it easily using variables.
Currently only Ubuntu 14.04 and 16.04 are supported more will be added soon.

Requirements
------------

This role does not include any special requirements.

Role Variables
--------------

This role uses three variables all of them has default values, these variables are:

* **PROMETHEUS_VERSION**: The version of prometheus to install default is **1.7.1**
* **PROMETHEUS_BIND_PORT**: The port used to bind prometheus to it default is **9090**
* **PROMETHEUS_JOBS**: This variable is an array, it defines the jobs used by prometheus and their respective instances
  default value is:
    ```
    - prometheus:
      - "localhost:{{ PROMETHEUS_BIND_PORT }}"
    ```
  This means that prometheus will only monitor it self, to add more jobs and instances use this syntax:
    ```
    - prometheus:
      - "prom_server:{{ PROMETHEUS_BIND_PORT }}"
    - node:
      - "server1:9100"
      - "server2:9100"
    - mysql:
      - "dbserver1:9104"
      - "dbserver2:9104"
    ```
    Adding new jobs and instances is super easy just add them to prom_jobs and run the role again

    For more information about prometheus jobs and instances visit [this page](https://prometheus.io/docs/concepts/jobs_instances/)

Dependencies
------------

This role does not depend on any other roles to work.

Example Playbook
----------------


    - hosts: prom_server
      vars:
        - PROM_VERSION: 1.7.1
        - PROMETHEUS_BIND_PORT: 9091
        - prom_jobs:
          prometheus:
            - "prom_server:{{ PROMETHEUS_BIND_PORT }}"
          node:
            - "server1:9100"
            - "server2:9100"
            - "server3:9100"
          mysql:
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
