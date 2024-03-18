# :cloud: Mawingu-Dev
> :bulb: Devstack Project
## 💬 Description
> This are the steps to follow to deploy a django application on a devstack instance. I have installed devstack on a virtual machine and through horizon I will create an instance and clone a django application on that instance and run it.

# :briefcase: Resources
> Links to the youtube videos and documentation i have used to achieve this.
> 1. ![Nginx and Gunicorn with django](https://www.youtube.com/watch?v=YnrgBeIRtvo)
> 2. ![DevStack for beginners](https://www.youtube.com/watch?v=_gWfFEuert8&t=1938s)
> 3. ![DevStack Docs](https://docs.openstack.org/devstack/latest/)
## 📜 More
> ## Virtual Machine or Instance
>   1. Virtualization or simulation of a computer system.
     > For this project I am using an virtual machine that's running on ubuntu Os.
      
> ## Devstack
   1. An development open-source cloud platform running as IaaS model that allows you to manage and create resources such as computation, networks etc. In other words the "minikube" to openstack. 
     > I installed devstack on my machine using the stable/xena branch.
    
> ## Django App
  1. A python framework that allows you to create web application and more.
     > In this project I am going to clone a simple django project of mine that just displays a static page.
     
> ## Nginx and G-Unicorn
  1. Nginx will serve as a server proxy while G-unicorn will implement a WSGI server.
     > This will allow me to serve my application to a web browser.
## 🔧 Steps
> I am considering you have installed and deployed devstack on your virtual machine and have managed to open up horizon on your web browser.
> If you want to follow the CLI codes you can use link. ![CLI STEPS](https://docs.openstack.org/networking-ovn/latest/contributor/testing.html)
> 1. Create a new project.
     > A project is a logical grouping of resources in a devstack environment that are isolated from other users and groups.
     > On horizon, on the left side bar navigate to Identity -> Projects -> Create New Project
> 1. Create a new user.
     > This will be an entity that will allow you to interact with the resources in devstack through your created project
     > On horizon, on the left side bar navigate to Identity -> Users -> Create New User
     > Choose member as the role and link the user to your created project.
     > Sign out as the admin and log in as the new user with the credentials made.
> 1. Create a new network.
     > A network isolation for instances and resources in a project.
     > On horizon, on the left side bar navigate to Project -> Network -> Networks -> Create New Network
     > Add the name, subnet name , set IP address (I used 192.168.0/24) and create.
> 1. Create a Router.
     > A router will allow transfer of data through networks by reading IP Addresses.
     > On horizon, on the left side bar navigate to Project -> Network -> Routers -> Create New
     > Add an interface to the created router to link the external network to the private network created.
> 1. Create a Security Group.
     > A security group is a virtual firewall that controls ingress and egress traffic to your instance.
     > On horizon, on the left sidebar click on Network -> Security Groups -> Create New
     > Add a new rule in the Security group to allow SSH traffic from your hardware node.
> 1. Generate SSH key
> The key will be used to log in into an instance.

```bash
			ssh-keygen -b 4096
```

> 1.  Create an Instance.
This will be a virtual machine instance associated with its networks, security group etc.
> On horizon, on the left sidebar click on Compute -> Instance -> Create New
> Create new instance with predefined specs called flavors (I used the m1.small)  and with a downloaded images ( i used the ubuntu image). ![Click here to select images to download](https://docs.openstack.org/image-guide/obtain-images.html)
> Once downloaded you can add it through the images bar and select it during instance creation
    
> 1. Create an Floating IP.
> This will allow accessibility of the instance with outside network, this will allow accessing the instance over SSH. 
> On horizon, on the left sidebar click on Network -> Floating IP -> Create New
> Set the pool to the external network and associate it with the instance created.

> 1. Login to instance with SSH.
     > Access the instance with the floating IP created and private SSH key generated.
```bash
			ssh -i </path/to/ssh/private_key> <user_name@ip_address>
```   
