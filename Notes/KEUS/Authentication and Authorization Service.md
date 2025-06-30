## Services
### Cloud Authentication Service
1. Lives on cloud, verifies the identity of a person

### Cloud Authorization Service
1. Lives on cloud, checks what roles a person has, and whether any of these role
has permission for performing a required action on a resource

### Local Authorization Service
1. Responsibilities same as cloud authorization service, but only for those responsibilities that are 
required locally inside a home network

#### More requirements 
1. Roles' permissions should be configurable through API (e.g., REST API or User Interface)
## Code guideline 
1. Make use of MoleculerJS, and all these services and functions, should be moleculerjs services and 
moleculerjs actions

1. Permissions can be of the form of 
