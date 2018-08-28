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
│   │   └── wso2is.yml
│   └── inventory
├── FAQ.md
├── files
│   ├── mysql-connector-java-5.1.45-bin.jar
│   └── wso2is-linux-installer-x64-5.6.0.deb
├── issue_template.md
├── LICENSE
├── pull_request_template.md
├── README.md
├── roles
│   └── wso2is
│       ├── tasks
│       │   ├── customize.yml
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

Copy the following files to `ansible-is/files` directory.

1. WSO2 Identity Server 5.6.0 package (deb or rpm)
2. mysql-connector-java-5.1.45-bin.jar

## Running WSO2 Identity Server Ansible scripts

### 1. Run the existing scripts without customization
The existing Ansible scripts contain the configurations to set-up a single node WSO2 Identity Server pattern. In order to deploy the pattern, you need to replace the IP address(172.28.128.4) given in the inventory file under dev folder by the IP of the location where you need to host the Identity Server.

Run the following command to run the scripts.

`ansible-playbook -i dev site.yml`

### 2. Customize the WSO2 Ansible scripts

The axis2.xml.j2 file is added under roles/wso2is/templates/carbon-home/repositoy/conf/axis2/, in order to enable customizations. You can add any other customizations to customize.yml under tasks of each role as well.
Follow the steps mentioned in the [ansible-is wiki](https://github.com/wso2/ansible-is/wiki) to customize/create new Ansible scripts.
