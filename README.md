# Integreatly catalog source poc

POC to deploy integreatly operator(s) from the operator catalog (OLM)

## Commands

### Integratly catalog source

#### Install

```
ansible-playbook \
-i inventories/local.ini \
playbooks/catalog-install.yml
```

The integratly catalog should now be listed in openshift's operator catalog as a catalog source.

#### Uninstall

```
ansible-playbook \
-i inventories/local.ini \
playbooks/catalog-uninstall.yml
```

### Webapp operator

```
ansible-playbook  \
-i inventories/local.ini \
-e 'webapp_openshift_host=master-host:443' \
-e 'webapp_sso_route=sso-host' \
playbooks/webapp-install.yml
```

This creates two CRs in a given namespace:

* A Subscription CR required by OLM (to deploy the webapp operator)
* A WebApp CR required by its operator (to deploy the webapp itself)

You can now check the cluster console again - it should list a webapp subscription for the used namespace (defaults to `webapp-subs`)

#### Uninstall

```
ansible-playbook \
-i inventories/local.ini \
playbooks/catalog-uninstall.yml
```
