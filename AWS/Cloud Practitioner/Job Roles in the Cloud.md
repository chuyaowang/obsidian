# Job Roles in the Cloud

> [Source](https://explore.skillbuilder.aws/learn/course/156/play/80055/job-roles-in-the-cloud;lp=82)
> 
## On-premise IT Job Roles

> [!summary] IT Solutions Architect
> 
> They create high level solutions for business applications, systems, portfolios, infrastructures, or an entire enterprise.
> 
> They develop IT services and solutions for companies and organizations and often design and manage communications, security, networking, and storage.
^itarchitect

> [!summary] System Administrator
> 
> They keep servers operational, ensure servers meet uptime goals, patch or upgrade operating systems, hardware, and hypervisors, and make system backups.
^sysadmin

> [!summary] Network Administrator
> 
> They administer network access points and manage personnel access, configurations, and VPNs. 
^netadmin

> [!summary] Desktop Administrator
> 
> They administers installing and maintaining applications on desktop and laptop computers. They work with the [Network Administrator](#^netadmin) for network and security configurations.
^deskadmin

> [!summary] Applications Administrator
> 
> They handle web and customer applications. They work with the [System Administrator](#^sysadmin) to host and maintain applications on servers. They also partner with the [Network Administrator](#^netadmin) for application access control.
^appadmin

> [!summary] Database Administrator
> 
> They manage databases by working with the [System Administrator](#^sysadmin) on the servers that the database is on. They work with the [Network Administrator](#^netadmin) for the database access control.
^dbadmin

## Shared Responsibility Model

AWS operates, manages, and controls the components from the host operating system and virtualization layer down to the physical security of the facilities in which the service operates. The customer assumes responsibility and management of the guest operating system, including updates and security patches. The customer also assumes responsibility for other associated application software and the configuration of the AWS provided security group firewall.
## On-cloud IT Job Roles


> [!summary] Cloud Architect
> 
> The Cloud Architect is responsible for delivering an overall cloud strategy and is in charge of the entire cloud environment. The Cloud Architect builds a business’s cloud architecture blueprint to deliver highly available, cost-efficient, and scalable cloud environments. This role supervises deployment in the cloud environment and application architecture for all aspects of the cloud. It is critical that a Cloud Architect is knowledgeable enough to be your business’s AWS Cloud subject matter expert and the go-to for anything related to the cloud.
^cloudarchitect

> [!summary] System Administrator
> 
> The System Administrator is responsible for overall performance of cloud systems. They are the glue that keeps systems working together by managing configurations, completing detailed tasks, and assisting Database Administrators with setting up database servers in the cloud. 
> 
> A System Administrator in the cloud maintains data integrity by deploying, configuring, and monitoring hybrid and cloud solutions instead of infrastructure performance and maintenance. 
> 
> It’s essential that the System Administrator is adaptable and proficient with configuration management, requirements gathering, deployment planning, and completing detailed hands-on tasks.
^cloudsysadmin

> [!summary] Security Administrator
> 
> A Security Administrator must be someone that is trusted and exceptionally knowledgeable because they are responsible for the overall integrity, confidentiality, and protection of data and resources in the cloud.
> 
> This role is a combination of reactive (investigates when security incidents or concerns are reported) and proactive (puts standards and development processes in place to reduce the number of security incidents). While the Security Administrator does not need to know all of the details of cloud operations, they do define security requirements based on their company’s security and regulatory requirements.  
> 
> To ensure security *in* the cloud, the Security Administrator must have a deep understanding of security rules and requirements applicable to their unique business. They must be highly resourceful, because it isn’t possible to memorize every rule or regulation. This role communicates these requirements down to engineers and up to decision makers to understand and address security risks.
^cloudsecurityadmin

> [!summary] DevOps Administrator
> 
> The DevOps Administrator optimizes the use of the AWS Cloud. They help businesses operate at a larger, faster scale by managing developers and orchestrating the numerous tools and stages in the pipeline. 
> 
> This role creates and maintains processes so that teams and developers can follow the model of small, rapid releases. To do this, this role manages the release cycle to ensure that there is enough pipeline to evaluate changes that need to be made, tested, and pushed to production. Additionally, the DevOps Administrator conducts tests and backs out changes if there are issues. They have the ability to quickly roll back changes if something doesn’t work.
> 
> DevOps Administrators implement continuous build, integration, deployment, and infrastructure as code. They review and recommend operational improvements. DevOps Administrators also perform application testing and recovery.
> 
> Because the DevOps Administrator is responsible for orchestrating the pipeline, this role must be proficient with programming scripting languages, operations, QA, and testing.
^clouddevopsadmin

## Mapping On-premise Roles to Cloud Roles

- [IT Solutions architect](#^itarchitect) maps to [cloud Architect](#^cloudarchitect);
- [System administrators](#^sysadmin), [network and security administrators](#^netadmin), and [desktop administrators](#^deskadmin) map to [AWS system operations administrators](#^cloudsysadmin) who oversees the server, network, and desktop teams or [AWS security administrators](#^cloudsecurityadmin);
- [Application administrators](#^appadmin) and [database administrators](#^dbadmin) can move to [devOps administrators](#^clouddevopsadmin), who typically oversee developer and database teams.