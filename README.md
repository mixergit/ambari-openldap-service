#### An Ambari Stack for OpenLDAP
Ambari stack for easily installing and managing OpenLDAP on HDP cluster

- Download HDP 2.2 sandbox VM image (Sandbox_HDP_2.2_VMware.ova) from [Hortonworks website](http://hortonworks.com/products/hortonworks-sandbox/)
- Import Sandbox_HDP_2.2_VMware.ova into VMWare and set the VM memory size to 8GB
- Now start the VM
- After it boots up, find the IP address of the VM and add an entry into your machines hosts file e.g.
```
192.168.191.241 sandbox.hortonworks.com sandbox    
```
- Connect to the VM via SSH (password hadoop) and start Ambari server
```
ssh root@sandbox.hortonworks.com
/root/start_ambari.sh
```

- To deploy the OpenLDAP stack, run below
```
cd /var/lib/ambari-server/resources/stacks/HDP/2.2/services
git clone https://github.com/abajwa-hw/openldap-stack.git   
sudo service ambari restart
```
- Then you can click on 'Add Service' from the 'Actions' dropdown menu in the bottom left of the Ambari dashboard:

On bottom left -> Actions -> Add service -> check openLDAP server -> Next -> Next -> Enter password -> Next -> Deploy
![Image](../master/screenshots/screenshot-vnc-config.png?raw=true)

- On successful deployment you will see the openLDAP service as part of Ambari stack and will be able to start/stop the service from here:
![Image](../master/screenshots/screenshot-vnc-stack.png?raw=true)

- When you've completed the install process, openLDAP server will appear in Ambari 
![Image](../master/screenshots/screenshot-freeipa-stack.png?raw=true)

- You can see the parameters you configured under 'Configs' tab
![Image](../master/screenshots/screenshot-freeipa-stack-config.png?raw=true)

- To remove the openLDAP service: 
  - Stop the service via Ambari
  - Delete the service
  
    ```
    curl -u admin:admin -i -H 'X-Requested-By: ambari' -X DELETE http://sandbox.hortonworks.com:8080/api/v1/clusters/Sandbox/services/OPENLDAP
    ```
  - Remove artifacts 
  
    ```
    /var/lib/ambari-server/resources/stacks/HDP/2.2/services/openldap-stack/remove.sh
    ```


#### Browse users

- You can browse the groups/users in OpenLDAP using any LDAP browser like JXplorer 
![Image](../master/screenshots/screenshot-browse-LDAP.png?raw=true)

- The OpenLDAP webUI login page should come up at the below link: 
http://sandbox.hortonworks.com/ldapadmin

![Image](../master/screenshots/screenshot-error.png?raw=true)

- You can also open it from within Ambari via [iFrame view](https://github.com/abajwa-hw/iframe-view)
![Image](https://github.com/abajwa-hw/iframe-view/blob/master/screenshots/phpldap.png)

