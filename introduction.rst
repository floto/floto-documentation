Introduction
============

floto allows you to describe your infrastructure using a domain-specific language (DSL) embedded in JavaScript.
Using such a description systems can be deployed and updated automatically.
The same descriptions can be used during development (on a local virtual machine) and in production (on bare metal or virtual machines).
Using docker containerization, these deployments are fast as well as isolated. The description language and a templating mechanism allows services to publish their service endpoints, so that other services can access them.