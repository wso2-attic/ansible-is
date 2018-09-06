# Pattern 1 - HA clustered deployment of WSO2 Identity Server

## Deployment diagram
![HA clustered deployment of WSO2 Identity Server](images/Deployment-pattern-1-diagram.png)

## Changing hostname and ports
1. Uncomment the parameters in the `is_2.yml` and give the values for both `is_1.yml` and `is_2.yml`, following the [documentation](https://docs.wso2.com/display/IS560/Setting+Up+Deployment+Pattern+1) to deploy pattern 1.

2. Uncomment the following lines in the `site.yml` file.
```
hosts:
  - is_1
  - is_2
```

3. Go to `host_vars` and uncomment the following lines in the yaml files.
```
proxy_port_https: proxyPort="443"
proxy_port_http: proxyPort="80"
```
4. In the same files, change the `hostname` and the `mgt_hostname` to the hostname of your servers.
```
carbon:
      hostname: wso2.is.com
      mgt_hostname: wso2.is.com
```
NOTE: This hostname is used by the cluster. It must be defined in the /etc/hosts file.


## Adding a new file to the templates to parameterize

1. Add the parameterized file to the `templates/carbon-home` directory. This maintains the exact folder structure of the WSO2 Identity Server pack.

2. Add the action you need to take on the above file to the `customs.yml` file as mentioned in [here](README.md#Step_2).

3. Based on the parameters, add the values to the yml files under `group_vars` or `host_vars`. An example is given in the file itself.
