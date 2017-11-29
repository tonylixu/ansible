## Choosing The Right Configuration Managment/Orchestration Tool For Your Infrastructure

Choosing the best configuration management tools is not easy, there is a wide range of options on the market, ranging from simple command-line tools to full-blown packaging systems, as well as application release automation and orchestration tools.

First of all, let's take a minute and look at the definition of "Configuration Managment". Configuration management deals with both hardware and software resources of a business. It often refers to the process of systematically handling changes to a system in a way that it maintains its integrity over time.

Choose the right configuration management tool will make a Devops engineer's life much easier. But with so many CM tools out there, how do you choose the best one that fit for you? The key to slecting the best fit is to focus on what the business infrastructure needs are and analyze which of many offerings will suit your business. This blog helps you make the decision, and also, I am sharing the comparisons between Puppet and Ansible, based on my own experiences.

### Questions You Should Ask Yourself Before Choose Anything:
1. Consider the full context of the whole enginering process. How does the whole application stack look like? Is it a typical frontend/backend/db stack or something more complext? What existing tools are the engineers using? The tool you choose should fits in the existing tool chain in an easy enough manner. The ultimate goal here is to enable full end-to-end integration, delivery, monitoring and reporting.
2. Where is your infrastructure? Cloud/In-house or hybird. Does this tool support the different types of architectural platform? Even though your current infrastructure is private on-premise, what about couple of years later?
3. What's your infrastructure growth rate? Is the tool you choose easy to sacle, along with your infrastructure?
4. How much in-depth will the engineer team be involved in writing recipes, manifests, or playbooks? Does the tool require a deep learning curve?
5. How inclusive should the tool be? Do you just want to manage the provisioning of software into the operations environment, or do you want to support a full DevOps environment?

After you fully answered the above 5 questions, you should have your answer. Let me give you my answer, maybe it will help or inspire you. :)

So based on the above 5 questions, I choose Ansible for my new job, as a senior Devops engineer. I was a puppet user/programmer for 2 years, and I didn't really like it. For me, Ansible is easy to implement, there is no agent required running on the target servers, and I am a Python programmer, I like YAML.

### Additional: Ansible vs Puppet

#### Server and client: 
**Puppet**:
* Puppet requires one or more "master" servers, along with a special puppet agent installed on each target/client server. Eventhough you could choose to not have the client running in a background process, only invoke when needed, but you still need to install the puppet client package. 
**Ansible**:
* No master/client requirement. The ansible-playbook can be triggered on any server. You only need SSH protocol and proper SSH keys setups.
	
#### Push vs Pull
**Puppet**:
* If runs as a background process, the puppet clinet "pull" information from mater periodically, this sometimes could cause surprises.
**Ansible**:
* Ansible playbook pushes configuration changes to clients.

#### Resources vs Ordering
**Puppet**:
*Resources defined in a Puppet manifest are not applied in order of their appearance (ex: top->bottom) which is confusing for people who come from conventional programming languages (C, Java, etc). Instead resources are applied randomly, unless explicit resource ordering is used. Ex: “before”, ”require”, or chaining arrows.
**Ansible**:
* The playbooks are applied top-to-bottom, as they appear in the file. This is more intuitive for developers coming from other languages. 
	
#### Modules vs Playbooks
**Puppet**:
* Puppet itself provides a series of primitives (File, User, Package, Service, etc) that one can compose modules with. Modules are either written in-house or downloaded from PuppetForge. Some open-source puppet modules are poorly written.
**Ansible**:
* Ansible follows Python’s “batteries included” philosophy. There is an extensive STDLIB of Ansible modules automatically included as part of the Ansible installation. There is also a site for community written “roles” called Ansible Galaxy.

#### Programming Language:
**Puppet**:
* Puppet is built upon Ruby. Writting complex functionality is done through Ruby modules. But on top of that, Puppet has its own syntax. You kinda need to learn both languages.
**Ansible**:
* Ansible is built upon Python and follows YAML syntax. "Life is short, use Python" :)
