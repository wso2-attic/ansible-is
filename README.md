# WSO2 Identity Server Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 Identity Server.

## Supported Operating Systems

- Ubuntu 16.04 or higher

## Supported Ansible Versions

- Ansible 2.0.0.2

## Directory Structure
```
.
├── dev
│   ├── group_vars
│   │   └── is.yml
│   ├── host_vars
│   │   ├── is_1.yml
│   │   └── is_2.yml
│   └── inventory
├── docs
│   ├── images
│   │   ├── Deployment-pattern-1-diagram.png
│   │   └── Deployment-pattern-2-diagram.png
│   ├── Pattern1.md
│   └── Pattern2.md
├── files
│   ├── mysql-connector-java-5.1.45-bin.jar
│   └── wso2is-linux-installer-x64-5.6.0.deb
├── issue_template.md
├── LICENSE
├── pull_request_template.md
├── README.md
├── roles
│   └── is
│       ├── tasks
│       │   ├── custom.yml
│       │   └── main.yml
│       └── templates
│           ├── carbon-home
│           │   ├── bin
│           │   │   └── wso2server.sh.j2
│           │   └── repository
│           │       ├── conf
│           │       │   ├── axis2
│           │       │   │   └── axis2.xml.j2
│           │       │   ├── carbon.xml.j2
│           │       │   ├── datasources
│           │       │   │   └── master-datasources.xml.j2
│           │       │   ├── identity
│           │       │   │   └── identity.xml.j2
│           │       │   ├── registry.xml.j2
│           │       │   ├── tomcat
│           │       │   │   └── catalina-server.xml.j2
│           │       │   └── user-mgt.xml.j2
│           │       └── deployment
│           │           └── server
│           │               └── eventpublishers
│           │                   ├── IsAnalytics-Publisher-wso2event-AuthenticationData.xml.j2
│           │                   ├── IsAnalytics-Publisher-wso2event-RoleData.xml.j2
│           │                   ├── IsAnalytics-Publisher-wso2event-SessionData.xml.j2
│           │                   └── IsAnalytics-Publisher-wso2event-UserData.xml.j2
│           └── wso2is.service.j2
└── site.yml
```

## Packs to be Copied

Copy the following files to `files` directory.

1. [WSO2 Identity Server 5.6.0 package](https://wso2.com/identity-and-access-management/install)
2. [mysql-connector-java-5.1.45-bin.jar](https://dev.mysql.com/downloads/connector/j/5.1.html)

## Running WSO2 Identity Server Ansible scripts

### 1. Run the existing scripts without customization
The existing Ansible scripts contain the configurations to set-up a single node WSO2 Identity Server pattern. In order to deploy the pattern, you need to replace the `[ip_address]` given in the `inventory` file under `dev` folder by the IP of the location where you need to host the Identity Server. An example is given below.
```
[is]
wso2is ansible_host=172.28.128.4
```

Run the following command to run the scripts.

`ansible-playbook -i dev site.yml`

If you need to alter the configurations given, please change the parameterized values in the yaml files under `group_vars` and `host_vars`.

### 2. Customize the WSO2 Ansible scripts

The templates that are used by the Ansible scripts are in j2 format in-order to enable parameterization.

The `axis2.xml.j2` file is added under `roles/wso2is/templates/carbon-home/repositoy/conf/axis2/`, in order to enable customizations. You can add any other customizations to `custom.yml` under tasks of each role as well.

#### Step 1
Uncomment the following line in `main.yml` under the role you want to customize.
```
- import_tasks: custom.yml
```

#### Step 2
Add the configurations to the `custom.yml`. A sample is given below.

```
- name: "Copy custom file"
  template:
    src: path/to/example/file/example.xml.j2
    dest: destination/example.xml.j2
  when: "(inventory_hostname in groups['is'])"
```

Follow the steps mentioned under `docs` directory to customize/create new Ansible scripts and deploy the recommended patterns.
