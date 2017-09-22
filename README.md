# Kubernetes RBAC Scripts

This ansible project is for creating rbac configs and kubeconfigs for kubernetes

### Prerequisites

**ansible 2.3 or newer**

**Jinja2 2.9 or newer**

**openssl in your path - plan is to replace this with the new openssl modules that are coming to ansible 2.4 and above**

**The CA keypair from your kubernetes cluster - You can test by creating your own key and cert in the root level of the project :**

```
openssl genrsa -out ca-key.pem 2048
openssl req -x509 -new -nodes -key ca-key.pem -days 10000 -out ca.pem -subj "/CN=kube-ca"
```  

## Getting Started

first edit the group_vars/local/vars.yml to suit your needs and then run the main play

```
ansible-playbook site.yml -e env=ENV -t TAG
```
**find your desired role tag under the roles section of site.yml e.g (kubectl)**
 ``` roles:
    - { role: kubectl, tags: ['kubectl'] } 
    - { role: kubeconfig, tags: ['kubeconfig'] } 
    - { role: rbac_certs, tags: ['certs'] } 
    - { role: cluster_role, tags: ['cluster_role'] } 
    - { role: namespace_role, tags: ['namespace_role'] } 
```
**and then run ansible-playbook with that single tag**

```ansible-playbook site.yml -e env=local -t certs ```
