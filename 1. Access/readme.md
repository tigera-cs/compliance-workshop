# 1. Access

## Set Up Users

Calico Cloud supports Google Social Authentication as well as local users and connecting to your own IdP (based on OIDC).

## Local User Setup

In Kubernetes, cluster roles specify cluster permissions and are bound to users using cluster role bindings. In Calico Cloud we provide the following predefined roles.

**Admin**

- Full access to Calico Cloud Manager
    - Create and modify Calico Cloud resources
    - Superuser access for Kibana, including Elasticsearch user

**Viewer**

- Basic user with access to Calico Cloud Manager and Kibana:
    - List/view Calico Cloud policy, Kubernetes policy, and tier resources
    - List/view logs in Kibana

## OIDC User Setup

Calico Cloud supports the following IdPs:
- OIDC-based Auth providers (for example Google, Azure AD)

To add an IdP, open a [Support ticket.](https://support.tigera.io/)

## Reference Documentation

For more details on Users, please see the [Calico Cloud Documentation.](https://docs.calicocloud.io/operations/user-management)