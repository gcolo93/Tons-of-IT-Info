Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 21 The Internet
Chapter 22 Virtualization
Chapter 23 Portable Computing
42h 21m remaining
CHAPTER 22
Virtualization
In this chapter, you will learn how to

•   Explain why virtualization is so highly adopted

•   Describe the service layers and architectures, and characteristics of cloud computing

The subject of this chapter, virtualization, can be a little slippery and hard to understand. A big reason is that virtualization isn’t one concrete thing you can grab with your hands. There are many kinds of virtualization, and the thread tying them together isn’t very obvious—it’s just an idea.

The important idea at the heart of every kind of virtualization is to take an existing component (anything in or attached to the system) and make it more flexible by replacing it with a layer of software that (as far as anything interacting with the component can tell) behaves the same. This idea is so fundamental to modern computing that, way back in Chapter 4, we looked at a well-known application of it: virtual memory.

Once upon a time, computer programs had direct access to the system’s RAM. Programs in modern systems actually access virtual memory—a layer of software that, as far as the program can tell, is RAM. Operating systems use the extra flexibility this layer of software provides to store the memory contents of active programs in RAM but swap the memory contents of idle programs out to a storage drive.

To virtualize something is to replace it with this more flexible layer of software. Why do we virtualize things? The answer is almost always because the extra flexibility enables us to do something new, makes things easier to manage, or both.

This chapter delves into virtualization in detail, starting with the reasons why virtualization is important today, and then looking at a collection of technologies that use virtualization extensively: cloud computing. Let’s get started.

1101
Hardware Virtualization
One of the most important kinds of virtualization, hardware virtualization, takes the entire computer that an OS expects to interact with and virtualizes it. The physical host computer uses software known as a hypervisor to create environments (each saved in a separate file) that have virtual versions of all the “hardware” devices you need to install and run an OS. The hypervisor allocates fractions of the host’s real hardware resources to power these virtual devices.



EXAM TIP   For clarity, I will specify what kind of virtualization I mean and only use the term “virtualization” by itself to refer to the broader idea. If you see “virtualization” by itself on the exam, however, it will almost certainly mean hardware virtualization!

These environments are called virtual machines (VMs) or guests. Figure 22-1 shows one such example: a Windows host system using a hypervisor called Hyper-V to run two guest virtual machines, one running Ubuntu Linux and another running Windows 10.



Figure 22-1  Hyper-V running Linux and Windows 10

The CompTIA A+ 1101 objectives expect you to be able to summarize the purpose of virtual machines. We’ll build up to the list of purposes CompTIA has in mind by the end of this section, but first I want to get philosophical so that we don’t lose sight of something.

Just as a hammer is a tool for the purpose of hitting things, a computer is a tool for the purpose of computing things. Virtualizing a computer doesn’t change this—the purpose of a virtual machine is still to run computations! The benefits of hardware virtualization are to make virtual machines more convenient than physical computers in some situations, but they are just another tool we can use to meet a need or solve a problem.

Let’s take a closer look how we can use hardware virtualization on our own local systems, and then address the elephant in the room—what are the benefits of virtual computers and what on Earth can you do with them? Then, I’ll walk you through the process of setting up a VM of your own to experiment with, and finish the section with a look at how hardware virtualization tends to manifest on a server.

Client-side Virtualization
A normal operating system installed directly on the hardware uses programming called a supervisor (better known as the kernel) to handle very low-level interaction among hardware and software, such as task scheduling, allotment of time and resources, and so on. Figure 22-2 shows how the supervisor works between the OS and the hardware.



Figure 22-2  Supervisor on a generic single system

Hardware virtualization enables one machine—the host—to run multiple guest operating systems simultaneously. The CompTIA A+ 1101 objectives focus mostly on what CompTIA calls client-side virtualization—when the VM host also serves as someone’s day-to-day workstation.



EXAM TIP   If you see the words “client-side” and “virtualization” in the same question on the exam, keep an open mind! As a term, “client-side virtualization” is vague. It refers to where the work is done—usually in contrast to server-side virtualization—and omits what kind of virtualization it is. I think CompTIA means client-side hardware virtualization, but CompTIA might mean client-side desktop virtualization. We’ll discuss desktop virtualization later in the chapter.

In hardware virtualization, the hypervisor takes on the role of the supervisor—plus the added chore of dividing up the hardware resources among active virtual machines. Figure 22-3 shows a single hypervisor hosting three different guest virtual machines.



Figure 22-3  Hypervisor on a generic single system hosting three virtual machines

There are a fair number of hypervisors to choose from. Microsoft’s Hyper-V (shown earlier in Figure 22-1) is included in Windows Server and Windows Pro. Another very popular hypervisor is Oracle VM VirtualBox (see Figure 22-4), which runs on Windows, macOS, and Linux.



Figure 22-4  Oracle VM VirtualBox

This is in no way a complete list. Many Linux users swear by KVM, for example, and VMware has long made a number of popular commercial hypervisors.

Benefits of Virtualization
One of the tricks to getting your mind around any given kind of virtualization is understanding why anyone bothers—what benefits are they getting from the extra flexibility? Hardware virtualization unlocks a lot of little benefits, so I’ll focus on two big categories: saving resources and making systems easier to manage.

Saving Resources
A dirty little secret of modern life is that most people have things they almost never use—and big organizations are no different! When it comes to resource use, most computers and cars have a lot in common: they spend most of the time just sitting there, a little time partly occupied, and are only rarely used to their full capacity.

Before hardware virtualization, each OS needed a physical system. With a hypervisor, though, you can place multiple virtual servers or clients on a single physical system. Rather than one machine running a Windows file server, another Windows system acting as a DNS server, and a third machine running Linux for a DHCP server, why not use one physical computer to handle all three servers simultaneously as virtual machines?

The flexibility of virtual machines makes it possible to consolidate multiple systems down into a single box. Every physical computer requires a minimum amount of hardware, and a lot of that hardware—like its fans, power supply, and motherboard—require a minimum amount of electricity just to turn on. When organizations reduce the number of physical systems they need to do the same amount of work, they benefit from ongoing energy savings (see Figure 22-5).



Figure 22-5  Hardware virtualization saves power.

Lowering your energy bill is great, but it’s just where the benefits start. Hardware consolidation reduces the time and money an organization spends maintaining hardware and enables it to entirely avoid purchasing expensive hardware that rarely if ever runs at full capacity during its useful lifetime.

These benefits are biggest for servers, but they also apply to desktop computers. A Windows user who needs regular access to Linux doesn’t need two computers or a complex multi-boot setup—they just need a Windows hypervisor and a Linux VM. Likewise, support techs who need occasional access to every OS version they support can have a single system with a VM for each.

Complex desktop PCs can also be replaced with simple but durable thin clients that offload most of their work on servers. Each thin client still needs a keyboard, mouse, and monitor—but they may not need hard drives or fans. They can usually get away with simpler motherboards and less-powerful CPUs, GPUs (which can be built into the CPUs), and RAM.

Simplifying System Management and Security
The most popular reason for virtualizing is probably the benefits we reap from easy-to-manage systems. We can take advantage of the fact that VMs are simply files: like any other files, they are easy to copy around. It’s easy to set up new employees with a department-specific virtual machine that has all of the software they need already installed.

These management advantages turn out to be a nice security advantage, too. Let’s say you have set up a new employee with a traditional physical system. If that system goes down—due to hacking, malware, or so on—you need to restore the system from a backup (which may or may not be easily at hand) or break out the OS installation media. With hardware virtualization, the host machine, hypervisor, and any other VMs it runs are generally unaffected and uninfected; you merely need to shut down the virtual machine and reload an alternate (clean) copy of it. And because VMs are just files, these are easy to keep around.



TIP   VMs on a network face the same risks—and pose the same risks to other networked devices—as any other networked computer. Networked VMs have security requirements similar to a physical system and should usually get whatever security treatment you’d give physical systems. VMs need regular OS and software updates, firewalls, anti-malware software, accounts with strong passwords, backups, and good general security hygiene.

Most virtual machines also let us make a snapshot or checkpoint, which saves the virtual machine’s state at that moment, allowing us to quickly return to this state later. Snapshots are great for doing risky (or even not-so-risky) maintenance with a safety net. They also give you the freedom to install updates without worrying they’ll render the OS unusable, making it easier to keep systems secure. These aren’t, however, a long-term backup strategy—each snapshot may reduce performance and should be removed as soon as the danger has passed. Figure 22-6 shows VMware ESXi saving a snapshot.



Figure 22-6  Saving a snapshot



TIP   Virtualized operating systems use the same security features as real operating systems. For each virtual machine user account, you’ll need to keep track of user names, passwords, permissions, and so on, just like on a normal PC.

Purpose of Virtual Machines
As I said earlier: like physical computers, virtual machines are just another tool for computing things. This means you can find people using virtual machines to do almost anything they can do with physical computers. It also means you’ll find people using physical computers for things virtual machines do well.

Above all else, it means that—just like with physical computers—people are constantly finding new ways to use virtual machines. Let’s review the list of purposes you should know for the CompTIA A+ 1101 exam—but keep in mind that the best problem you ever solve with a VM may not be on this list!

Sandboxing
We’ll take a closer look at security topics in Chapter 27, so for now I just want to touch lightly on a fundamental idea. If you need to run software that you don’t trust, the safest way to do it is to run it on a separate computer where it can’t interact with real data and programs.

Isolating untrusted software this well is rarely practical, so the next-best thing is to run the software inside a tightly restricted execution environment—a sandbox—which limits how the software can interact with the host system and any files and other programs on it. CompTIA wants you to know that virtual machines can serve as a sandbox—but I need to split a few hairs.

First, there are many kinds of sandbox. One of the most common types is for keeping applications from interfering with each other in day-to-day use. These generally come with the operating system and are especially important on smartphones. Another type enables you to occasionally run untrusted software in an environment that is isolated from the core system—a good example is Windows Sandbox, included in Windows 10 Pro and newer. There are also sandboxes designed from the ground up for analyzing the behavior and safety of software you run inside them.

Second, a general virtual machine is not a true sandbox. It is not designed to isolate software! As a tool, virtual machines just happen to be useful for this task; they are better than running sketchy software on the host, but not perfectly safe.



NOTE   If you need to isolate the software for boring reasons—imagine you need to run multiple versions of a program but can’t install more than one on a system—a VM is just fine (though it will consume a lot of resources).

Development Testing
When it comes to programming, there’s always a chance that differences between systems will cause the software that developers are working on to run differently—or not at all! For this reason, developers often test the software they are writing in a development environment that matches the intended environment (i.e., where the software should run) as closely as possible. Virtual machines are a popular choice for these environments.



EXAM TIP   The CompTIA A+ 1101 objectives call this purpose test development. I think CompTIA means “test” as a verb—to test development work. But there’s a chance CompTIA means “development” as the verb—to develop tests. Know that VMs are a popular way to test development work and look for “VM” in the answers if you see a question about creating or developing tests.

It isn’t enough to just use any VM, though. Surprisingly small differences between systems can cause trouble. Not only are two systems set up by hand likely to differ, but differences accumulate on every system as users install different software in them, run updates at different times, create different files, and so on. Developers may regularly run special software to prepare a fresh VM—to provision it with the exact operating system, files, and software specified in configuration files shared among everyone working on the project.

Application Virtualization
The final purpose of VMs that CompTIA focuses on is application virtualization. Application virtualization entails virtualizing the OS capabilities that an application would normally use to install and do its work. The flexibility this creates enables some neat tricks, such as being able to run an application without installing it, run applications that only work in a different version of your OS, run applications that would normally interfere with each other, and even run applications that were written for another OS entirely.



EXAM TIP   The CompTIA A+ 1101 objectives call out two of these tricks: running applications for a different OS version (identified as legacy software/OS), and running applications written for another OS (identified as cross-platform virtualization). Look for “application virtualization” or “virtual machines” as an answer to questions about running applications for a different or older OS.

I need to be clear about two things here. First, there are different approaches to application virtualization out there and they don’t all use virtual machines. Second, you can manually use virtual machines to accomplish these same tricks, but application virtualization means more than just running an application in a VM. The point is to have your cake and eat it, too.

Here’s an example of application virtualization. Having to run a full Windows 7 VM to access a legacy app on macOS is clunky. Users must jump through hoops to move files around between the host system and the VM, and they’ll almost certainly catch themselves trying to use macOS keyboard shortcuts inside the Windows VM or Windows keyboard shortcuts outside of it.

In contrast, some forms of application virtualization are so seamless that users will launch it just like any other native desktop app and not even know they are interacting with old software written for Windows 7.

Creating a Virtual Machine
Before we go any further, let’s take the basic pieces you’ve learned about hardware virtualization and put them together in one of its simplest forms: a virtual machine on your local system.

The basic process for creating virtual machines is as follows:

1.   Set up your system’s hardware to support virtual machines and verify it can meet the resource requirements for running them.

2.   Install a hypervisor on your system.

3.   Create a new virtual machine that has the proper virtualized hardware requirements for the guest OS.

4.   Start the new virtual machine and install the new guest OS exactly as you’d install it on a new physical machine.

Hardware Support and Resource Requirements
While any computer running Linux, Windows, or macOS will support a hypervisor, there are a few hardware requirements we need to address.

Every Intel-based CPU since the late 1980s is designed to support a supervisor for multitasking, but it’s hard work for that same CPU to support multiple supervisors on multiple VMs. Both AMD and Intel added extra features to their CPUs just to support hypervisors: Intel’s VT-x and AMD’s AMD-V. This is hardware virtualization support, and VMs will run better with it enabled.

If your CPU and BIOS support hardware virtualization, you can turn it on or off inside the system setup utility (it may or may not be enabled by default). Figure 22-7 shows the virtualization setting in a typical system setup utility. Note that AMD’s AMD-V virtualization is often referred to as SVM mode, as shown in Figure 22-7.



Figure 22-7  BIOS setting for CPU hardware virtualization support on an AMD-based system

RAM  The most important concern is RAM. Each virtual machine needs just as much RAM as a physical one, so it’s common practice to stuff your host machine with large amounts of RAM. The more virtual machines you run, the more RAM you need. Generally, you need to leave enough RAM (4 GB recommended) for the hypervisor and every VM you intend to run simultaneously.



NOTE   As we discussed way back in Chapter 4, different motherboards can support different quantities of RAM. If you plan to build a PC to run virtual machines, it pays to do your research. You don’t want to get stuck with a board that maxes out at 16 GB of RAM.

VM Storage  VM files can be huge because they include everything installed on the VM. Depending on the OS and how the VM is used, the VM file could range from megabytes to hundreds of gigabytes. On top of that, every snapshot or checkpoint you make requires space. Figure 22-8 shows a newly minted Windows 10 VM taking about 10 GB of storage space.



Figure 22-8  Single VM file taking about 10 GB

The particulars of VM storage depend on your circumstances, but here are a few basic recommendations:

•   Make sure you have plenty of storage space for all of the VMs you plan to have, and room to grow.

•   Your VM files are precious. Plan ahead to protect them with good RAID arrays and regular backups to make sure they are available when you need them.

•   If performance is critical for your VMs, plan to store them on an SSD.

Virtual Networks
Probably one of the coolest features of VMs is that you can “virtually” network them in many different ways. Don’t just limit yourself to thinking, “Oh, can I get a VM to connect to the Internet?” Well, sure you can, but hypervisors do so much more. Every hypervisor has the capability to connect each of its virtual machines to a network in a number of different ways. All of these options depend on virtual switches, but the way this looks will vary a lot from hypervisor to hypervisor.

Some common ways to network VMs include the following:

•   Create an internal network (see Figure 22-9) for multiple VMs within the same hypervisor, enabling them to communicate with each other (and optionally the outside world).



Figure 22-9  Configuring a VM for an internal network in VirtualBox

•   Place a VM on a virtual network that only enables it to communicate with the host system.

•   “Bridge” a VM’s NIC to the host’s NIC, enabling the VM to join the same network that the host computer is connected to.

•   Provide a VM with no network, isolating it from other VMs, the host, and the broader network.

Installing a Virtual Machine
The actual process of installing a hypervisor is usually no more complicated than installing any other type of software. Let’s use Hyper-V as an example. If you have a Windows 10 or 11 Professional system, you can enable Microsoft’s Hyper-V by going to the Programs and Features Control Panel applet and selecting Turn Windows features on or off, which opens the Windows Features dialog box, as shown in Figure 22-10.



Figure 22-10  Installing Hyper-V in Windows



NOTE   If you are using Windows 10/11 Home, Hyper-V is not available from this menu. Use a third-party virtualization tool.

Once you’ve installed the hypervisor of choice, you’ll have a virtual machine manager (VMM) that acts as the primary place to create, start, stop, save, and delete guest virtual machines. Figure 22-11 shows the manager for VirtualBox.



Figure 22-11  Oracle VM VirtualBox Manager (three VMs installed)

How to Build a Virtual Machine
Now that you’ve got a hypervisor, you can set up a virtual machine. On pretty much any virtual machine manager, this is simply a matter of selecting New | Virtual Machine, which starts a wizard to ensure you’re creating the right virtual machine for your guest OS. Most hypervisors have presets for crucial settings (such as virtual RAM, storage space, and so on) to ensure your guest OS has the virtual hardware it needs to run. Figure 22-12 shows the VirtualBox wizard asking what OS you intend to install in the Machine Folder field. You also need to give the virtual machine a name. For this overview I’m going with Fedora Workstation.



Figure 22-12  Creating a new VM in Oracle VirtualBox



NOTE   Use descriptive names for virtual machines. This will spare you a lot of confusion when you have multiple VMs on a single host.

Click Next, and you get to pick how much memory you want for your VM (see Figure 22-13). VirtualBox recommends at least 1 GB for Fedora, but I’m going with 2 GB.



Figure 22-13  Selecting the amount of memory for the VM

After clicking Next, you get to create the virtual hard drive. Clicking Create opens the Create Virtual Hard Disk wizard, which asks several technical questions about hard disk file type and how it should allocate the space. I’m just going with the defaults, but it can be useful to change them in certain situations. Finally, on the last screen, you get to set how big the virtual disk will be, the default being 8 GB. That’s a bit small for me, so I’ve gone with 25 GB, as shown in Figure 22-14. With that, you’ve created a new virtual machine.



Figure 22-14  Setting the virtual drive size

Installing the Operating System
Once you’ve created the new guest VM, it’s time to install a guest operating system. Would you like to use Microsoft Windows in your virtual machine? No problem, but every Windows virtual machine requires a separate, legal copy of Windows; this also goes for any licensed software installed in the VM.

All good virtual machine managers enable you to load installation media from removable media on the host, but the easy way is to tell the new virtual machine to treat an ISO file as its own optical drive. In Figure 22-15, I’m installing Fedora Workstation on a VirtualBox virtual machine. I downloaded an ISO image from the Fedora Web site (https://getfedora.org) and selected it as the installation media. From here I click Start and install Fedora like any other installation.



Figure 22-15  Selecting the installation media

After you’ve gone through all the configuration and OS installation screens, you can start using your virtual machine. Figure 22-16 shows VirtualBox running the newly installed Fedora Workstation.



Figure 22-16  Fedora Workstation running in VirtualBox

Like with a real system, you can add or remove hardware—but adding hardware won’t take a trip to the electronics store or a box from Newegg. With a good hypervisor, you can easily add and remove virtual hard drives, virtual network cards, virtual RAM, and so on, helping you adapt your VM to meet changing needs. Figure 22-17 shows the Settings System screen from VirtualBox.



Figure 22-17  Configuring virtual hardware in VirtualBox



SIM   Check out the excellent Chapter 22 Show! and Click! sims on “Virtual Hardware” over at https://www.totalsem.com/110X. These help reinforce terminology and typical steps for setting up a virtual machine.

Server-side Virtualization
When it comes to servers, hardware virtualization has pretty much taken over everywhere. Many of the servers we access, such as those that power Web sites and video streaming services, are virtualized. These severs usually aren’t running in a desktop hypervisor such as VirtualBox because that type of hypervisor requires the host to have a full operating system.

This full host OS not only ties up at least enough resources to run a full VM—it also adds a little overhead to every operation. For this reason (and others), most server VMs run on a powerful hypervisor/OS combination called a bare-metal hypervisor. We call it bare metal because there’s no other software between it and the hardware—just bare metal. The industry also refers to this class of hypervisors as Type-1, and applications such as VirtualBox as Type-2 (see Figure 22-18).



Figure 22-18  Type-1 versus Type-2 hypervisors

I hope by this point that you have a sense of what hardware virtualization is—but don’t worry if you’re still a bit confused about why it’s a big deal. One hurdle to understanding how and why virtualization is continually revolutionizing IT is that the flexibility it creates is often most helpful at very large scales (like data centers with tens of thousands of servers) that aren’t familiar to most people. In the next section, we’ll see how this flexibility plays out on a massive scale.

To the Cloud
Before we look at what “the cloud” is, I want to take a step back and talk about something that will sound unrelated: money. One of the really great things money does is give us common, easily divisible units we can exchange for the goods and services we need. When we don’t have money, we have to trade goods and services to get it, and before money was invented, humans had to trade goods and services for other goods and services.

Let’s say I’m starving and all I have is a hammer, and you just so happen to have a chicken. I offer to build you something with my hammer, but all you really want is a hammer of your own. This might sound like a match made in heaven, but what if my hammer is actually worth at least five chickens, and you just have one? I can’t give you a fifth of a hammer, and once I trade the hammer for your chicken, I can’t use it to build anything else. I have to choose between going without food and wasting most of my hammer’s value. If only my hammer was money!

In the same vein, a top-of-the-line physical server can be a bit like a really expensive hammer. It has the resources to do a lot of work, but it is often underused because you would have to find tasks in which to take advantage of its various resources. Installing a hypervisor on this server sets us on the path to using it in a new, more productive way.

In this new model, servers become (a little) less like hammers and (a little) more like money. I still can’t trade a fifth of my hammer for a chicken, but a powerful physical server has the flexibility to host one huge VM, two large VMs, or one large VM and a dozen tiny ones—and this configuration can change constantly!

As the number of VM hosts and guest VMs increases, so do the options for distributing VMs across hosts to minimize unused resources (see Figure 22-19). At larger scales, the hosts become more and more like a pool of common, easily divisible units we can use to solve problems—more and more like money.



Figure 22-19  No vacancy on these hosts

Many organizations use this flexibility to make their own data centers more efficient, but its most impressive use is in the services offered by massive cloud computing providers. These companies cobble together massive pools of computing resources from data centers all around the world.

When we talk about the cloud, we’re talking not just about friendly file-storage services like Dropbox or Google Drive, but about all of the services that enable us to dip into the vast pools of computing resources sold by Amazon (see Figure 22-20), Microsoft, and many other companies over the open Internet. The technology at the heart of these innovative services is virtualization (and they apply it to far more than just virtual servers).



Figure 22-20  Amazon Web Services Management Console

The Service-Layer Cake
Service is the key to understanding the cloud. At the hardware level, we’d have trouble telling the difference between the cloud and the servers and networks that comprise the Internet as a whole. We use the servers and networks of the cloud through layers of software that add great value to the underlying hardware by making it simple to perform complex tasks or manage powerful hardware. As end users we generally interact with just the sweet software icing of the service-layer cake—Web applications like Dropbox, Gmail, and Facebook, which have been built atop it. The rest of the cake exists largely to support Web applications like these and their developers. Let’s slice it open (see Figure 22-21) and start at the bottom.



Figure 22-21  A tasty three-layer cake

Infrastructure as a Service
Large-scale global Infrastructure as a Service (IaaS) providers use hardware virtualization to minimize idle hardware, protect against data loss and downtime, and respond to spikes in demand. We can use big IaaS providers like Amazon Web Services (AWS) to launch new virtual servers using an operating system of choice on demand (see Figure 22-22) for pennies an hour. The beauty of IaaS is that you no longer need to purchase expensive, heavy hardware. You are using Amazon’s powerful infrastructure as a service.



Figure 22-22  Creating an instance on AWS

A huge number of Web sites are really more easily understood if you use the term Web applications. If you want to access Mike Meyers’ videos, you go to https://hub.totalsem.com. This Web site is really an application that you use to watch videos, practice simulation questions, and so forth. This Web application is a great tool, but as more people access the application, we often need to add more capacity so you won’t yell at us for a slow server. Luckily, our application is designed to run distributed across multiple servers. If we need more servers, we just add as many more virtual servers as we need. But even this is just scratching the surface. AWS provides many of the services needed to drive popular, complex Web applications—unlimited data storage (see Figure 22-23), database servers, caching, media hosting, and more—all billed by usage.



Figure 22-23  Amazon Simple Storage Service (S3)

The hitch is that, while we’re no longer responsible for the hardware, we are still responsible for configuring and maintaining the operating system and software of any virtual machines we create. This can mean we have a lot of flexibility to tune it for our needs, but it also requires knowledge of the underlying OS and time to manage it. If you want someone to handle the infrastructure, the operating system, and everything else (except your application), you need to move up to Platform as a Service (PaaS).

Platform as a Service
Web applications are built by programmers. Programmers do one thing really well: they program. The problem for programmers is that a Web application needs a lot more than just a programmer. Developing a Web application requires people to manage the infrastructure: system administrators, database administrators, general network support, and so on. A Web application also needs more than just hardware and an operating system. It needs development tools, monitoring tools, database tools, and potentially hundreds of other tools and services. Getting a Web application up and running is a big job.

A Platform as a Service (PaaS) provider gives programmers all the tools they need to deploy, administer, and maintain a Web application. The PaaS provider starts with some form of infrastructure, which could be provided by an IaaS, and on top of that infrastructure the provider builds a platform: a complete deployment and management system to handle every aspect of a Web application.

The important point of PaaS is that the infrastructure underneath the PaaS is largely invisible to the developer. The PaaS provider is aware of their infrastructure, but the developer cannot control it directly, and doesn’t need to think about its complexity. As far as the programmer is concerned, the PaaS is just a place to deploy and run his or her application.

Heroku, one of the earliest PaaS providers, creates a simple interface on top of the IaaS offerings of AWS, further reducing the complexity of developing and scaling Web applications. Heroku’s management console (see Figure 22-24) enables developers to increase or decrease the capacity of an application with a single slider, or easily set up add-ons that add a database, monitor logs, track performance, and more. It could take days for a tech or developer unfamiliar with the software and services to install, configure, and integrate a set of these services with a running application; PaaS providers help cut this down to minutes or hours.



Figure 22-24  Heroku’s management console

Software as a Service
Software as a Service (SaaS) sits at the top layer of the cake. SaaS shows up in a number of ways, but the best examples are the Web applications we just discussed. Some Web applications, such as Total Seminars Training Hub, charge for access. Other Web applications, like Google Maps, are offered for free. Users of these Web applications don’t own this software; you don’t get an installation DVD, nor is it something you can download once and keep using. If you want to use a Web application, you must get on the Internet and access the site. While this may seem like a disadvantage at first, the SaaS model provides access to necessary applications wherever you have an Internet connection, often without having to carry data with you or regularly update software. At the enterprise level, the subscription model of many SaaS providers makes it easier to budget and keep hundreds or thousands of computers up to date (see Figure 22-25).



Figure 22-25  SaaS versus updating every desktop

The challenge to defining SaaS perfectly is an argument that almost anything you access on the Internet could be called SaaS. A decade ago we would’ve called the Google search engine a Web site, but it provides a service (search) that you do not own and that you must access on the Internet. If you’re on the Internet, you’re arguably always using SaaS.

It isn’t all icing, though. In exchange for the flexibility of using public, third-party SaaS, you often have to trade strict control of your data. Security might not be crucial when someone uses Google Drive to draft a blog post, but many companies are concerned about sensitive intellectual property or business secrets traveling through untrusted networks and being stored on servers they don’t control.



EXAM TIP   Know the differences between basic cloud concepts such as SaaS, IaaS, and PaaS.

Ownership and Access
Security concerns like those just discussed don’t mean organizations have to forfeit all of the advantages of cloud computing, but they do make their management think hard about the trade-offs between cost, control, customization, and privacy. Some organizations also have unique capacity, performance, or other needs no existing cloud provider can meet. Each organization makes its own decisions about these trade-offs, but the result is usually a cloud network that can be described as public, private, community, or hybrid.

Public Cloud
Most folks usually just interact with a public cloud, a term used to describe software, platforms, and infrastructure delivered through networks that the general public can use. When we talk about the cloud, this is what we mean. Out on the open, public Internet, cloud services and applications can collaborate in ways that make it easier to think of them collectively as the cloud than as many public clouds. The public doesn’t own this cloud—the hardware is often owned by companies like Amazon, Google, and Microsoft—but there’s nothing to stop a company like Netflix from building its Web application atop the IaaS offerings of all three of these companies at once.

Private Cloud
If a business wants some of the flexibility of the cloud, needs complete ownership of its data, and can afford both, it can build an internal cloud the business actually owns—a private cloud. A security-minded company with enough resources could build an internal IaaS network in an onsite data center. Departments within the company could create and destroy virtual machines as needed and develop SaaS to meet collaboration, planning, or task and time management needs all without sending the data over the open Internet. A company with these needs but without the space or knowledge to build and maintain a private cloud can also contract a third party to maintain or host it.

Community Cloud
While a community center is usually a public gathering place for those in the community it serves, a community cloud is more like a private cloud paid for and used by more than one organization. Community clouds aren’t run by a city or state for citizens’ use; the community in this case is a group of organizations with similar goals or needs. If you’re a military contractor working on classified projects, wouldn’t it be nice to share the burden of defending your cloud against sophisticated attackers sponsored by foreign states with other military and intelligence contractors?

Hybrid Cloud
Sometimes we can have our cake and eat it too. Not all data is crucial, and not every document is a secret. Needs that an organization can only meet in-house might be less important than keeping an application running when demand exceeds what it can handle onsite. We can build a hybrid cloud by connecting some combination of public, private, and community clouds, allowing communication between them. Using a hybrid cloud model can mean not having to maintain a private cloud powerful enough to meet peak demand—an application can grow into a public cloud instead of grind to a halt, a technique called cloud bursting.

But a hybrid cloud isn’t just about letting one Web application span two types of cloud—it’s also about integrating services across them. Let’s take a look at how Jimmy could use a hybrid cloud to expand his business.



EXAM TIP   Know the differences between public, private, community, and hybrid cloud models.

Jimmy runs a national chain of sandwich shops and is looking into drone-delivered lunch. He’ll need a new application in his private cloud to calculate routes and track drones, and that application will have to integrate with the existing order-tracking application in his private cloud. But then he’ll also need to integrate it with a third-party weather application in the public cloud to avoid sending drones out in a blizzard, and a flight-plan application running in a community cloud to avoid other drones, helicopters, and aircraft (and vice versa). The sum of these integrated services and applications is the hybrid cloud that will power Jimmy’s drone-delivered lunch.

Cloud Characteristics
When it comes to whether and how to make use of cloud computing, every organization has to weigh the positives and negatives of the cloud against a more traditional approach. Different organizations will care about different things, but let’s take a moment to discuss five cloud characteristics that CompTIA wants you to know for the exam.

Shared Resources
Cloud computing focuses less on individual physical systems and more on the underlying resources. Instead of renting out each physical unit separately, cloud providers aggregate them into a pool of shared resources that they make available on-demand. The provider’s customers draw from this pool as they need additional resources and release them back into the pool when they are done.

This flexibility is one of the cloud’s big strengths. For example, this makes it practical to spin up tons of resources to render special-effects animations for an upcoming movie and release the resources once the job’s done. Unfortunately, this also means jobs for other users are likely running on the same hardware—and that’s not always acceptable.

Most cloud neighbors are fine, but you never know! There’s always a chance that a cloud neighbor could be intentionally exploiting a weakness in the host system to spy on their neighbors, could get hacked or infected with malware, or could overuse shared resources in a way that hinders performance for everyone else.

Rapid Elasticity
Let’s say you start a new Web application. If you use an IaaS provider such as Amazon, you can start with a single server and get your new Web application out there. But what happens if your application gets really, really popular? No problem! Using AWS features, you can easily expand the number of servers, even spread them out geographically, with just a click of the switch. This capability is known as rapid elasticity.

Metered Utilization
Ah, the biggest downside to using someone else’s cloud: you have to write a check to whoever is doing the work for you—and boy can these cloud providers get creative about how to charge you! In many cases they charge a precise metered utilization rate based on factors such as the traffic that goes in and out of your Web application and how much data you store. In other cases you pay for the exact amount of time that every single one of your virtualized servers is running.

Regardless of how costs are measured, this differs from more traditional hosting with a fixed monthly or yearly fee. You pay for what resources you use, rather than a more general fee for all the hardware of a system.

High Availability
For every small organization with a single physical server doing some critical job 24 hours a day, there’s a tech who doesn’t sleep well at night. All kinds of problems can knock a single system out of commission for hours or days, and many organizations can’t justify the cost of hiring someone to keep an eye on the server closet all night just in case.

Large cloud providers, however, have an army of automated systems and technicians perpetually watching over their global network of data centers. This already reduces the odds of an extended outage, enabling many cloud providers to promise that most of their services will be available 99.9 percent of the time or more.

Cloud computing enables organizations to get as close to 100 percent uptime as they can afford. Sometimes this is as simple as paying the cloud provider extra for a service to guarantee greater uptime. Organizations can also design their cloud deployments for high availability—for example, they can set up redundant servers all around the world and automatically reroute traffic whenever a server is down.



NOTE   High availability isn’t limited to the cloud—it is a huge topic in its own right! If you continue on to take the CompTIA Network+ exam, you’ll learn more about how important high availability is in networking and data centers.

File Synchronization
Cloud file storage services, like Dropbox and Box, were early smash successes in getting people to move to the cloud for some of their storage needs. Most of these services provide file synchronization apps that propagate file changes to the storage provider on to any other connected devices. Synchronization apps make it easy to access the same set of files across multiple devices.

These days, file synchronization is often bundled with productivity suites (i.e., collections of apps that enable you to edit documents, spreadsheets, presentations, and so on) such as Microsoft 365 and Google Workspaces. Regardless of how your organization approaches it, file synchronization makes it easier for users to collaborate or work on the same files from multiple devices without having to shuffle files around.

Unfortunately, cloud-based file synchronization also means giving up a lot of control over the organization’s files to the provider. It also makes it easier for disgruntled users to pass documents on to people who shouldn’t have access to them.

Desktop Virtualization
Desktop virtualization tries to apply the flexibility associated with both hardware virtualization and cloud computing to user workstations. The most common forms of desktop virtualization entail using a client program on one device to connect to a virtual desktop, providing access to a user’s files and applications.

If each human user still needs a system to access their virtual desktop, why would an organization be eager to also set aside server resources for them? Some of the big reasons are control, security, and management. Every user walking around with a laptop stuffed to the gills with sensitive organization data and applications is a huge risk! Desktop virtualization enables users to access the apps and files they need without storing them on local devices that could get lost or stolen at any time.

Some folks do desktop virtualization with just a remote desktop client and a user account on a multiuser OS such as Windows Server. The CompTIA A+ 1101 objectives focus on a form called virtual desktop infrastructure (VDI), in which each user’s client program connects to an automatically managed virtual machine running on a central server. In many organizations these VDI servers will be on premises, but it’s also possible to set up VDI servers in the cloud.



NOTE   CompTIA didn’t include cloud-based Desktop as a Service (DaaS) in the 1101 objectives, but any organization considering cloud-based VDI will likely consider using DaaS as well. They both accomplish roughly the same goal, but differ when it comes to cost, licensing, control, flexibility, and management.

Chapter Review
Questions
1.   Upgrading which component of a host machine would most likely enable you to run more virtual machines simultaneously?

A.   CPU

B.   Hard drive

C.   RAM

D.   Windows

2.   Which of the following could an organization use to enable its users to access their files and applications from multiple devices?

A.   Virtual desktop

B.   Client-side virtual machine

C.   File-synchronization service

D.   Virtual memory

3.   What feature lets you save a VM’s state so you can quickly restore to that point? (Choose two.)

A.   Checkpoint

B.   Save

C.   Snapshot

D.   Zip

4.   What do you need to install a legal copy of Windows 10 into a virtual machine using VirtualBox?

A.   A valid Windows 10 license

B.   Valid Windows 10 installation media

C.   A valid ESXi key

D.   A second NIC

5.   Which of the following is an advantage of a virtual machine over a physical machine?

A.   Increased performance

B.   Hardware consolidation

C.   No backups needed

D.   Operating systems included

6.   Janelle wants to start a new photo-sharing service for real pictures of Bigfoot, but doesn’t own any servers. How can she quickly create a new server to run her service?

A.   Public cloud

B.   Private cloud

C.   Community cloud

D.   Hybrid cloud

7.   After the unforeseen failure of her Bigfoot-picture-sharing service, bgFootr—which got hacked when she failed to stay on top of her security updates—Janelle has a great new idea for a new service to report Loch Ness Monster sightings. What service would help keep her from having to play system administrator?

A.   Software as a Service

B.   Infrastructure as a Service

C.   Platform as a Service

D.   Network as a Service

8.   Which kind of hypervisor is installed and run from within a full operating system?

A.   Bare-metal

B.   Virtual-metal

C.   Type-1

D.   Type-2

9.   When a virtual machine is not running, how is it stored?

A.   Firmware

B.   RAM drive

C.   Optical disc

D.   Files

10.   BigTracks is a successful Bigfoot-tracking company using an internal service to manage all of its automated Bigfoot monitoring stations. A Bigfoot migration has caused a massive increase in the amount of audio and video sent back from their stations. In order to add short-term capacity, they can create new servers in the public cloud. What model of cloud computing does this describe?

A.   Public cloud

B.   Private cloud

C.   Community cloud

D.   Hybrid cloud

Answers
1.   C. Adding more RAM will enable you to run more simultaneous VMs. Upgrading a hard drive could help, but it’s not the best answer here.

2.   A. Users can access a virtual desktop, which may include their files and applications, from different devices.

3.   A, C. The saved state of a VM is called a snapshot or checkpoint. Not to be confused with a true backup.

4.   A. You need a valid Windows 10 license to run Windows legally.

5.   B. A big benefit of hardware virtualization is hardware consolidation.

6.   A. Using the public cloud will enable Janelle to quickly create the servers she needs.

7.   C. By switching to a PaaS, Janelle can concentrate on creating her service and leave the lower-level administration up to the PaaS provider.

8.   D. A Type-2 hypervisor runs inside a full operating system.

9.   D. VMs are just files, usually stored on a hard drive.

10.   D. BigTracks is creating a hybrid cloud by connecting its internal private cloud to a public cloud to quickly expand capacity.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right

Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 22 Virtualization
Chapter 23 Portable Computing
Chapter 24 Mobile Devices
42h 21m remaining
CHAPTER 23
Portable Computing
In this chapter, you will learn how to

•   Describe the many types of portable computing devices available

•   Explain ways to expand portable computers

•   Manage and maintain portable computers

•   Upgrade and repair portable computers

•   Troubleshoot portable computers

There are times when the walls close in, when you need a change of scenery to get that elusive spark that inspires greatness . . . or sometimes you just need to get away from your coworkers for a few hours because they’re driving you nuts! For many occupations, that’s difficult to do. You need access to your documents and spreadsheets; you can’t function without e-mail or the Internet. In short, you need a computer to get your job done.

Portable computing devices combine mobility with accessibility to bring you the best of both worlds; portables enable you to take some or even all of your computing capabilities with you when you go. Featuring all the bells and whistles of a desktop system, many portables offer a seamless transition from desk to café table.

This chapter looks at the classic portable computer, essentially a desktop transformed into a mobile format. Classic portables usually run the same operating systems as their desktop counterparts—Windows, macOS, or Linux. However there are some operating systems—like Chrome OS, based on Linux—that are unique to portable computers.

Historical/Conceptual
Portable Computing Devices
All portable devices share certain features. For output, they use LCD screens, although these vary from 20-inch behemoths to diminutive 10-inch displays. Portable computing devices employ sound of varying quality, from bland mono playback to fairly nice faux-surround reproductions. All of them run on DC electricity stored in batteries when not plugged into an AC outlet.

When asked about portable computing devices, most folks describe the traditional clamshell notebook computer, such as the one shown in Figure 23-1, with built-in LCD monitor, keyboard, and input device (a trackpad, in this case). The notebook is also called a portable or a laptop. All the terms are synonymous. A typical laptop functions as a fully standalone computer, but there are always trade-offs that come with portability. Common trade-offs are price, weight, size, battery life, computing power, input devices, ports, drives, support for hardware upgrades, storage capacity, durability, and the quality of any warranty/support programs. Finding the right portable is easier if you can figure out what it will be used for and narrow your search to only devices with essential features and exclude those with unacceptable trade-offs.



Figure 23-1  An older notebook computer

Taxonomy
The companies making mobile and portable devices experiment a lot, so the terms we use to describe these devices are always in flux. New device categories and their related marketing terms may flood the market and blur the lines between existing categories one year, only to fall out of use within a few years.

The CompTIA A+ objectives don’t focus on these terms and categories, but it’s still a good idea to keep up with them. Knowing how to categorize portable and mobile devices makes it easier to identify devices that are a good fit for specific uses. It also helps you apply the best troubleshooting procedures for a given device. These categories can be slippery, so don’t think of them as mutually exclusive. Sometimes more than one of these terms apply to a single device.

Portable vs. Mobile
Over the years, the lines between portable computing devices such as laptops and mobile devices such as smartphones have blurred. Smartphones have become more powerful, laptops have incorporated touch screens and smaller form factors, and many tablets allow the use of external keyboards and mice. Despite these blurred lines, portable computing devices and mobile devices are separate concepts, with unique use cases and applications. A good rule of thumb is to look at the operating system that the device uses. If it uses the same operating system as its desktop counterparts, it is a portable device. If it uses a dedicated mobile operating system like Android, iOS, or iPadOS, it is a mobile device.

Types of Laptops
There are many terms that address the size or purpose of traditional clamshell laptops/notebooks, but over time, a lot of these distinctions have become less important. As the technology has been developed, use cases for many laptops have started to overlap. Terms like ultrabook, thin and light, and business laptop are mostly for marketing at this point, because apart from the examples I’m about to mention, laptops in general are a lot thinner, lighter, and more powerful than they were when many of these terms were coined (see Figure 23-2).



Figure 23-2  Older full-size laptop (left) versus the thin-slice aesthetic of the MacBook Air (right)

•   Gaming laptops, which tend to have flashy designs, typically come loaded with the latest top-end processors, graphics cards, RAM, SSDs, and large, high-quality displays. They also tend to come with thoughtful touches like RGB lighting.

•   A Chromebook is a portable computer running Google’s Linux-based Chrome OS. Chrome OS is a proprietary Linux-based operating system developed by Google. Thanks to Chrome OS, Chromebooks offer an experience focused on Web applications by making use of virtually unlimited data storage in the cloud and Software as a Service (SaaS) applications available over the Web. Using primarily cloud-based applications and storage allows users to get by with less powerful hardware, and as a result saves on cost. Because they offload so much work, Chromebooks have a reputation for being cheap and light, but premium Chromebooks are increasingly common.

•   2-in-1s are touch-screen computers somewhere along the spectrum from laptop-and-tablet to tablet-and-laptop. We’ll take a closer look at pure mobile tablets (such as the Apple iPad and various Android tablets) in Chapter 24. Some 2-in-1s have removable screens that separate from the rest of the laptop to function as a tablet (see Figure 23-3). Others have special hinges that enable you to fold the entire device up and use it in tablet form. 2-in-1s are also sometimes referred to as convertibles or hybrids.



Figure 23-3  Microsoft Surface Pro 6 with its keyboard cover (Used with permission from Microsoft)



NOTE   Innovative portable form factors like those in the 2-in-1 category are often designed to be handled, rotated, flipped, and passed around. As a result, Windows now supports the automatic screen-rotation tricks we’ve seen on smartphones and tablets for years. Anyone who has used a device like this for long knows that occasionally you’ll run into problems with the automatic screen-orientation sensor; see the “Troubleshooting Portable Computers” section later in the chapter for fixes.

1101
Input Devices
Portable computers come with a variety of input devices. Most have a fully functional keyboard and a device to control the mouse pointer.

Keyboard Quirks
Laptop keyboards differ somewhat from those of desktop computers, primarily because manufacturers have to cram all the keys onto a smaller form factor. They use the QWERTY format, but manufacturers make choices with key size and placement of the non-alphabet characters.

Almost every portable keyboard uses a Function (FN) key to enable some keys to perform an extra duty. You’ll either hold the FN key to access the extra function, or you’ll hold it to access the traditional function (the latter is more common with extra functions on the F1–F12 keys). On some systems, you can also configure this behavior. Figure 23-4 compares a laptop keyboard with a standard desktop keyboard. Note that the former has no separate number pad on the right and is a more compact layout.



Figure 23-4  Keyboard comparison

Pointing Devices
Portables need a way to control your mouse pointer, but their smaller size requires manufacturers to come up with clever solutions. Beyond the built-in solutions, portables usually have USB ports and can use every type of pointing device you’d see on a desktop. Early portables used trackballs, often plugged in like a mouse and clipped to the side of the case. Other models with trackballs placed them in front of the keyboard at the edge of the case nearest the user, or behind the keyboard at the edge nearest the screen.



NOTE   The FN key also enables you to toggle other features specific to a portable, such as GPS tracking or the keyboard backlight, to save battery life.

The next wave to hit the laptop market was IBM’s TrackPoint device, a joystick the size of a pencil eraser, situated in the center of the keyboard (see Figure 23-5). With the TrackPoint, you can move the pointer around without taking your fingers away from the “home” typing position. You use a forefinger to push the joystick around, and then click or right-click, using two buttons below the spacebar. This type of pointing device has since been licensed for use by other manufacturers, and while it continues to appear on some business-focused laptops today, it has primarily been replaced by our next link in the pointing device chain.



Figure 23-5  IBM TrackPoint

By far the most common laptop pointing device found today is the trackpad (see Figure 23-6)—a flat, touch-sensitive pad just in front of the keyboard. To operate a trackpad, you simply glide your finger across its surface to move the pointer and tap or press the surface once or twice to single- or double-click. You can also click by using buttons just below the pad on some older devices. Most people get the hang of this technique after just a few minutes of practice. The main advantage of the trackpad over previous laptop pointing devices is that it uses few moving parts—a fact that can really extend the life of a hard-working laptop.



Figure 23-6  Trackpad on a laptop



EXAM TIP   Use the Settings | Devices | Mouse dialog box or the Mouse applet in Control Panel for trackpad configuration. You can change sensitivity and much more in either tool.

Many manufacturers today include a multitouch trackpad that enables you to perform gestures, or actions with multiple fingers, such as scrolling up and down or swiping to another screen or desktop. The Multi-Touch trackpad on Apple’s laptops pioneered such great improvements to the laptop-pointing-device experience that the lack of a mouse is no longer a handicap on many laptops.



TIP   In the past it was common to accidentally “use” a trackpad with your palm while typing, so you may find some devices with a hardware switch or FN key combination for disabling the trackpad. More recent trackpads are usually capable of detecting and ignoring accidental input like this on their own.

Continuing the trend of mobile’s influence on more traditional portables, a number of laptops come equipped with a touch screen like you would find on a smartphone or tablet, again relying heavily on gestures to enable users to fluidly perform complex actions. In some cases these are otherwise very traditional laptops that happen to include a touch screen, but in other cases they are devices that are intended to be used as both a tablet and a laptop. Many of these touch screens are designed to take advantage of dedicated touch pens, also known as a stylus. These pens enable users to be more precise with their touch-screen interactions, hand write notes, draw, and keep the screen free of fingerprints. We’ll take a closer look at touch screens when we discuss mobile devices in Chapter 24.

Webcams and Microphones
The ability to communicate with others through real-time video is such a common expectation of mobile and portable devices these days that most of these devices (including laptops) come equipped with some sort of front-facing video camera—a webcam in the case of laptops—and one or more built-in microphones. A single microphone may be suitable for picking up the user’s voice, and additional microphones can help noise-cancellation routines improve the audio quality.

Even though most of us may just use the microphone in conjunction with the webcam, a growing number of programs support voice commands. Microsoft, for example, promotes its Cortana functionality built into Windows 10 (and optionally added to Windows 11). Any Windows 10 or 11 user on a system with a microphone, as long as they can live with letting Windows listen in on them, can perform voice searches and other actions from anywhere within earshot (mic-shot?) of their device.

The downside of these input devices becoming ubiquitous is the security risk they pose. It might be bad enough if a nefarious hacker or government agency (from any country) managed to get malware into my computer to see everything I click or type, but the risks are amplified if they can also hear and see anything going on near the device. It’s common enough for webcams to include a light that indicates when they’re recording, but built-in microphones don’t do the same. In some cases, vulnerabilities allow the recording indicator to be disabled anyway.

Display Types
Laptops come in a variety of sizes and at varying costs. One major contributor to the overall cost of a laptop is the size of the LCD screen. Most laptops offer a range between 10.1-inch to 17.3-inch screens (measured diagonally), while a few offer just over 20-inch screens.

In the past, 4:3 aspect ratio screens were common, but these days it’s hard to find one on anything but special-purpose or ruggedized laptops; almost all regular laptops come in one of two widescreen format ratios. Aspect ratio is the comparison of the screen width to the screen height, as you’ll recall from Chapter 17. While widescreens can have varying aspect ratios, almost all of the screens you find in present-day laptops will be 16:9 or 16:10.



EXAM TIP   Laptop LCDs are the same in almost every way as desktop LCDs with a TFT screen and a LED backlight (add an inverter and swap in a CCFL backlight for older laptops). You know all about these screens from Chapter 17. Expect questions about laptop displays but know that they’re pretty much the same as desktop displays. The only major difference is that the LCD frame contains an antenna, and may contain a camera and microphone, but we’ll discuss this later in the chapter.

Laptop screens typically come with one of two types of finish: matte or high-gloss. The matte finish was the industry standard for many years and offered a good trade-off between color richness and glare reduction. The better screens have a wide viewing angle and decent response time. The major drawback for matte-finished laptop screens is that they wash out a lot in bright light. Using such a laptop at an outdoor café, for example, can be very difficult without a bright enough display.

Manufacturers released high-gloss laptop screens more than a decade ago, and they rapidly took over many store shelves. The high-gloss finish offers sharper contrast, richer colors, and wider viewing angles when compared to the matte screens. The drawback to the high-gloss screens is that, contrary to what the manufacturers claim, they pick up lots of reflection from nearby objects, including the user! So, although they’re usable outside during the day, you’ll need to contend with increased reflection as well. Higher-end laptops include various anti-reflective solutions to mitigate this issue, with varying degrees of success.

With the advent of LED backlighting for LCD panels, many manufacturers have switched back to an anti-glare screen, though they’re not quite the matte screens of old. When the LED brightness is up high, these are lovely screens. (See the “Troubleshooting Portable Computers” section, later in this chapter, for issues specific to LED-backlit portables.)

As with other LCD technologies that you’ll recall from Chapter 17, most LCD/LED screens initially used twisted nematic (TN) technology. Most modern laptop screens use in-plane switching (IPS) panels for the greater viewing angle and better color quality. You’ll mostly find TN panels on older portables.



EXAM TIP   You may recall from Chapter 17 that there is another LCD panel type, vertical alignment (VA). While you’re very unlikely to encounter a VA panel on a laptop, it is possible and CompTIA may ask about one on the A+ 1101 exam. Just be aware that while they are uncommon for laptops, it isn’t impossible.

Organic light-emitting diode (OLED) displays are becoming more common on laptops (originally, due to their cost, they were limited primarily to large desktop monitors and TVs). OLED screens sip energy when compared to LCDs, and while less expensive and more common than they used to be, you’ll mostly find them on smartphones and tablets today. Chapter 24 discusses OLED screen technology.



EXAM TIP   The CompTIA A+ 1101 exam objectives may refer to OLED displays for laptops. Manufacturers were slow to incorporate OLED display technology in laptops, but OLED displays have gradually seen more adoption in recent years, particularly on higher-end devices. You may not see many in the wild yet, but know they exist for the exam!

Extending Portable Computers
In the dark ages of mobile computing, you had to shell out top dollar for any device that would operate unplugged, and what you purchased was what you got. Upgrade a laptop? Connect to external devices? You had few if any options, so you simply paid for a device that would be way behind the technology curve within a year and functionally obsolete within two.

Portable computers today offer a few ways to enhance their capabilities. Most feature external ports that enable you to add completely new functions, such as attaching a scanner, mobile printer, or both. You can take advantage of the latest wireless technology breakthrough simply by slipping a card into the appropriate slot on the laptop.

I’ll first describe single-function ports, and then turn to networking options. Next, I’ll cover card slots, and then finish with a discussion of general-purpose ports.

Single-Function Ports
All portable computers come with one or more single-function ports. You’d have a hard time finding a portable computing device that doesn’t have an audio jack, for example. Laptops often provide a video port for hooking up an external monitor, though wireless screen sharing and screencasting are gaining popularity as an alternative.



NOTE   Some laptop manufacturers, in a quest to make increasingly thinner and lighter devices, have moved away from including single-function ports like HDMI. Not only have they done away with most single-function ports, but they have also removed some common general-purpose ports like USB-A, in favor of a smaller number of USB-C or Thunderbolt ports. This port deficiency is often compensated for with a USB-C dongle, replacing on-board ports with optional expansion instead.

Ports work the same way on portable computers as they do on desktop models. You plug in a device to a particular port and, as long as the operating system has the proper drivers, you will have a functioning device when you boot.

Audio
Most portable computers have a 3.5-mm audio jack that is used for audio-out. This jack is quite often a combined headset jack that also supports microphone-in on the same three-ring plug. Older laptops might have a similarly sized microphone-in jack (see Figure 23-7), though built-in microphones are most common. You can plug in headphones, regular PC speakers, or even a nice surround sound setup to enable the laptop to play music just as well as a desktop computer can.



Figure 23-7  3.5-mm audio jacks

You can control the sound (both out and in) through the appropriate Settings app area or Control Panel applet in Windows, System Preferences in macOS, or some kind of switches on the laptop. The portable shown in Figure 23-8, for example, enables you to mute the speakers by pressing a special mute button above the keyboard. Other portables use a combination of the FN key and another key to toggle mute on and off, as well as to play, pause, fast-forward, and rewind audio (or any other media options). Most portables have volume up/down controls in the same location.



Figure 23-8  The mute button on a laptop

As Bluetooth wireless headphones have increased in popularity, some laptop manufacturers have excluded a dedicated 3.5-mm audio jack altogether. This isn’t a common or particularly popular move, but if you encounter a portable device with no dedicated audio jacks, don’t be surprised, because you heard about it here first.

Display
Most laptops support a second monitor via a digital port of some sort. There are many of these—you may find HDMI (including Mini-HDMI and Micro-HDMI) or DisplayPort (including USB Type-C and Thunderbolt); on ancient or special-purpose portables, there’s even a chance you may still find a VGA or DVI port. With a second monitor attached, you can duplicate your screen to the new monitor, or extend your desktop across both displays, letting you move windows between them. Not all portables can do all variations, but they’re more common than not.

Most portables use the FN key plus another key on the keyboard to cycle through display options. To engage the second monitor or to cycle through the modes, hold the FN key and press F8 (see Figure 23-9).



Figure 23-9  Laptop keyboard showing Function (FN) key that enables you to access additional key options, as on the F8 key



NOTE   Although many laptops use the Function key method to cycle the monitor selections, that’s not always the case. You might have to pop into Settings to do so. Just be assured that if the laptop has a video output port, you can cycle through monitor choices!

You can control what the external monitor shows by adjusting your operating system’s display settings. In Windows 10/11, this is all contained in the Display area of the Settings app. Open the Settings app and navigate to System | Display; from there scroll down till you find the Multiple displays section (see Figure 23-10). You’ll see a drop-down menu with several options. Extend these displays makes your desktop encompass both the laptop and the external monitor. Duplicate these displays places the same thing on both displays. You’d duplicate these displays for a presentation, for example, rather than for a workspace.



Figure 23-10  Multiple-display options menu in Windows 10

Near-Field Scanner
It isn’t really a port, but you’ll find some portable computers—especially ones designed for and marketed to business users—with a very thin slot the width of a credit card on one side or the other. No, it isn’t an expansion or memory card slot—it’s a smart card reader. If you’ve seen a credit or debit card with a little metallic chip (see Figure 23-11), you’ve seen a smart card. Smart card readers make use of a near-field scanner. While smart cards have tons of uses, what matters here is that you can log in to a portable device (if it has a built-in or USB smart card reader) using your smart card and a PIN number. We’ll go into a little more detail on the use of smart cards for authentication in Chapter 27.



Figure 23-11  Smart card

Networking Options
Rarely will you find a portable computer without at least one network connection option. Today’s portables come with some combination of 802.11, Bluetooth, and wired Ethernet connections. Generally they work exactly as you’ve seen in previous chapters, but you may stumble into a few issues that are unique to portables. (Mobile devices—tablets, smartphones—have even more options, as you’ll see in Chapter 24.)

802.11 Wireless
Most portables today have Wi-Fi built directly into the chipset for connecting the device to a wireless access point (WAP) and from there to a bigger network, such as the Internet. The 802.11n standard is common on older laptops; newer portable computers use 802.11ac (Wi-Fi 5) or 802.11ax (Wi-Fi 6).



NOTE   While the newest portables are shipping with 802.11ax, which is backward compatible with older standards, be aware that, especially as portables are getting powerful enough to live longer useful lives, you may see a few previous standards built into devices in the wild.

Bluetooth
802.11 isn’t the only wireless technology commonly found in portable devices. Nearly all modern portables use Bluetooth as well. Bluetooth is really handy on a laptop because, as you may recall from Chapter 20, it enables you to add wireless peripherals such as mice, keyboards, and headsets, as well as communicate with smartphones, speakers, and other Bluetooth devices.

Hardware Switches
Portable computers that come with wireless technologies such as 802.11, mobile broadband, GPS, or Bluetooth have some form of on/off switch to toggle the antenna off or on so that you may use the laptop in areas where emissions aren’t allowed (like a commercial aircraft, hence the term “airplane mode”). The switch may be hardwired on older devices, like the one shown in Figure 23-12, or if you’re using a more modern machine, will be a toggle of the FN key plus another key on the keyboard. Also, if you’re not using Wi-Fi or Bluetooth, turn them off to save some electricity and lengthen the portable’s battery life.



Figure 23-12  Wireless switch



EXAM TIP   Hardware switches or special Function key toggles enable you to switch features on and off, such as wireless networking, cellular networking, and Bluetooth. Toggle them off when in a scenario where battery life takes priority over networking.

Wired Ethernet
Some full-size laptops have an RJ45 wired Ethernet connection like the one shown in Figure 23-13. These work exactly like any other Ethernet jack—they have link lights and connect via UTP cable. Be aware, however, that wired Ethernet is one of the things many smaller contemporary laptops leave out.



Figure 23-13  Ethernet port on laptop

There are two issues with RJ45s on laptops. First, they do not have an on/off switch like the 802.11 and Bluetooth connections. You can turn them off just like you would turn off the NIC on a desktop: disable the NIC in Device Manager or turn the NIC off in BIOS. The other issue is the relative weakness of the physical connection. If you ever plug a laptop into a wired network and the OS doesn’t see a connection, check the RJ45 port.

Portable-Specific Expansion Slots
The makers of portable computers have developed methods for you to add features to a portable via specialized connections known generically as expansion slots. For many years, the Personal Computer Memory Card International Association (PCMCIA) established standards involving portable computers, especially when it came to expansion cards and slots. Once a common feature on laptops, these specialized expansion slots are almost impossible to find due to the dominance of USB. The last standard was called ExpressCard.

Storage Card Slots
Many portable computers offer one or more flash memory card slots to enable you to add storage to the portable. Particularly popular with photographers and videographers, these slots also enable the fast transfer of data from the card to the portable, and vice versa. They come in the standard varieties that you already know from Chapter 10, such as SD or microSD.

General-Purpose Ports
Portable computers rarely come with all of the hardware you want. Today’s laptops usually include at least USB-A or USB-C ports to give you the option to add more hardware. A few special-purpose laptops may still provide legacy general-purpose expansion ports (PS/2, RS-232 serial ports, eSATA, FireWire, and so on) for installing peripheral hardware, but these are increasingly less common. Most portables focus on more modern ports like USB-C or Thunderbolt. If you’re lucky, you will have a docking station or port replicator so you don’t have to plug in all of your peripheral devices one at a time.

USB and Thunderbolt
Universal serial bus (USB) and Thunderbolt enable users to connect a device while the computer is running—you won’t have to reboot the system to install a new peripheral. With USB and Thunderbolt, just plug in the device and go! Because portables don’t have a desktop’s multiple internal expansion capabilities, USB and Thunderbolt are some of the more popular methods for attaching peripherals to laptops and other portables (see Figure 23-14). Keeping with the trend toward fewer and more standardized general-purpose ports, many modern laptop manufacturers design their devices to charge using USB-C rather than the older AC adapters or more proprietary solutions.



Figure 23-14  Devices attached to USB on a portable PC

Docking Stations
Docking stations offer legacy and modern single- and multifunction ports (see Figure 23-15). The traditional docking station uses a proprietary connection, though the high speeds of USB 3.x and Thunderbolt 3 and 4 have made universal docks more common. A docking station makes an excellent companion to small portables with fewer ports.



Figure 23-15  Docking station

Port Replicators
A port replicator supplies one of the most critical aspects of docking stations, but in a smaller, more portable format: support for connectors that the laptop lacks. A modern USB Type-C port replicator, for example, will plug into a laptop’s USB-C port and offer an array of other port types, such as VGA, HDMI, USB Type-A (2, 3, 3.1), RJ45, and more. Port replicators work great with ultra-light, ultra-thin laptops to enhance the capabilities of the machine.

Smaller port replicators are also often referred to as dongles or USB-C dongles. Modern port replicators support something called pass-through charging, enabling the user to connect their charger to the port replicator. Be careful, because sometimes a port replicator won’t allow enough power through to the laptop, which can lead to slow charging, or even losing charge while plugged in.



EXAM TIP   Over time, the lines between docking station, port replicator, and dongle have blurred, and you’ll hear the terms used interchangeably in the IT world. Nonetheless, there are distinctions between docking stations and port replicators. A docking station is an external device that attaches to a mobile computer or other device, has a power connection, and allows connections to peripherals such as a keyboard and a mouse. It usually also includes slots for memory cards, optical disc drives, and other devices. Docking stations are perfect for professionals who need their work desk while traveling. A port replicator is an external device that provides connections to peripherals through ports. They are also perfect for travelers who just need to access email and communicate with others. Keep these differences in mind when you’re taking the CompTIA A+ exam.

USB Adapters
When you don’t need access to a number of ports at once, you can often find a USB adapter for whatever you need to connect. When it comes to drives or connectors that you need only occasionally, these adapters can enable you to use a much more portable device.

Two great examples of this are wired Ethernet and optical drives. I don’t know about you, but I haven’t spun up an optical disc in months, nor am I sure when I last opened my laptop within a few feet of a wired Ethernet connection. A USB to Ethernet (RJ45) dongle and a USB optical drive can provide these features when and where I need them, leaving me a much smaller laptop to carry the rest of the time.

Another good use for USB adapters is updating connectivity support for older devices. A USB to Wi-Fi dongle or a USB Bluetooth adapter can let me update an old laptop to 802.11ax, or add Bluetooth to a laptop that didn’t come with it built in.



EXAM TIP   The CompTIA A+ 1101 exam expects you to be familiar with USB to Ethernet adapters.

Managing and Maintaining Portable Computers
Most portables come from the factory fully assembled and configured. From a tech’s standpoint, your most common work on managing and maintaining portables involves taking care of the batteries and extending the battery life through proper power management, keeping the machine clean, and avoiding excessive heat.

Everything you normally do to maintain a computer applies to portable computers. You need to keep current on OS updates and use stable, recent drivers. Use appropriate tools to monitor the health of your storage drives and clean up unwanted files. That said, let’s look at issues specifically involving portables, with one caveat: because more compact or hybrid portables are often built like mobile devices, you may need to approach those devices by combining steps mentioned here with troubleshooting ideas from Chapter 25.

Batteries
Manufacturers over the years have used a few types of batteries for portable computers: Nickel-Cadmium (Ni-Cd), Nickel-Metal Hydride (Ni-MH), and Lithium-Ion (Li-Ion). Today, only Li-Ion is used because that battery chemistry provides the highest energy density for the weight and has few problems with external factors.

The Care and Feeding of Batteries
In general, keep in mind the following basics. First, always store batteries in a cool place. Although a freezer might seem like an excellent storage place, the moisture, extreme freezing cold, metal racks, and food make it a bad idea. Second, keep the battery charged, at least to 70–80 percent. Many modern laptops include optimized charging features that can prevent your battery from charging over a certain percentage while it’s plugged in, and in some cases, like with modern MacBooks, even learn your charging routine and adjust itself accordingly. Third, never drain a battery all the way down unless required to do so as part of a battery calibration (where you, in essence, reset the battery according to steps provided by the manufacturer). Rechargeable batteries have only a limited number of charge-discharge cycles before overall battery performance is reduced. Fourth, never handle a battery that has ruptured or broken; battery chemicals are very dangerous and flammable (check YouTube for videos of what happens when you puncture a Li-Ion battery). Finally, always recycle old batteries.

Try This!

Recycling Old Portable Device Batteries

Got an old portable device battery lying around? Well, you need to get rid of it, and there are some pretty toxic chemicals in that battery, so you can’t just throw it in the trash. Sooner or later, you’ll probably need to deal with such a battery, so try this!

1.   Do an online search to find the battery recycling center nearest to you. Electronics retailers are getting much better about accepting a wide array of e-waste, including batteries, though they may place quantity limits.

2.   Sometimes, you can take old laptop batteries to an auto parts store that disposes of old car batteries—I know it sounds odd, but it’s true! See if you can find one in your area that will do this.

3.   Many cities offer a hazardous materials disposal or recycling service. Check to see if and how your local government will help you dispose of your old batteries.

Power Management
Many different parts are included in the typical laptop, and each part uses power. The problem with early laptops was that every one of these parts used power continuously, whether or not the system needed the device at that time. For example, the hard drive continued to spin even when it was not being accessed, the CPU ran at full speed even when the system was doing light work, and the LCD panel continued to display even when the user walked away from the machine.

Over the years, a lot of work has gone into improving the battery life of portable devices. Beyond engineering better batteries and ever-more-efficient components, the system firmware and OS of most modern portables collaborate with the firmware of individual components to manage their power use. To reduce power use, the computer can power off unused components until they are needed, enter a low-power mode when the device isn’t in use, and throttle the performance of power-hungry components like the CPU to fit the current workload. This process of cooperation among the hardware, BIOS, and OS to reduce power use is known generically as power management.

Low-Power Modes
If you don’t know what’s going on under the hood, computers usually appear to be clearly off or on. In reality, most computers (both desktops and portables!) that appear to be off are using at least a little power, and may be in one of a few low-power modes. The CompTIA A+ 220-1102 exam focuses on configuring basic power options in the Windows Control Panel, but it’s good to have a handle on low-power modes in general.



NOTE   Low-power mode names can differ from OS to OS (and even from version to version), but the basic concepts are the same.

When the computer is off, turning it on will boot the OS from scratch. You can think of there being two kinds of true off mode:

•   Mechanical off mode The system and all components, with the exception of the real-time clock (RTC), are off.

•   Soft power-off mode The system is mostly off except for components necessary for the keyboard, LAN, or USB devices to wake the system.

Computers that appear to be off may actually be in a sleep (also called standby or suspend) mode: waking them will resume any programs, processes, and windows that were open when they entered the low-power mode. There are a number of fine-grained sleep modes, but the highlights are:

•   A device can wake quickly from normal sleep mode (sometimes called suspend to RAM) because it doesn’t power down the RAM, enabling the system to save its place. If the device loses power unexpectedly, it can lose whatever was in RAM.

•   Devices wake more slowly from a deeper sleep mode called hibernate (or suspend to disk) because they save everything in RAM to a hard drive or SSD (and restoring it all takes a moment) before powering down. On the up side, hibernation saves more power and won’t lose its place if the device loses power.

Configuring Power Options
You configure power options via the system setup utility or through the operating system. OS settings override CMOS settings. Implementations differ, but certain settings apply generally, like the ability to enable or disable power management; configure which devices can wake the system; configure what the power button does; and configure what the system should do when power is restored after an outage.

Operating systems tend to use friendly terms like Energy Options or Power Options, but you might run into some more technical terms in a system configuration utility. Many CMOS versions present settings to determine wake-up events, such as directing the system to monitor a modem or a NIC. You’ll see this feature as Wake on LAN, or something similar.

In Windows, power options can be found in the Settings | System | Power & sleep | in Windows 10/11 and the Control Panel applet Power Options. Windows offers power plans that enable better control over power use by customizing a Balanced, Power saver, or High performance power plan (see Figure 23-16).



Figure 23-16  Windows 10 Balanced, Power saver, and High performance power plan options



NOTE   While you can customize most laptops’ power plans to your heart’s content, on some models, such as Microsoft’s Surface Pro line, you are restricted to just the default Balanced plan.

You can customize a power plan for your laptop, for example, and configure it to turn off the display at a certain time interval while on battery versus plugged in or configure it to put the computer to sleep (see Figure 23-17). To see the specific power plans, click Additional power settings or go directly to the Control Panel Power Options applet. There you can tweak a lot more, including choices like hibernation (see Figure 23-18).



Figure 23-17  Customizing a laptop power plan in Windows 10



Figure 23-18  Windows 10 hibernation settings in the Power Options applet

Manual Control over Power Use
Most portables give you several manual options for reducing battery use in certain circumstances. We’ve already discussed using the on/off switch or keyboard combinations for disabling the Wi-Fi antenna or shutting off Bluetooth, but many modern portables borrow a feature from smartphones and tablets for disabling most or all of their wireless components at once: airplane mode. Beyond its intended use, airplane mode is also a great way to disable power-sucking components quickly. On the flipside, some newer gaming laptops include something known as a MUX switch, which enables a user to disable the computer’s integrated graphics in favor of the dedicated graphics card, which increases performance, but decreases battery life significantly.

Try This!

Adjusting Your System’s Power Management

Go into the Power Options applet on a Windows computer and look at the various settings. What is the current power plan for the computer? Check to see if it is running a Balanced or High performance power plan. If it is, change the power plan to Power saver and click Change plan settings. Familiarize yourself with some of the advanced power settings (click the Change advanced power settings link).

Try changing the individual settings for each power scheme. For instance, set a new value for the Turn off the display setting—try making your display turn off after five minutes. Don’t worry; you aren’t going to hurt anything if you fiddle with these settings.

Note that Microsoft changed power settings for laptops in Windows 10 to be Balanced. You can still adjust advanced power settings and tweak everything.

Laptops with backlit keyboards or RGB lighting will have some way you can disable this feature when it’s not needed, usually with a keyboard combination. You can also reduce the output of the LCD backlight using a combination of FN and another key to eke out a few more precious minutes of computing time before you have to shut down. Figure 23-19 shows a close-up of the FN-activated keys for adjusting screen brightness.



Figure 23-19  Keys for adjusting screen brightness

One of the best ways to conserve battery is to plan ahead for times when you’ll be unplugged. This can mean a lot of different things in practice, but they all boil down to thinking of ways to minimize the number of programs and hardware devices/radios you’ll need to use while your laptop is running on battery power. When I travel, for example, and know that I’m going to need a certain set of files stored on my file server at the office, I put those files on my laptop before I leave, while it’s still plugged into the AC. It’s tempting to throw the files on a thumb drive so I don’t have to break out my laptop at the office, or to let Dropbox do my syncing for me when I get to a Wi-Fi hotspot, but both USB and Wi-Fi use electricity.

Better than that, Windows enables me to designate the files and folders I need as offline files, storing a local, duplicate copy of the files and folders on my hard drive. When I connect my laptop to my office network, those offline files are automatically synced with the files and folders on the file server. Anything I changed on the laptop gets written to the server. Anything anyone changed in those folders on the server gets written to my laptop. If changes were made on both sides, a sync conflict pops up automatically, enabling me to resolve problems without fear of overwriting anything important.

To designate a folder and its contents as offline files, right-click the folder you want and select Always available offline from the context menu. The sync will occur and you’re done. When you want to open the files offline, go to the Control Panel and open the Sync Center applet (see Figure 23-20). Click the Manage offline files link to open the Offline Files dialog box (see Figure 23-21). Click the View your offline files button and you’re in.



Figure 23-20  Sync Center applet



Figure 23-21  Offline Files dialog box



EXAM TIP   Another option for extending battery life is to bring a spare battery. While most modern laptops don’t have easily swappable batteries, larger power banks enable you to charge your laptop on the go, much like you’d do with your smartphone.

Cleaning
Most portable computers take substantially more abuse than a corresponding desktop model. Constant handling, travel, airport food on the run, and so on can radically shorten the life of a portable if you don’t take action. One of the most important things you should do is clean the device regularly. Use an appropriate screen cleaner (not a glass cleaner!) to remove fingerprints and dust from the fragile LCD panel. (Refer to Chapter 17 for specifics.) Using a dedicated screen cleaner is important, otherwise you run the risk of doing permanent damage to the display.

We’ll go into greater detail on environmental threats in Chapter 27, but if you’ve had the portable in a smoky or dusty environment where air quality alone can cause problems, try cleaning it with compressed air. Compressed air works great for blowing out dust and crumbs from the keyboard and for keeping any ports, slots, and sockets clear. Don’t use water on your keyboard! Even a little moisture inside the portable can toast a component.

Heat
To manage and maintain a healthy portable computer, you need to deal with heat issues. Every portable has a stack of electronic components crammed into a very small space. Unlike their desktop brethren, portables don’t have lots of freely moving air space that enables fans to cool everything down. Even with lots of low-power-consumption devices inside, portable computers crank out a good deal of heat. Excessive heat can cause system lockups and hardware failures, so you should handle the issue wisely.

The following steps have more traditional portables in mind; very compact portables are usually designed to handle heat more like mobile devices; in some cases, such as the newer MacBook Air, this is even accomplished without fans. Chapter 25 will approach heat issues with mobile device construction in mind. For more traditional portables, try this as a starter guide:

•   Use power management, even if you’re plugged into the AC outlet. This is especially important if you’re working in a warm (more than 80 degrees Fahrenheit) room.

•   Keep air space between the bottom of the laptop and the surface on which it rests. Putting a laptop on a soft surface, such as a pillow on your lap, creates a great heat-retention system—not a good thing! Always use a hard, flat surface.

•   Don’t use a keyboard protector for extended amounts of time.

•   Listen to your fan, assuming the laptop has one. If it’s often running very fast—you can tell by the whirring sound—examine your power management settings, environment, and running programs so you can change whatever is causing heat retention.

•   Speaking of fans, be alert to a fan that suddenly goes silent. Fans do fail on laptops, causing overheating and failure.

Protecting the Machine
Even midrange laptops can be pricey, and replacing them before you’re ready is always a pain. To protect your investment, you’ll want to adhere to certain best practices. You’ve already read tips in this chapter to deal with cleaning and heat, so let’s look at the “portable” part of portable computers.

Tripping
Pay attention to where you run the power cord when you plug in a laptop. One of the primary causes of laptop destruction is people tripping over the power cord and knocking the laptop off of a desk. This is especially true if you plug in at a public place such as a café or airport. Remember, the life you save could be your portable’s!

Storage
If you aren’t going to use your portable for a while, storing it safely will go a long way toward keeping it operable when you do power it up again. A quality case is worth the extra few dollars—preferably one with ample padding. Not only will this protect your system on a daily basis when transporting it from home to office, but it will keep dust and pet hair away as well. Also, protect from battery leakage, at least on devices with removable batteries, by removing the battery if you plan to store the device for an extended time. Regardless of whether the battery is removable or built in, it’s a good idea to store the battery partially charged and top it up occasionally to keep it from fully discharging.

Travel
If you travel with a laptop, guard against theft. If possible, use a case that doesn’t look like a computer case. A well-padded backpack makes a great travel bag for a laptop and appears less tempting to would-be thieves, though some brands and styles of these are still quite obvious. Smaller portables can often hide in less obvious bags. Don’t forget to pack any accessories you might need, like modular devices, power banks, and AC adapters. Most importantly—back up any important data before you leave!

Make sure to have at least a little battery power available. Heightened security at airports means you might have to power on your system to prove it’s really a computer and not a transport case for questionable materials. And never let your laptop out of your sight. If going through an x-ray machine, request a manual search. The x-ray won’t harm your computer like a metal detector would, but if the laptop gets through the line at security before you do, someone else might walk away with it. If flying, stow your laptop under the seat in front of you where you can keep an eye on it.

If you travel to a foreign country, be very careful about the electricity. North America uses ~115-V power outlets, but most of the world uses ~230-V outlets. Most portable computers have auto-switching power supplies, meaning they detect the voltage at the outlet and adjust accordingly (but most people just call it a charger). An auto-switching power supply will have an input voltage range printed on it somewhere (see Figure 23-22).



Figure 23-22  Input and output voltages on laptop power brick

Double-check the charger to make sure its supported range covers voltages used in any country you plan to visit. If it doesn’t, you may need a full-blown electricity-converting device, either a step-down or step-up transformer. You should be able to find converters and transformers at electronics retailers, travel stores, and, of course, online.

Shipping
Much of the storage and travel advice can be applied to shipping. If possible, remove batteries and optical discs from their drives. Pack the portable well and disguise the container as best you can. Back up any data and verify the warranty coverage. Ship with a reputable carrier and always request a tracking number and, if possible, delivery signature. It’s also worth the extra couple of bucks to pay for the shipping insurance. And when the clerk asks what’s in the box, it’s safer to say “electronics” rather than “a new 17-inch laptop computer.”

Security
The fact is, if someone really wants to steal your laptop, they’ll find a way. While we cover securing devices against physical theft in Chapter 27, there are some things you can do to make yourself, and your portable devices, less desirable targets. As you’ve already learned, disguise is a good idea.

Another physical deterrent is a laptop lock. Not all laptops are able to use one, but they can be helpful if the option is available for your device. Similar to a steel bicycle cable, there is a loop on one end and a lock on the other. The idea is to loop the cable around a solid object, such as a bed frame, and secure the lock to the small security hole on the side of the laptop (see Figure 23-23). Again, if someone really wants to steal your computer, they’ll find a way. They’ll dismantle the bed frame if they’re desperate. The best protection is to be vigilant and not let the computer out of your sight.



Figure 23-23  Cable lock

An alternative to securing a laptop with a physical lock is to use a software tracking system that makes use of GPS. It won’t keep your device from being taken, but tracking software can use the many sensors and networking capabilities of modern devices to help recover them. While functionality differs by application, common features include seeing the location of the stolen computer, capturing images or audio with its sensors, and wiping sensitive files from the device. Because this functionality is more common in mobile devices, we’ll save the details for Chapter 25.

Theft isn’t the only security risk that laptop owners face; modern laptops account for the need to protect user privacy and data as well. Screen locks have been around for a long time, requiring a user to enter a PIN or password before being able to actually use the device. In recent years, these features have been enhanced using biometrics. Biometrics are measurements of physical characteristics that are documented and verified through the use of scanners. Biometrics can be used to match a physical characteristic of a user with a valid user account in order to authenticate the user. Common biometric security features found on laptops include fingerprint scanners located on the keyboard or facial recognition software that uses the device’s webcam. These are popular because they allow a user to quickly access their device without needing to enter a complex password every time they open the lid or come back from a lunch break.

Upgrading and Repairing Laptop Computers
A competent tech can upgrade and repair portable computers to a degree, though true laptop techs are specialists. Over the years, laptops have become more and more based on proprietary parts, to a point where some laptops can only really be repaired by the manufacturer or authorized third parties, and in some cases, upgrades are off the table altogether. Upgrading the basics usually means breaking out the trusty screwdriver and avoiding electrostatic discharge (ESD). Repairing portables successfully, on the other hand, requires research, patience, organization, special tools, and documentation. Plus, you need a ridiculously steady hand. This section provides an overview of the upgrade and repair process. Keep in mind that the growing number of form factors and the shrinking size of portable devices mean there are many exceptions, especially for very compact portables; these devices may be trickier to take apart, and components may be soldered on or use less-common interfaces.

Disassembly Process
Disassembling a portable PC is usually pretty easy, if it was designed to be upgraded or serviced by casual users. Putting it back together in working condition is the hard part! You need to follow a four-step process to succeed in disassembly/reassembly.



NOTE   Many modern laptops are designed with portability in mind over repairability and, as a result, are not easily repairable without access to proprietary tools or parts. In laptops like this, even components like RAM or an SSD may be soldered onto the motherboard. Nonetheless, knowing your way around the inside of a laptop is a great skill as a tech.

First, document and label every cable and screw location. Laptops don’t use standard connectors or screws. Often you’ll run into many tiny screws of varying threads. If you try to put a screw into the wrong hole, you could end up stripping the screw, stripping the hole, or getting the screw wedged into the wrong place.

Second, organize any parts you extract from the laptop. Seriously, put a big white piece of construction paper on your work surface, lay each extracted piece out in logical fashion, and clearly mark where each component connects and what it connects to as well. You may even want to use a smartphone camera to take pictures or a webcam to record your workspace in case something goes missing.

Third, refer to the manufacturer’s resources. I can’t stress this point enough. Unlike desktops, portables have no standardization of internal structure. Everything in the portable is designed according to the manufacturer’s best engineering efforts. Two portables from the same manufacturer might have a similar layout inside, but it’s far more likely that every model differs a lot.

Finally, you need to use the appropriate hand tools. A portable, especially on the inside, will have a remarkable variety of tiny screws that you can’t remove/reinsert without tiny-headed Phillips or Torx drivers. You’ll need tiny pry bars—metal and plastic—to open components. Figure 23-24 shows an entry-level toolkit for a laptop tech that you can order from iFixit (https://www.ifixit.com; more on this site in a moment). Their professional toolkit version has 70 tools, plus there’s an expansion kit! Like I said at the beginning of this section, portable techs are specialists.



Figure 23-24  Bare-minimum laptop repair tools

Now that you have the official line on the disassembly process, let’s get one thing clear: a lot of manufacturers don’t provide access to their resources to just any tech, but only to authorized repair centers. So what do you do when faced with an unfamiliar laptop that a client brought in for repair?

You have essentially two options. First, you can find a dedicated laptop tech and refer your client to that person. If the problem is exceptionally complicated and the portable in question is mission critical, that’s often the best option. If you want to tackle the problem or it looks like something you should be able to do, then you go to third-party sources: YouTube and iFixit.

Every portable computer has a specific make and model. Open up a Web browser and go to YouTube. Type in precisely what you want to do, such as “Dell XPS 13 keyboard replacement,” and see what pops up (see Figure 23-25). You’ll most likely get results back, especially if the laptop in question is a couple of years old. People all over the world have to deal with broken devices, so you’re not alone.



Figure 23-25  YouTube search result

Once you’ve found the appropriate video or something that’s close enough to enable the repair attempt, watch it. If it’s too difficult for your skill level or requires a set of expensive tools, then fall back to step one and go find a dedicated tech. Otherwise, figure out what tools and parts you need. Parts specific to a laptop (as in that Dell keyboard in the preceding example) will need to be purchased from the manufacturer. More generic parts, like hard drives, CPUs, and so on can be purchased from Newegg (my favorite tech store) or some other online retailer.

For general tools, parts, and a lot of very detailed step-by-step instructions, I highly recommend iFixit. Billed as “Repair guides for everything, written by everyone,” iFixit is built by techs like you and me who conquer a problem, document the steps, and post the details (see Figure 23-26). This means the next tech along who runs into the same problem doesn’t have to reinvent the wheel. Just go to iFixit.com. The proceeds from parts and tools they sell, by the way, go toward supporting the site.



Figure 23-26  Some of the Dell laptop repair walkthroughs at iFixit.com

Standard Upgrades
Every CompTIA A+ tech should know how to perform the two standard upgrades to portable computers: adding RAM and replacing a hard drive. Let’s go through the steps.

Upgrading RAM
Not every modern laptop has the option to upgrade RAM, but there are still plenty that do. As a result, one of the more common laptop upgrades you’ll be called on to do is to add more RAM. A quick Google search of the make and model that you’re working on will tell you whether or not the RAM is soldered or replaceable. If it’s replaceable, you’ll need to make sure you know what kind you need.



EXAM TIP   Expect a question or two on the CompTIA A+ 1101 exam about scenarios where you should install (and configure) laptop memory—as in random access memory (i.e., RAM). Adding RAM or replacing existing sticks with more RAM can dramatically improve performance.

How to Add or Replace RAM  Upgrading the RAM in a laptop requires a couple of steps. Once you’ve determined that the specific device you’re working on can be upgraded, you need to get the correct RAM. Refer to the manufacturer’s Web site or to the manual (if any) that came with the laptop for the specific RAM needed. Once you know the type, you need to make sure you know the configuration of any existing RAM in the system. If you are planning to upgrade from 8 GB to 16 GB, you need to know if your portable already has one module at 8 GB or two modules at 4 GB.

Second, every portable offers a unique challenge to the tech who wants to upgrade the RAM, because there’s no standard location for RAM placement in portables. The RAM slots may not even be in the same spot. More often than not, you need to unscrew or pop open a panel on the underside of the portable or remove the entire back plate (see Figure 23-27). Then you press out on the restraining clips and the RAM stick pops up (see Figure 23-28). Gently remove the old stick of RAM and insert the new one by reversing the steps.



Figure 23-27  Removing the back plate



Figure 23-28  Releasing the RAM

Always remove all electrical power from the laptop before removing or inserting memory. Disconnect the AC cord from the wall outlet. Take out any removable batteries! Failure to disconnect from power can result in a fried laptop. In the case of systems with built-in batteries, consult the manufacturer’s resources to evaluate the safety of working on the system and any additional steps or precautions you should take.

Upgrading Mass Storage
You can replace a hard disk drive (HDD) or solid-state drive (SSD) in some laptops fairly easily, while others (like MacBooks) cannot be upgraded at all. Contemporary laptops with upgradeable storage make use of the small M.2 form factor in order to save space, although a fair number of systems, particularly older ones, will also use 2.5-inch SATA drives. Using smaller form-factor drives enables manufacturers to include a second slot for easy mass storage expansion.

mSATA and M.2  If you have a newer portable, chances are the computer uses one of the smaller SSD formats—mSATA or M.2. You read about them in detail back in Chapter 8, but glance back to refresh your memory if necessary.

Most manufacturers make it fairly easy to replace or upgrade an mSATA or M.2 drive. Remove the bottom plate or dedicated drive bay covering from the computer. Remove the tiny retaining screw and pop the old drive out. Put the new drive in its place, insert the retaining screw, and reattach the covering. You’re good to go, at least from the hardware side of things.

One of the best upgrades you can make on a laptop is to migrate from an HDD to an SSD. You may get less storage capacity for the money, but the trade-offs are worth it. Beyond improved reliability, the SSD will use a lot less electricity than an HDD, thus extending battery life. Additionally, any SSD is rip-roaringly faster than an HDD and performance across the board will be boosted. An upgrade from an HDD to an SSD can breathe new life into an otherwise sluggish older system.

The process of replacing a hard drive mirrors that of replacing RAM. You find the hard drive hatch—either along one edge or in a compartment on the underside of the computer—and release the screws. If the device doesn’t have a hatch, you may need to remove the bottom of the chassis (as previously shown in Figure 23-27). Remove the old drive and then slide the new drive into its place (see Figure 23-29). Reattach the hatch or cover and boot the computer. If you’re replacing your boot drive, grab a bootable USB flash drive and prepare to reinstall.



Figure 23-29  Inserting a replacement drive

Hardware/Device Replacement
Once you get beyond upgrading RAM and replacing a hard drive on a portable, you take the plunge into the laptop-repair specialty. You can replace some components by lifting them out, detaching a ribbon cable, and then reversing the steps with the replacement part. Other parts require a full teardown of the laptop to the bare bones, which presents a much greater magnitude of difficulty. Because every portable differs, this section provides guidance, but not concrete steps, for replacement. Be aware, as mentioned earlier, that many systems are trending toward more integrated parts; make sure the part you’re replacing is actually replaceable in the specific system you’re working on.

Components
Replaceable components require more work than the RAM or drive upgrades, but replacing them generally falls into the category of “doable.” What I call components are the battery, keyboard, internal speaker(s), and expansion cards.

Battery  If a battery’s performance falls below an acceptable level, you can replace it with a battery from the manufacturer or from an aftermarket vendor. Although this should be a simple swap replacement (and usually is, at least if the battery isn’t built in), you might encounter a situation where the real problem wasn’t the battery per se, but an inadequate or malfunctioning charging system. The new battery might not give you any better performance than the old one. Try it.

Keyboard  Getting a keyboard off a laptop computer often requires little pry bars, but also look for screws, clips, and so on. Keyboards connect via a tiny, short, and very delicate cable, often held down by tape. Replacing one is tricky, but doable in many cases. Look up steps for detaching and reattaching keys on a specific device if possible, and otherwise find generic instructions for the clip type before proceeding.

Speaker  Replacing the internal speaker or speakers on a laptop will most likely require you to open up the device. Most laptop speakers are inside the chassis, so if you want to replace them, you need to dismantle the portable to get to them. (See the upcoming “Integral Parts” section.)

Wireless and Expansion Cards  Many portables have one or more true expansion slots for add-on cards. The more modular varieties will have a hatch on the bottom of the case that opens like the hatch that gives you access to the RAM slot(s). This enables you to change out an older wireless cards (alternative names Wi-Fi card and WLAN card), for example, with one that support current Wi-Fi card standards, thus greatly enhancing the Wi-Fi experience on this device. Similarly, you could change out a Bluetooth module for an upgraded version. Figure 23-30 shows a wide-open laptop with the expansion slot exposed for the insertion of a WLAN card.



Figure 23-30  M.2 expansion slot on laptop with WLAN card

Just like when installing RAM in a portable, you must avoid ESD and remove all electricity before you take out or put in an expansion card. Failure to remove the battery and the AC adapter (or follow any extra steps and precautions in the manufacturer’s resources if the battery is built in) can and probably will result in a shorted-out laptop motherboard, and that just makes for a bad day.



NOTE   Check with the portable manufacturer to get a Wi-Fi card that’s compatible with the portable. Just because a card will fit in the slot does not, in this case, mean it will work.

The only other consideration with expansion cards applies specifically to wireless. Not only will you need to connect the card to the slot properly, but you must reattach the antenna connection and often a separate power cable. Pay attention when you remove the card as to the placement of these vital connections.

You’ll find one of two types of expansion slots in a portable: Mini-PCIe and M.2. The older ones (think 2013 and earlier) use Mini-PCIe and are uncommon to see today, while newer devices use M.2.

Display and Its Components  A laptop screen presents unique challenges when faced with a replacement scenario. The display has the typical parts you’d expect in an LCD, such as the panel, backlight(s), and inverter (on older portables); plus, the display typically has other components along for the ride, such as the Wi-Fi antenna, a webcam, and a microphone. Finally, a touch-screen display offers even more of a challenge.



NOTE   For a deeper dive on the type of display technologies that exist, refer back to Chapter 17. Laptops typically make use of the same technologies that desktop monitors use, just in smaller sizes.

The process for replacing the screen (flat, touch screen, digitizer), inverter, Wi-Fi antenna, webcam, or microphone follows the same steps. You pry the plastic frame off the display, most commonly using a spudger or other tool from your toolkit, then remove any exposed screws. The screen will lift out, and you’ll need to detach the internal parts. I can’t give you precise details, because every model differs, but the parts are usually secured with tiny screws or compression, or mild adhesive. Plus, you’ll need to gently disconnect data cables for each component. If you’re just replacing a defective webcam or microphone, you won’t need to disconnect other parts (most likely), but if you need to replace the screen or inverter, you’ll have to remove everything.

Take pictures with your phone. Keep track of which connectors go where. Don’t rush the process when dealing with so many tiny connectors and parts. Document the locations and types of screws. The extra work you do to record each step or layer will pay off with a properly repaired laptop. Trust me!



EXAM TIP   Expect a question or two on the CompTIA A+ 1101 exam on a typical scenario where replacement of the screen or components within the display needs to happen. These are obvious—cracked screen, failure of the digitizer/touch screen, Wi-Fi antenna malfunction, and so on. (Note that the specific objective language on the antenna is WiFi antenna connector/placement, which refers to the wireless antenna wires—yes, that’s an oxymoron—that run along the top and sides of the display and connect with a tiny ribbon cable.) While you don’t need to know the steps of the repair process for the exam, you need to at least be able to understand the differences between display components and troubleshoot issues that they may have.

Integral Parts
Some hardware replacements require you to get serious with the laptop, opening it fully to the outside, removing many delicate parts, and even stripping it down to the bare chassis. I leave these repairs to the professional laptop repair folks, simply because they have the specific tools and expertise to do the job efficiently. To understand the process, I’ve outlined it here. This pertains to three components: DC jack, trackpad, and system board.



NOTE   While a few laptops used to have removable/replaceable video cards, these were few and far between and you are very unlikely to encounter them in the wild. Modern devices have the GPU as part of the system board.

Portables generally open in two different ways, depending on the manufacturer. You either peel away layers from the top down, through the keyboard, or from the bottom up, through the base. Either direction requires careful attention to detail, part connectivity, and locations. You’ll need a system to keep track of the dozens of tiny screws.

Every one of the replacements here requires you to detach the screen from the main chassis of the portable. Aside from finding the connection points and removing the proper screws, you need to pay attention to the connection points for the data stream to the monitor and the antenna that’s in the frame of the display, as mentioned earlier.

Once you have the portable stripped down, you replace whichever component you’re in there to replace and then begin the process of building it back up into a coherent unit. Pay incredibly careful attention to getting data cables connected properly as you rebuild. I can’t imagine a worse tech experience than replacing a trackpad and rebuilding a laptop only to have missed a connection and having to do it all over again.



EXAM TIP   The DC jack requires extra-special love when you need to replace one. The part is soldered to the main board, so replacing it means you’ll need to not only strip the laptop to the bare metal, but also unsolder the old part and solder the new part. Then you’ll rebuild the laptop and hope you got everything right. CompTIA cannot expect a CompTIA A+ technician to know how to do this stuff. Expect a question that explores whether it can be done. Rest assured, specialized techs can replace any component on a laptop, even the DC jack.

Troubleshooting Portable Computers
Many of the troubleshooting techniques you learned about for desktop systems can be applied to laptops. For example, take the proper precautions before and during disassembly. Use the proper hand tools, and document, label, and organize each plastic part and screw location for reassembly. Additionally, here are some laptop-specific procedures to try.

Power and Performance
Some of the most common portable device issues relate to how well they do (or don’t!) run—so let’s take a look at a few issues related to power, performance, and heat.

Laptop Won’t Power On
•   If a laptop won’t power up—a no power scenario—verify AC power by plugging another electronic device into the wall outlet. If the other device receives power, the outlet is good.

•   If the outlet is good, connect the laptop to the wall outlet and try to power on. If no LEDs light up, you may have a bad AC adapter. Swap it out with a known-good power adapter.

•   A faulty peripheral device might keep the laptop from powering up. Remove any peripherals such as USB or Thunderbolt devices.

Poor Performance
•   The most common reason for slow performance is that a running application or process is consuming high resources. All operating systems have a utility to check this—such as the Task Manager in Windows or Activity Monitor in macOS—and look into any problems it finds. The application or process may need to be closed or stopped, you may need to reboot, or the application may need an update.

•   Extreme performance issues may lead to a frozen system. If they don’t resolve on their own and you can’t interact with the device, you may need to perform a hard reboot (which may result in the loss of any unsaved work). Usually, holding down the power button for 10 seconds is sufficient, though you may need to check the manufacturer’s resources for the proper procedure. If the battery is removable, you may be able to reboot the device by pulling the battery out and replacing it.



NOTE   Be aware, that you might find official or third-party resources discussing hard and soft resets. These are not the same as hard and soft reboots, so you should pay careful attention to the instructions and make sure you’re performing the correct procedure. See Chapter 25 for more on hard and soft resets.

Battery Issues
•   A swollen battery will probably go unnoticed at first, and the symptoms it creates may be hard to identify if you aren’t aware it can happen. The cause is usually over-charging, perhaps due to a failure in the circuits that should prevent it, but the early symptoms might be a laptop that doesn’t quite sit right on flat surfaces, a screen that doesn’t fit flush when closed, problems with input devices like the trackpad or keyboard, and trouble removing or inserting a removable battery. Eventually, the device’s case may be obviously deformed. While battery packs are designed to handle a little swelling, it increases the risk they’ll puncture—and a punctured battery can be dangerous. Don’t ignore these symptoms; open the case carefully to check the battery, and very carefully deliver it to an e-waste recycling or disposal site.

•   If you have a laptop with a battery that won’t charge up—a poor battery health problem—it could be one of three things: The device has a setting that limits how much charge the battery can hold to preserve its lifespan, the battery might be cooked, or the AC adapter isn’t doing its job, also known as improper charging. To troubleshoot, first go to the devices battery settings and look to see if there is a charge limiting setting. If there isn’t, you can try removing the battery and run the laptop on AC power only. If it works, you know the AC adapter is good. If it doesn’t work, you probably need to replace the adapter. Another option is to replace the battery with a known-good battery. If the new battery works, you’ve found the problem. Just replace the battery.

•   The reasons for very short battery life in a battery that charges properly are fairly benign. The battery has usually outlived its useful life and needs to be replaced, or some programs or hardware are drawing much more power than usual. Check wireless devices you usually keep disabled to make sure they aren’t on. Follow recommendations in the preceding “Poor Performance” section to address problem programs.

Overheating
•   Because overheating can be both a symptom and a cause of a variety of issues, you should be alert to any device that is running hotter than usual. Note which parts of the device are hot—this can give you important clues. If the device feels dangerously hot, err on the side of protecting the device from heat damage instead of trying to diagnose the cause. Power the device down and remove the battery if possible. Set it on a cool, hard surface, out of direct sunlight, with the hottest part of the device exposed to air if possible.

•   Likewise, look for possible signs a device is overheating—like inconsistent reboots, graphical glitches, system beeps—and rule out heat issues.

•   Listen for fans. While some portables don’t have any, complete silence may indicate a failed fan, and unusual noise may signal one on its way out. Before you open the device to check the fans, make sure that the device isn’t set to some type of silent mode. Many modern laptops include software that allows you to run the laptop quietly or silently when not doing resource-intensive tasks. If this setting is active, it may be the reason for the lack of fan noise.

•   Dust build-up in the laptop can lead to major overheating issues over time. If a computer is having overheating issues, it’s very possible that there is dust, pet hair, or residue from smoke gumming up the works. To fix this, you should first check the fan vents for obstructions, grab your ESD wrist strap, then open the laptop and disconnect the battery. Once this is done, use a can of compressed air to blow the dust out of the chassis using short bursts from different angles. Be careful, laptop fans can be fragile, so don’t be too aggressive when you clean them.

•   Know when to expect a hot device. Busy or charging devices can create a lot of heat; follow the steps mentioned in the preceding “Poor Performance” and “Battery Issues” sections for identifying components that shouldn’t be on, especially if they are hot to the touch, and finding runaway programs. If the device is charging, unplug it and see if the device cools. If you find nothing unexpected and the device is unusually hot, it may have an airflow problem.

•   If the entire device is hot, it may have simply been left in direct sunlight or a hot environment. Cool the device down and see if the trouble goes away.

Components
Various hardware components can encounter issues, including the display, wireless networking, audio, and input devices.

Display Problems
•   If the laptop is booting (you hear the beeps and the drives) but the screen doesn’t come on properly—a no display problem—first, make sure the display is turned on. Press the FN key and the key to activate the screen a few times until the laptop display comes on. If the device is a 2-in-1 with a removable screen, make sure it is properly attached and that it is receiving power.

•   If the laptop display is very dim—a dim display problem—it may be as simple as adjusting the brightness settings. Most laptops allow you to do this by using the FN key and the key to adjust the brightness. If this doesn’t work, it may also be due to some power saving setting. Check the power saving settings to see if the screen brightness is being limited there. If those options don’t fix the problem, you may be dealing with a failing backlight. This can be caused by failed inverters on older laptops.

•   If the screen won’t come on or is cracked, most laptops have a port for plugging in an external monitor, which you can use to log in to your laptop.

•   If you plug a laptop into an external monitor and that monitor does not display, remember that you have both a hardware and an OS component to making dual displays successful. There’s usually a combination of FN and another key to toggle among only portable, only external, and both displays. Plus, you have the Display area of Settings or the Display in the Control Panel to mirror or extend the desktop to a second monitor.

•   If you have a flickering display, you should check for software issues before you try to open the laptop chassis. Laptop displays can flicker because of bad device drivers or application issues just like desktop displays. Unlike desktop displays, laptops are more likely to be dropped or accidentally knocked off a table. This can loosen connectors inside the display and lead to flickering as well. If software isn’t the problem, loose connections just might be.

•   If the screen orientation on a Windows portable doesn’t change when the device is rotated, auto-rotation may be disabled. Likewise, if the orientation changes at the wrong time, you can lock rotation in Settings, or via the Display in the Control Panel. If the rotation needs to remain locked, you can still change the orientation via Settings/Display, or possibly with FN key combinations.

Wireless Devices (Bluetooth, Wi-Fi, NFC, or GPS) Don’t Work or Work Intermittently
•   If the wireless doesn’t work at all, check along the front, rear, or side edges of the laptop for a physical switch that toggles the internal wireless adapter, Bluetooth adapter, or airplane mode on and off. Also check your notification area for an airplane icon.



EXAM TIP   Expect a couple of questions on the CompTIA A+ 1101 exam that explore poor/no connectivity scenarios where a client experiences issues with wireless connectivity or Bluetooth connectivity issues.

•   If a tech has recently replaced a component that required removal of the laptop display, dead wireless could mean simply a disconnected antenna. Most portables have the antenna built into the display panel, so check that connection.

•   Try the special key combination for your laptop to toggle the wireless or Bluetooth adapter, or one for toggling airplane mode. You usually press the FN key in combination with another key.

•   You might simply be out of range or, if the wireless works intermittently, right at the edge of the range. Physically walk the laptop over to the wireless router or access point to ensure there are no out-of-range issues. You might also be experiencing congestion, too many wireless devices operating in the same frequency range.

•   With Bluetooth specifically, remember that the pairing process takes action or configuration on both devices to succeed. Turn on the Bluetooth device, actively seek it, and try again.

•   If only the GPS is not functioning, privacy options may be preventing applications from accessing your GPS location information. Check the Control Panel or the Privacy section of the Settings app to see whether the GPS device is enabled, and if location services are enabled both system-wide and for the appropriate applications. Check System Preferences in macOS or a similar location in Linux for the same options.

•   While we won’t discuss Near Field Communication (NFC) in depth until Chapter 24, some portable computers may have NFC support; if NFC isn’t functioning, you may need to enable a setting to enable communication with nearby devices. In Windows, open the Proximity applet in the Control Panel (only present if you have NFC hardware) and make sure Proximity support is enabled.

Audio Problems
•   If audio isn’t working when it should be, check for a hardware mute or volume button or switch and verify through the notification area Volume icon that the audio output isn’t muted. Verify proper output device configuration through the operating system, and verify the application is using the right output device.

•   If no sound is coming from the device speakers, try plugging in a pair of headphones or some external speakers. If these work fine, there’s a chance the built-in speakers have been damaged. Depending on their location, it can be easy to get them wet.

•   If the device has had repairs or upgrades lately, make sure the speakers are properly connected.

•   If headphones work fine with the device, the speakers may need replacing. First, make sure the device has been rebooted, double-check the audio output device settings, try changing and resetting the default output device, and try disabling and re-enabling the appropriate device.

Input Problems
•   Before assuming an input problem is hardware related, confirm that the system is otherwise running smoothly. Input devices may appear not to work or work erratically if the system is freezing up. Refer to the earlier “Power and Performance” section for troubleshooting a frozen system.

•   If none of the keys work on your laptop, there’s a good chance you’ve unseated the keypad connector. These connectors are quite fragile and are prone to unseating from any physical stress on the laptop. Check the manufacturer’s disassembly procedures to locate and reseat the keypad.

•   If you’re getting numbers when you’re expecting to get letters, the number lock (NUM LOCK) function key is turned on. Turn it off. Pay attention to the NUM LOCK indicator lights, if any, on a portable if you experience these sorts of problems.

•   Laptop keyboards take far more abuse than the typical desktop keyboard, because of all those lunch meetings and café brainstorm sessions. Eating and drinking while over or around a keyboard just begs for problems. If you have a portable with sticking keys, look for the obvious debris in the keys. Use compressed air to clean them out. If you have serious goo and need to use a cleaning solution, disconnect the keyboard from the portable first. Make sure it’s fully dried out before you reconnect it or you’ll short it out.

•   A laptop keyboard key that doesn’t register presses or feels sticky may also have had its switch knocked out of place, especially if the key appears slightly raised or tilted. These switches can be delicate, so be careful if you want to avoid ordering replacements. Research what kind of switch your device’s keyboard uses, and be aware that a single keyboard may use a few different kinds. Look up steps for detaching and reattaching keys on that specific device if possible, and otherwise find generic instructions for the clip type before proceeding.

•   If the trackpad is having problems, a shot of compressed air does wonders for cleaning pet hair out of the trackpad sensors. You might get a cleaner shot if you remove the keyboard before using the compressed air. Remember to be gentle when lifting off the keyboard and make sure to follow the manufacturer’s instructions.

•   The trackpad driver might need to be reconfigured. Try the various options in the Control Panel | Mouse applet, or the equivalent location in System Preferences.

•   If the touch screen is unresponsive or erratic, a good first step is to check the screen for dirt, grease, or liquids, which can make the sensors go haywire; wipe it down with a dry microfiber cloth.

•   Some touch screens may appear to work improperly if they are registering an unintentional touch. Depending on the design of the device, it may be tempting to hold it in a way that leaves some part of your hand or arm too close to the edge of the screen; some devices will register this as a touch.

•   Your device may have touch-screen diagnostics available through hardware troubleshooting menus accessible through the BIOS. Refer to the manufacturer’s resources for how to access these diagnostics. If available, they are a quick way to identify whether you’re looking at a hardware or software/configuration issue. The Mouse applet in the Control Panel or Settings enables you to calibrate or reset your touch support. macOS has a Trackpad applet in System Preferences. Attempt to reset and recalibrate the display.



EXAM TIP   The troubleshooting issue known as a cursor drift can mean one of two things. First, the display shows a trail of ghost cursors behind your real cursor as you move it. This might point to an aging display or an improperly configured refresh rate. Second, the cursor moves erratically or drifts slowly in a steady direction (also known as touch calibration), whether you are touching the trackpad or not. If a reboot doesn’t fix the pointer drift, the trackpad has probably been damaged in some way and needs to be replaced.

Chapter Review
Questions
1.   Which of the following are good ideas when it comes to batteries? (Select two.)

A.   Keep the contacts clean by using alcohol and a soft cloth.

B.   Store them in the freezer if they will not be used for a long period of time.

C.   Toss them in the garbage when they wear out.

D.   Store them in a cool, dry place.

2.   To replace a wireless antenna in a laptop, what must you do?

A.   Remove the keyboard.

B.   Remove the screen.

C.   Remove the expansion slot cover on the bottom of the laptop.

D.   This cannot be done.

3.   Which of the following SSD form factors are commonly used in laptops? (Select two.)

A.   2.5 inch

B.   M.2

C.   3.5 inch

D.   1.8 inch

4.   Clara just finished a long road trip on a hot day in a car with a broken air conditioner. When she arrives at her destination, she immediately opens her laptop, which was working before she left, to check her e-mails. For some reason, every time she tries to power up the computer, it shuts down again within a few seconds. What is the most likely problem?

A.   The laptop’s hard drive died and needs to be replaced.

B.   The laptop display is faulty and needs to be replaced.

C.   The laptop fans are very dusty and need to be cleaned.

D.   The laptop is already hot from sitting in the car and needs time to cool off.

5.   What is a type of sensing device that detects the locations and duration of contact across its face, usually by a finger or stylus?

A.   Trackpad

B.   Touchscreen

C.   Touchpad

D.   Laptop

6.   Which of the following display types will you commonly find on a laptop today?

A.   CRT

B.   LCD

C.   CCFL

D.   Plasma

7.   Steve complains that his aging Windows laptop still isn’t snappy enough after upgrading the RAM. What might improve system performance?

A.   Add more RAM.

B.   Replace the power supply.

C.   Replace the battery.

D.   Replace the HDD with an SSD.

8.   Jim likes his laptop but complains that his wireless seems slow compared to all the new laptops. On further inspection, you determine his laptop runs 802.11n. What can be done to improve his network connection speed?

A.   Add more RAM.

B.   Replace the display with one with a better antenna.

C.   Replace the 802.11n card with an 802.11ac card.

D.   Get a new laptop, because this one can’t be upgraded.

9.   Edgar successfully replaced the display on a laptop (a toddler had taken a ballpoint pen to it), but the customer called back almost immediately complaining that his wireless didn’t work. What could the problem be?

A.   The problems are unrelated, so it could be anything.

B.   Edgar inadvertently disconnected the antenna from the 802.11 card.

C.   Edgar replaced the display with one without an internal antenna.

D.   Edgar failed to reconnect the antenna in the new display.

10.   Rafael gets a tech call from a user with a brand new laptop complaining that his display is flickering. What is the most likely issue?

A.   The laptop uses a plasma display.

B.   The laptop uses a CRT display.

C.   The laptop display drivers are outdated.

D.   The laptop display is faulty and needs to be replaced.

Answers
1.   A, D. Keeping a battery in the freezer is a good idea in theory, but not in practice. All batteries contain toxic chemicals and should never be treated like regular trash.

2.   B. The antenna for laptop Wi-Fi connections is located in the screen portion of the laptop. To access the antenna, remove the screen (or at least the plastic frame parts).

3.   A, B. 2.5-inch and M.2 solid-state drives are commonly used in laptops.

4.   D. Because Clara just had a long road trip in a hot car, the laptop is most likely already hot and needs time to cool off.

5.   B. A touchscreen is a type of sensing device that detects the locations and duration of contact across its face, usually by a finger or stylus.

6.   B. You’ll only see LCD displays on portables today (though they may be marketed as LED displays).

7.   D. Replacing the HDD with an SSD will speed up the system.

8.   C. Replacing the 802.11n wireless card with an 802.11ac NIC should improve his network connection speed.

9.   D. A disconnected antenna makes Wi-Fi unhappy.

10.   C. Flicker is most commonly caused by software issues like outdated or corrupted drivers.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 23 Portable Computing
Chapter 24 Mobile Devices
Chapter 25 Maintaining and Securing Mobile Devices
42h 21m remaining
CHAPTER 24
Mobile Devices
In this chapter, you will learn how to

•   Explain the features and capabilities of mobile devices

•   Describe the major mobile operating systems

•   Describe how to configure mobile devices

It’s hard to imagine that most of the mobile devices we use today (in particular the popular iPhone, iPad, and Android devices) at one time sounded like science fiction rather than reality. Mobile devices have revolutionized the way we work and play. Devices such as smartphones and tablets enable people to access unique tools and features from just about anywhere and accomplish essential tasks on the go.

As amazing as mobile devices are, it’s not easy to find a definition of mobile device that everyone agrees on. If you ask folks who are comfortable with these devices, you’ll get lots of descriptions of functions and capabilities as opposed to what they are. In essence, the following aspects make a device mobile (and even these will sometimes create debate):

•   Lightweight, usually less than two pounds

•   Small, designed to move with you (in your hand or pocket)

•   Touch or stylus interface; no keyboard or mice

•   Sealed unit lacking any user-replaceable parts

•   Non-desktop OS; mobile devices use special mobile operating systems

The last one is important—as discussed in Chapter 23, a device’s OS is the easiest way to differentiate between something like a 2-in-1 laptop in a tablet form factor and a plain tablet mobile device. Your typical portable computer runs a desktop OS such as Windows, macOS, or some Linux distribution such as Ubuntu. A true mobile device will typically run Apple iOS, iPadOS, or some form of Google’s Android.



EXAM TIP   CompTIA A+ 1102 objective 1.8 lists iPadOS, iOS, and Android under cell phone/tablet OSs. The same objective lists Windows, Linux, macOS, and Chrome OS under workstation OSs. Be aware that while there are some tablets that run versions of Windows, for exam purposes, Windows is treated as a desktop operating system rather than a mobile one.

This chapter explores mobile devices in detail. We’ll first look at the hardware features and capabilities of devices common in the mobile market. Next, we’ll examine mobile operating system software. The chapter finishes with the details of configuring the devices for personal use. We’ll save mobile device troubleshooting and security for Chapter 25. The CompTIA A+ certification exams are serious about mobile devices and we have a lot of ground to cover, so let’s get started.

1101
Mobile Computing Devices
The specialized hardware of mobile devices defines to a large degree the capabilities of those devices. This first section examines smartphones and tablets and then looks at specific hardware common to many of these devices.

Device Variants
Most modern mobile devices fall into one of a few categories, including smartphones, tablets, and wearable technology, which all have similar features and capabilities. There are a few other mobile device types, and they are best understood as devices purpose-built to be better at some task than a general-purpose device such as a smartphone or tablet; an e-reader is a good example. The CompTIA A+ 1101 exam objectives focus on smartphones and tablets, but be aware that these other types of mobile devices exist.

Smartphones
One of the earliest types of mobile device was the personal digital assistant (PDA), such as the Compaq iPaq from the late 1990s. PDAs had the basic features of today’s mobile devices but lacked cellular connectivity, so you couldn’t make a phone call. Many people, your author included, spent close to ten years carrying a mobile phone and a PDA, wondering when somebody would combine these two things. Starting around 2003–2005, companies began marketing PDAs that included cellular telephones (although cool features like using the PDA to access Internet data weren’t well developed). Figure 24-1 shows an early PDA-with-a-phone, the once very popular RIM BlackBerry.



Figure 24-1  RIM BlackBerry (courtesy of the TotalSem Tech Museum)

While these tools were powerful for their time, it wasn’t until Apple introduced the iPhone (see Figure 24-2) in 2007 that we saw the elements that define a modern smartphone:



Figure 24-2  Early Apple iPhone

•   A multi-touch interface as the primary input method for using the smartphone

•   A well-standardized application programming interface (API) enabling developers to create new apps for the system

•   Tight consolidation of cellular data to the device, enabling any application (Web browsers, e-mail clients, games, and so on) to exchange data over the Internet

•   Synchronization and distribution tools that enable users to install new apps and synchronize or back up data

Since then, smartphones have developed many more features and uses. They have come to play a big role in the trend toward ever-present connectivity and seamless data access across all of our devices. Because smartphones do so much more than simply make and receive phone calls—we surf the Web with them, stream music and video, send and receive e-mail, and even do work with them—the infrastructure and technologies that connect smartphones with a mesh of networked data and services must be fast, robust, and secure.

Most smartphones run one of the big two operating systems: Google Android or Apple iOS (see Figure 24-3). iOS runs exclusively on Apple hardware, such as the iPhone. Phones running Android come from a multitude of manufacturers. Smartphones typically have no user-replaceable or field-replaceable components, and have to be brought into specialized (and in some cases, authorized) service centers for repair.



Figure 24-3  Examples of the big two smartphone OSs: Android (left), iOS (right)

Tablets
Tablets are very similar to smartphones; they run the same (or at least similar in the case of Apple’s tablets) OSs and apps, and use the same multi-touch screens. From a tech’s perspective, they are like large smartphones (without the phone). While a typical smartphone screen is around 5 to 6 inches, tablets run around 7 to 12.9 inches (see Figure 24-4).



Figure 24-4  Typical tablet

Unlike smartphones, tablets generally lack a cellular data connection (unless you buy a model specifically designed for it), instead counting on 802.11 Wi-Fi to provide Internet connectivity. Tablets are available at many price points, from more budget-friendly options that sacrifice performance and build quality in favor of affordability, all the way to high-end devices that use cutting-edge hardware, premium materials, and the most advanced available features. Tablets have come a long way since they debuted, and are now fairly ubiquitous not only for individual users but also in business settings.

Mobile Hardware Features
Much of the usefulness of mobile devices is driven by the many hardware features they include. This section explores the basics: screen technologies, cameras, microphones, digitizers, and GPS connectivity.

Screen Technologies
Mobile devices use a variety of screen types. Most tablets use some type of LCD panel, just like portable devices and desktop monitors. The less expensive ones use twisted nematic (TN); the better ones, like the Apple iPad, use an in-plane switching (IPS) panel for richer colors and better viewing angles. Refer back to Chapter 17 if you need to review the difference between these panel types. We’ll take a look at the technology that turns these screens into touch interfaces in the upcoming “Digitizers” section.

Some smaller devices, like the better smartphones, use a related technology—organic light-emitting diode (OLED)—that lights the screen with an organic compound. Applying an electric current causes the organic layer to glow in the precise spots desired. Displaying a checkerboard pattern of black and white, in other words, only lights up the white squares. OLEDs and AMOLEDs don’t use backlights at all, which means they can display true black, they’re lighter, and they use less electricity than LCDs.



EXAM TIP   OLED screens use an organic compound exposed to electrical current for lighting; they don’t have a traditional backlight.



NOTE   Some devices use active matrix OLED (AMOLED), which adds a TFT layer for more control over the screen. AMOLED is more expensive than OLED, but provides a better picture that uses less electricity.

Cameras
Many mobile devices have distinct front-facing and rear-facing cameras. These cameras enable chatting with Grandma over Facetime, tearful YouTube confessionals, and Instagram selfies! Devices with a camera can transmit video over cellular and IP-based networks (such as the Internet) just like dedicated or built-in webcams on full-fat desktops and laptops.

Smartphone cameras have come a long way since the grainy, low-resolution images of yesteryear. Many of them now rival all but the high-end dedicated point-and-shoot cameras used by advanced hobbyists and professional photographers (see Figure 24-5).



Figure 24-5  Author’s camera app on his iPhone

Modern smartphone camera features include high dynamic range (HDR), light compensation, and other functions that enable the user to finely tune a photo or video. Manufacturers have even incorporated advances in artificial intelligence to their image-processing software to enhance the end results. Higher-end and even midrange devices often have more than one camera lens built in, allowing for more versatile photography. Additionally, these cameras offer a variety of options when taking photos and video; some cameras enable you to take “bursts” of shots (like ten in a single second) to make sure you capture faster-moving objects and action shots, as well as slow-motion video. When coupled with the multitude of apps available for mobile devices, you can edit photos and videos on-the-fly, adding light-filter effects, cleaning up shots, and even adding special effects.

Microphones
Almost all mobile devices incorporate at least one microphone. Smartphones certainly wouldn’t be of much value without a microphone, and you wouldn’t be very effective at communicating over Skype or FaceTime without them. Additionally, many people use mobile devices to dictate speech or record other sounds, so microphones serve many purposes on mobile devices.

As with the portable devices discussed in the previous chapter, mobile devices commonly have more than one microphone to enable noise-cancelling routines to work their magic. In contrast to those more traditional portables, you may need to take more care to avoid blocking any of the microphones on a mobile device.

Digitizers
When electrical engineers talk about a digitizer, they refer to a component that transforms analog signals into digital ones; that is to say, it digitizes them. That’s not what we techs talk about when discussing digitizers on mobile devices. A digitizer refers to the component that provides the “touch” part of a touch screen. When your finger contacts a touch screen, the digitizer’s fine grid of sensors under the glass detects your finger and signals the OS its location on the grid. As with modern trackpads, you can use one or more fingers to interact with most touch screens.



EXAM TIP   The CompTIA A+ 1101 exam objectives mention touch-screen configuration as something you do on a laptop or mobile device. While this used to only really apply to touch-screen laptops, some configuration options for touch screens have made their way to tablets and smartphones as well.

Location Services
One major feature of mobile devices is the ability to track the device’s location through global positioning system (GPS) services, cellular, or Wi-Fi connections. Users rely on cellular location services to conveniently find things near them, such as stores and restaurants, or to determine when their Uber driver will show up. This section discusses some of what a mobile device such as a smartphone can do with GPS capability, followed by a look at privacy concerns associated with location tracking.

A great example of how smartphones can use GPS is the traffic and navigation app Waze (see Figure 24-6). Waze not only navigates, but its crowd-sourced data collection provides you with amazing real-time knowledge of the road ahead.



Figure 24-6  Waze in action

Another cool use of GPS is finding your phone when it’s missing. The iPhone offers the Find My iPhone app (see Figure 24-7), for example. This feature is part of the iCloud service that comes free with any iOS device.



Figure 24-7  Find My iPhone app

Location Tracking and Privacy  Tracking your location is generally a good thing…when you want to be tracked. By default, mobile OSs track and in many cases record your location for an extended amount of time. This is called geotracking, and not everyone likes it. If you don’t like this feature, turn it off. Figure 24-8 shows turning off Location on an Android phone.



Figure 24-8  Turning off Location



EXAM TIP   Because mobile devices tap into the Internet or cellular phone networks, the devices have identifying numbers such as a MAC address. The cell phone companies and government agencies can use the ID or MAC address to pinpoint where you are at any given time. Geotracking has a lot of room for abuse of power.

1102
Mobile Operating Systems
Most mobile devices run either Apple iOS or Google Android. This section discusses their development and implementation models, as well as some of their major features, including how their app stores work.

Development Models
Before we look at each mobile operating system in detail, let’s step back to consider the big picture. The different underlying philosophies inspiring these operating systems—and guiding the companies that make them—help us understand why they do something one way instead of another. We’ll start with a look at closed source and open source as development models. You may have heard these terms regarding how software is released and licensed (if not, Chapter 28 will discuss how these terms apply to licensing), but they also provide an interesting framework for looking at how products are developed and released. Then we’ll discuss how these models apply to operating systems.

Closed Source
When it comes to development models, it may help to think of closed source as another way to refer to the traditional practice of making and selling a product without telling anyone how you made it. The traditional model makes intuitive sense, at least in our culture; how your product is made is a trade secret—something that gives you a competitive edge—and sharing it could inspire competitors to use your design, or potential customers to make it themselves.

Vendor-Specific and Proprietary  We sometimes apply the terms vendor-specific or proprietary to a closed-source product or technology, most often when we’re trying to highlight something that doesn’t use common, open standards. The terms are related to closed source, but don’t confuse them; they aren’t interchangeable. These labels often imply that the product may not play nice (or be interoperable) with other products, may have connectors and cables that are hard to find or expensive, may not be friendly to users who want to tinker with or modify it, may be harder to repair, and may pose a host of other problems.

The concept behind and use of these terms is sometimes slippery. As you’ll see later in the chapter, a device maker may use a common standard such as USB 3.0, but design its own connector. Even though the device maker is technically using part of the open USB 3.0 standard, we’ll still call the device’s ports and cables proprietary.

Open Source
In this broader sense, you can think of a product as open source if its maker releases the instructions for making it—it doesn’t have to be software (though that’s usually the context). When a company commits to open sourcing one or more products, it has to operate differently than companies using a closed-source model. Secrecy, for example, is necessarily a smaller part of its business; knowing that anyone could make its products, the company has to focus on other factors (such as price, service, support, convenience, quality, innovation, etc.) to stay competitive.

Just because a company releases these instructions to the public doesn’t mean anyone else gets to own them. Much as artists and authors set terms that specify whether the rest of us can legally copy or modify their work, the owners or authors of the instructions for making a product will specify terms for how others are allowed to use them. Sometimes the owners or authors may just say they’re releasing the instructions for personal use or educational purposes—you can study what they’ve done and make your own product, but you can’t start selling copies. When it comes to open-source software, these terms commonly dictate whether companies who modify the software are obliged to publish their changes, and whether they’re allowed to profit from how they use it.

Development Models and the Mobile OS
The development model is one of many choices that reflect underlying company philosophy and goals. A company that makes an open-source mobile operating system like Google Android has little control over how the OS will be used and who can modify it. A company that makes a closed-source operating system like Microsoft Windows but licenses the OS to device makers has more control—the company knows the OS won’t be modified and can be picky about which devices to license it for. A company making a closed-source OS like Apple iOS for its own devices can tailor-fit the software to the hardware it will run on. A company that builds an OS others can use and modify as they see fit and a company that builds an OS handcrafted exclusively for its own hardware obviously have very different underlying philosophies and goals.

The big thing to keep in mind with an open-source operating system like Android is that companies building devices that use the OS don’t have to share the OS developer’s underlying philosophy—they can have wildly varying goals and development models of their own. If the operating system’s license allows it, each of the device makers could modify the OS before installing it on their own device—and never release those modifications. The modifications might just enable special hardware to work, but they could also install apps you don’t want and can’t remove, cause third-party apps coded without knowledge of the modifications to malfunction, or collect information about how you use the device.

To bring this all together, the point is that a manufacturer can put an open-source operating system on an otherwise closed-source device—don’t assume a device is itself open source just because the mobile OS it uses is. In fact, vanishingly few of the devices with an open-source OS are best seen as open-source products.

Think back to the earlier discussion of an open-source development process and apply it to a smartphone. The most extreme interpretation of an open-source smartphone is that the maker has released all of the instructions and code someone else would need to manufacture an identical smartphone and all of the components inside it. A more likely (but still exceptional) scenario is that all of the software on the device when it leaves the factory is open sourced, including the operating system, drivers, and the firmware powering its components.

Apple iOS and iPadOS
Apple’s closed-source mobile operating system, iOS (see Figure 24-9), runs on the iPhone. (The Apple iWatch runs a different OS, called watchOS. It is also closed source.) The Apple model of development is very involved: Apple tightly controls the development of the hardware, OS, developer tools, and app deployment platform. Apple’s disciplined development model is visible in its strict development policies and controls for third-party developers, and this control contributes to the high level of security in iOS.



Figure 24-9  iOS 15

iOS apps are almost exclusively purchased, installed, and updated through Apple’s App Store. An exception is providers of line-of-business apps specific to a particular organization. These internal development groups reside within an organization and can develop iOS apps, but deploy them only to devices that are under the organization’s control, skipping the public App Store. They still have to undergo a type of Apple partnering and enterprise licensing approval process.

Apple’s famous iPad tablet used to run iOS, but over time, the needs of tablet users evolved, and it now runs iPadOS (see Figure 24-10) The differences between iOS and iPadOS are slight, and the experience of using an iPad is very similar to that of using an iPhone. The average user may not notice the differences, but there are some important distinctions between the two that a good tech should aware of.



Figure 24-10  iPadOS in action

One key difference is in touch pen compatibility. Touch pens are, in general, an advanced version of the traditional stylus, which usually is just a plastic pointer with some kind of rubber point. Apple’s touch pen is called the Apple Pencil and only works with iPadOS-equipped devices. Beyond keeping the screen clear of fingerprints, a touch pen can be used to effectively handwrite notes and draw precise and often professional-caliber artwork. Tablet users have gravitated toward using tablets as laptop substitutes in some cases, so iPadOS accommodates this by incorporating some of the features more commonly associated with macOS, such as multitasking functionality, mouse and keyboard support, and the ability to connect external storage via USB-C. On the flipside, there are things that iOS does that iPadOS doesn’t. Most notably, iOS allows direct pairing with Apple’s smartwatch, while iPadOS does not.

Google Android
For simplicity, think of Android and iOS as opposites. Android (see Figure 24-11) is an open-source platform, based on yet another open platform, Linux, and is owned by Google. Because Android is open source, device manufacturers can (and do!) alter or customize it as they see fit; there are differences among the implementations from various vendors. Google writes the core Android code and occasionally releases new versions (naming each major update after a dessert or candy of some sort), at which point vendors customize it to add unique hardware features or provide a branded look and feel.



Figure 24-11  Android 12 (Snow Cone)

Android apps are available to purchase and download through various app stores, such as Google Play and the Amazon Appstore. Android app stores tend to be fairly open in contrast to the high standards and tight control Apple applies to its third-party app developers, and Android makes it easier to install arbitrary applications downloaded from a Web site.



NOTE   Android-based devices may be more open than iOS ones on average, but it isn’t a given. How open or closed an individual Android device is will depend greatly on how its manufacturer has modified the OS.

Mobile OS Features
Mobile operating systems come in a variety of flavors and sometimes have different features as well as different interfaces. But they also have a great deal in common, because consumers expect them to perform most of the tasks they are used to seeing in other mobile devices, regardless of operating system. Whether you are using an iPhone, an Android phone, or a smart watch, you still expect to be able to send texts, check your e-mail, and make video calls. Because of this, mobile OS differences boil down to hardware and app support, look and feel, and philosophical differences that manifest in how the OS goes about a common task. We’ll take a quick look at some of the features common to all mobile operating systems and point out differences along the way.

User Interfaces
All mobile OSs have a graphical user interface (GUI), meaning you interact with them by accessing icons on the screen. Current models do not offer a command-line interface. Each OS usually has either a major button or a row of icons that enables the user to navigate to the most prominent features of the device. They also all support touch gestures, such as swiping to navigate between screens or pinching to zoom in or out. Most mobile OSs have some type of menu system that enables the user to find different apps and data.

iOS offers some customization of the user interface. You can group apps together into folders, for example, and reposition most apps for your convenience. The iOS look and feel, however, will remain consistent.

Android offers a very different GUI experience by employing programs called launchers that enable users to customize their Android device extensively. Many companies make launchers, and different manufacturers ship devices preloaded with launchers they make or prefer. Samsung devices use the TouchWiz launcher, for example. I use the Nova launcher on my Android phone. The launcher enables you to change nearly every aspect of the GUI, including icon size, animations, gestures, and more.

Most mobile devices include an accelerometer and a gyroscope, one to measure movement in space and the other to maintain proper orientation of up and down. These extend the user interface to include how you move the device itself; a common use is changing the screen orientation when you rotate a device from vertical to horizontal, for example, to enhance watching videos on YouTube.

Wi-Fi Calling
While every mobile device that calls itself a phone must have support for cellular wireless, another feature that many mobile devices include is Wi-Fi calling, the capability to make regular phone calls over Wi-Fi networks. Wi-Fi calling is very useful if you often find yourself in a place with poor cellular coverage but good Wi-Fi. To use Wi-Fi calling, first both your phone and carrier need to support it, then you need to enable it in your phone settings (see Figure 24-12). Once Wi-Fi calling is enabled, the phone will use any Wi-Fi network it’s connected to (assuming the performance is acceptable) for all phone calls.



Figure 24-12  Option to enable Wi-Fi calling on an iPhone 13 Pro

Virtual Assistants
“Hey, Siri!”

“Yes, Mike?”

“What’s the weather like today?”

“Always sunny where you are, Mike.”

Okay, maybe they’re not quite that cool, but the virtual assistants on smartphones and tablets enable quick, vocal interaction to accomplish common goals. For example, one only has to ask Siri (Apple’s virtual assistant) how to find the nearest restaurant or tourist attraction, and she (Siri’s voice is female by default) will respond with the information sought. Virtual assistants can also be useful in performing Internet searches and, in some cases, even activating and using certain apps on the mobile device. This helps people who may have certain disabilities that may prevent them from tapping or typing on the device, by enabling them to use voice commands.

A virtual assistant is also useful if you must use your smartphone while driving (although anything that diverts your attention from the road is discouraged for safety reasons). You can speak to the smartphone’s virtual assistant to place a call or get directions while driving, especially if the smartphone is paired with the car’s Bluetooth system. The Windows 10/11 equivalent to Siri is called Cortana, and essentially serves the same functions and provides the same services and features. Google’s virtual assistant, Google Assistant, is also available for iOS and any of Google’s many platforms like Google Home and Android TV. In addition to the big three’s virtual assistants, there are also apps you can download that provide other virtual assistant services, depending upon your platform.

Software Development Kits
Most mobile operating systems come with some sort of software development kit (SDK) or application development kit that you can use to create custom apps or add features to existing apps on the device. Figure 24-13 shows the development (programming) environment for the iOS SDK, Xcode, with the code for an iOS app open in the background window, and the same app code running in an iPhone simulator on top.



Figure 24-13  Xcode running an app written with the iOS SDK

Each mobile OS poses its own challenge to app developers. Apple’s rigid development model makes it such that your app must pass a rigorous testing program before it is allowed into the App Store. Microsoft’s development model, while not typically as rigid, is similar in nature. Google, on the other hand, allows anyone to create Android apps and distribute them to the masses without much interference.

Emergency Capabilities
One feature almost all currently marketed smartphones have built in is the emergency notification feature that enables them to receive broadcasts from national emergency broadcast systems, such as the Emergency Alert System (EAS) in the United States. This can be a very useful feature during severe weather, enabling you to receive warning text messages. In the event someone reports a child missing in your immediate area, it enables you to get AMBER Alerts. Many of these emergency broadcast system alerts also force your phone to emit a very loud sound or vibrate incessantly in order to get your attention.

While modern smartphones can place 911 calls effectively, the old 911 system relied on the Public Switched Telephone Network (PSTN) to trace a call and determine its location, in order to dispatch emergency responders to the correct address quickly. This was problematic with mobile devices, so legislation was passed (the Wireless Communications and Public Safety Act of 1999) requiring carriers to be able to pinpoint the location of a mobile device, such as a smartphone. The Enhanced 911 (E911) system uses GPS and cellular networks to triangulate the location of a phone by its distance from cell towers, its transmission delay time, and other factors.

Mobile Payment Service
As smartphones and other mobile devices have become so much more commonplace in our daily lives, we’ve become very reliant on them to store our personal and sensitive information such as passwords, credit card numbers, financial documents, receipts, and more. Over time, smartphone manufacturers, as well as merchants, realized that the next logical step was to enable you to pay for goods and services simply by scanning your smartphone or using an app.

The app connects to your bank information and automatically transfers the funds from your bank to the merchant. This feature is called mobile payment service. Near field communication (NFC) applications refine the process further: simply place your device on or near the special pad at the register in order to authorize payment to the merchant. (See “NFC,” later in this chapter, for the scoop on these tiny networks.)

Additionally, smartphone manufacturers produce their own payment systems. The Apple payment system, called Apple Pay, was first implemented with the iPhone 6, and support has been integrated into the Apple Watch. Apple Pay supports major credit card payment terminals and point-of-sale systems, including those fielded by Visa, MasterCard, and American Express. Apple Pay can use contactless payment terminals with NFC and supports in-app payments for online purchases.

Mobile payment systems have become a lot more popular over time. Since Apple saw success with Apple Pay, other software companies and mobile manufacturers followed suit. Samsung, one of the most prominent manufacturers of Android smartphones, released Samsung Pay in 2015. Google released their version in 2018, and predictably named it Google Pay. These apps have expanded their functionality to serve as full-blown digital wallets, allowing you to do more than just pay for things. One of the coolest features is that users can now store and transfer digital tickets for concerts and sporting events, making forgotten or lost tickets largely a thing of the past.

Airplane Mode
Airplane mode is simply a switch (either an actual hardware switch located on the mobile device or a software switch that can be located in the device’s configuration settings) that turns off all cellular and wireless services, except Bluetooth (see Figure 24-14). The aptly named mode disables these communications so passengers can comply with restrictions protecting aircraft instruments from interference, though you can also use it as a shortcut for turning off communication functions.



Figure 24-14  Airplane mode enabled on iOS 15

VPN
As you’ll recall from earlier chapters, VPNs establish secure connections between a remote client and the corporate infrastructure, or between two different sites, such as a branch office and the corporate office. VPNs are typically implemented using tunneling methods through an unsecure network, such as the Internet. In a client VPN setup, the host has client VPN software specially configured to match the corporate VPN server or concentrator configuration. This configuration includes encryption method and strength, as well as authentication methods.

A site-to-site VPN scenario uses VPN devices on both ends of the connection, configured to communicate only with each other, while the hosts on both ends use their respective VPN concentrators as a gateway. This arrangement is usually transparent to the users at both sites; hosts at the other site appear as if they are directly connected to the user’s network.

VPNs can use a variety of technologies and protocols. The most popular ways to create a VPN are to use either a combination of the Layer 2 Tunneling Protocol (L2TP) and IPsec (see Figure 24-15), or Secure Sockets Layer (SSL)/Transport Layer Security (TLS). When using the L2TP/IPsec method, UDP port 1701 is used and must be opened on packet-filtering devices. In this form of VPN, users connect to the corporate network and can use all of their typical applications, such as their e-mail client, and can map shares and drives as they would if they were actually connected onsite to the corporate infrastructure.



Figure 24-15  Configuring a VPN

An SSL/TLS-based VPN, on the other hand, uses the standard SSL/TLS port, TCP 443, and is typically used through a client’s Web browser. SSL/TLS-based VPNs don’t normally require any special software or configuration on the client itself, but they don’t give the client the same direct access to resources on the corporate network. Therefore, users may have to access these network resources through the client browser via an access portal.



NOTE   SSL has been entirely replaced by TLS, but you’ll often still see things referred to as SSL/TLS or SSL. VPNs are one example where this is the case.

1101
Configuring a Mobile Device
Mobile devices require some setup and configuration to function seamlessly in your life, though the industry is constantly refining and simplifying this process. Mobile devices typically come preconfigured with everything but your user account and network credentials. Just because you don’t have to do much to get up and running anymore doesn’t mean you’re out of the woods, though. You may well need to configure corporate e-mail accounts, device add-ons, apps, synchronization settings, and other advanced features.

You can add capabilities by enhancing hardware and installing productivity apps. You also need to set up network connectivity, add Bluetooth devices, configure e-mail account(s), and enable the devices to synchronize with a computer. Plus you have a lot of add-on options; let’s take a look.

Enhancing Hardware
A mobile device is a computer, just like your desktop or laptop, with the same basic components doing the same basic things. The construction centers on a primary circuit board, the motherboard, onto which every other component is attached. The biggest of these components is often the system on a chip (SoC), a wonder of miniaturization combining a CPU, GPU, and sundry other support logic onto a single silicon die, saving a lot of space and power in the process. An interesting aside about the CPUs used in these devices is that they are rarely Intel x86 based; instead, you are much more likely to run across an ARM architecture chip when perusing the spec sheets of your new tablet or smartphone. The iPad uses Apple-designed ARM A-series or M-series chips, for example, while Samsung’s smartphones and tablets generally use ARM chips from Qualcomm’s Snapdragon line-up.

Mobile devices use storage, though you’ll never see one using a traditional magnetic hard disk drive (HDD) with spinning platters. Mobile devices use flash media such as a solid-state drive (SSD) or microSD card because they are smaller, use less power, and are much, much faster than spinning HDDs. Plus they’re cooler, just like you.

Mobile devices differ from their larger brethren in two very significant areas of importance to techs. First, none of them offer any user-replaceable parts. If something breaks, you send the device back to the manufacturer, visit a local manufacturer-supported retail outlet such as the Apple Store, or take it to a specialized repair shop. Second, you can’t upgrade mobile devices at all. Even a laptop enables you to upgrade RAM or a mass storage drive, for example, but the mobile device you buy is exactly what you get. You want something better? Buy a new one.

That said, every mobile device enables you to attach some kind of peripheral or external storage device. But every device offers different expansion capabilities, so it’s hard to generalize about them. The closest you can get is the audio jack, but many smartphones no longer include them, in favor of Bluetooth connectivity. That being said, audio jacks are still around on some devices (see Figure 24-16).



Figure 24-16  Earbuds plugged into a smartphone

Note this is quickly changing as Apple dropped the jack as of the iPhone 7, and many Android devices have started leaving the port off as well, as Bluetooth wireless earbuds and speakers continue to become more popular, reliable, and affordable. Current iPhones and most iPads use the Lightning jack or USB-C, respectively, for physical external connections.

Apple Expansion Options
Apple devices offer the least expansion capability of all mobile devices, so even though they dominate the U.S. marketplace, there’s not much to say about them. Most of the expansion on Apple devices is limited to proprietary cables and devices. The iPhone and iPad have historically used a single proprietary Lightning port for charging the device and connecting to the few external devices available. Figure 24-17 shows the typical use for the port: connecting to a USB AC adapter to charge.



Figure 24-17  USB charger connected to proprietary Lightning port

While the vast majority of Apple’s iOS devices stick with the proprietary Lightning connector, Apple has switched to USB Type-C with most iPad variants. Who knows what this means for the iPhone line, but it is nice to see Apple expanding its use of the industry standard. We’ll return to USB Type-C, along with a number of other connectors, later in the chapter.

iPhones and iPads enable you to mirror the screen to a multimedia device such as a projector or a smart TV. This enables seamless presentations, for example, through the excellent Apple Keynote program (see Figure 24-18). The multimedia connection originally required another adapter (see Figure 24-19), but if you’re using your device with a smart TV or another Apple device like an iMac, you can achieve this wirelessly with a feature called AirPlay.



Figure 24-18  Apple Keynote on an iPad and a projector



Figure 24-19  Apple Digital AV Adapter

Android Expansion Options
Devices that use Google Android come with a variety of connections and expansion capabilities. Some offer microSD slots for adding storage in the form of these tiny flash memory cards (see Figure 24-20), but this is becoming less common.



Figure 24-20  microSD card and slot

Android devices used to have a more diverse range of connectors available, both for charging and connecting peripherals. Older devices sometimes used miniUSB, or proprietary power connectors, and some Android smartphones even had a tiny Micro-HDMI port. This has largely gone the way of the dinosaurs though, and most Android devices you’ll see today make use of USB-C or occasionally still use microUSB.

Finally, some tablets (but rarely smartphones) sport a connector for attaching the device to an external monitor, such as a big screen or projector. Figure 24-21 shows a Micro-HDMI port and connector.



Figure 24-21  Micro-HDMI port and connector

Bluetooth
The last way that mobile devices expand their physical capabilities is wirelessly, most often using the Bluetooth standard (if you need a refresher on Bluetooth, refer back to Chapter 20). Traditionally, extending a mobile device with Bluetooth has meant adding a headset, mouse (though not with Apple iOS products), keyboard, or speaker. Figure 24-22 shows a diminutive Apple keyboard for the iPad and the iPad resting in a stand to make typing a little easier than using the virtual keyboard. With Bluetooth-enabled wearable devices growing in popularity, it can be tricky to decide how self-sufficient one of these must be before it stops counting as a mobile enhancement and enters the realm of full-fledged mobile device.



Figure 24-22  Keyboard associated with iPad



NOTE   See the “Bluetooth” section toward the end of this chapter for the steps to set up a mobile device with a Bluetooth speaker.

Installing and Configuring Apps
Mobile devices come from the manufacturer with a certain number of vital apps installed for accessing e-mail, surfing the Web, taking notes, making entries in a calendar, and so on. Almost all mobile devices offer multimedia apps to enable you to listen to music, take pictures, watch YouTube videos, and view photos. You’ll find instant messaging tools and, in the case of smartphones, telephone capabilities.

Beyond these essentials, you’ll install most other apps through an app store. As you read about the app ecosystem for each mobile OS, consider how well the details of each ecosystem mesh with the development models discussed earlier in the chapter. Even though the rules of each app ecosystem usually reflect this development model, don’t assume the apps on offer will follow suit—you’ll find plenty of closed-source apps available on Android and open-source apps available for iOS.

iOS/iPadOS Apps
Apple iPhone and the iPad use the iOS and iPadOS operating systems, respectively. Apple exerts more control over the user experience than any other manufacturer by insisting all app developers follow strict guidelines.

Apple maintains strict control over what apps can be installed onto iOS/iPadOS devices, meaning that if you want to get an app for your iPhone or iPad, you can only get it from the Apple App Store (see Figure 24-23). Apple must approve any app before it goes into the App Store, and Apple reserves the right to refuse to distribute any app that fails to measure up.



Figure 24-23  App Store

To add an app, select the App Store icon from the home screen. You can explore featured apps in the Today tab or peruse by category. You can check out the popular games, or simply search for what you want (see Figure 24-24).



Figure 24-24  Searching for Monument Valley 2

The first time you try to purchase an app through the App Store, you’ll be prompted to set up an account. You can use an account that you created previously through the Apple iTunes music and video store or create a new Apple ID account. You can create a new Apple ID account with a few quick steps (see Figure 24-25) and a valid credit card.



Figure 24-25  Creating an Apple ID for iCloud and App Store purchases

Another iCloud feature, the iCloud Keychain, builds on the Keychain feature in macOS to synchronize user information, passwords, payment information, and other credentials with all of your Apple devices. (See “Synchronization,” a little later in the chapter.) Keychain can seamlessly store many non-Apple credentials as well, such as logins for Facebook, Amazon, and other providers, and use them to auto-complete repetitive forms in both device apps and on Web sites. The real benefit is that you can authorize Apple to save this sensitive information, instead of authorizing each individual app or site to keep a copy.

Android Apps
Google Android powers many smartphones and a solid portion of tablets. Unlike Apple iOS, Google gives core Android away, enabling manufacturers to differentiate their Android devices from those of other manufacturers. A Samsung tablet, in other words, uses a version of Android that differs somewhat from the Android an ASUS tablet uses. Likewise, OnePlus developed a custom interface called OxygenOS to change the look and feel of Android on its devices.

Because of these modifications, few Android users ever use “stock” or unmodified Android. Despite the shared core OS, Android users familiar with devices from one manufacturer may get tripped up by the different interface on Android devices from a different maker. These differences make it important to combine knowledge of the Android version a smartphone or tablet runs with knowledge about the manufacturer and its modifications to Android. The manufacturer will typically assign a version number to each release of its modifications.

Android devices can usually get apps from more than one source. The most common is Android’s default app store, Google Play (which offers well over 2 million apps)—but some manufacturers (such as Amazon, for its line of Fire devices) modify Android to change this.

Many manufacturers offer a store with apps developed or customized to work with their devices. These vendor-specific stores enable you to get apps that should work well with your Android smartphone or tablet.

You can also go to a third-party app store or market for apps developed “for Android” that probably will work with your device, but there’s no guarantee that they’ll work on all Android devices. This Wild West approach to apps makes the Android smartphone or tablet experience vastly different from the experience on iOS.

Network Connectivity
Mobile devices connect to the outside world through the cellular networks or through various 802.11 Wi-Fi standards. You learned specifics about the standards in Chapter 20, so I won’t rehash them here. This section looks at standard configuration issues from the perspective of a mobile device.

When you want to connect to a Wi-Fi network, you need to enable Wi-Fi on your device and then actively connect to a network. If the network is properly configured with WPA2, or WPA3 encryption, then you also need to have the logon information to access the network. The most common way to connect is through the Settings app (see Figure 24-26).



Figure 24-26  Selecting the Settings icon

The Settings app enables you to do the vast majority of configuration necessary to a mobile device. To join a network, for example, tap the Wi-Fi (or Networks) option to see available networks (see Figure 24-27). Simply select the network you want to join and type in the passphrase or passcode. Give the mobile device a moment to get IP and DNS information from the DHCP server, and you’re on the network.



Figure 24-27  Browsing available networks

After you connect to a network successfully, all mobile devices store that network access information automatically, creating a profile for the network based on its SSID. This works just like with any other device that connects to a Wi-Fi network. If the SSID of a network changes after you’ve connected to that network, your mobile device will fail to connect to the rechristened network. You need to delete the profile and reconnect. Delete the profile through the Settings app by choosing the Wi-Fi network and selecting Forget this network.



EXAM TIP   You can use the Settings app to turn off Wi-Fi or to go into airplane mode to stop the device from sending any signals out.

Cellular Data Networks
Anyone with a smartphone these days can enjoy the convenience of using wireless cellular technology. Who doesn’t love firing up an Android phone or an iPhone and cruising the Internet from anywhere? As cell-phone technology converges with Internet access technologies, competent techs need to understand what’s happening behind the scenes. That means tackling an alphabet soup of standards. Regardless of the standard, the voice and data used on smartphones and some tablets (unless you have 802.11 wireless turned on) moves through a cellular wireless network with towers that cover the world. Back in Chapter 21, we discussed the technologies that make up cellular networking, so now we’re going to talk about how it can be enabled and disabled on most mobile devices.

As discussed earlier in this chapter in the context of mobile operating systems, Android and iOS have a lot in common and that includes similar ways to enable and disable your cellular network. The way to accomplish it is fairly simple: swipe down from the top of the screen to check for a quick option, labeled with something like Data or Cellular. Alternatively, you can use the Settings app (introduced in the previous section). Once you’ve found it, look for the menu option that says Data or Cellular, and toggle it on or off.

Radio Firmware
Mobile devices use a wide variety of radio technologies to access the Internet, e-mail, and corporate infrastructures. Generally, mobile devices have two types of radios: 802.11 and Bluetooth. If the device can make calls, it also has some form of cellular radio.

PRL, PRI, and Baseband Updates  As mobile devices travel, they frequently have to pass through areas that don’t have strong signals, or into areas that the carrier does not service. When a mobile device connects to different carriers’ networks, we say it is roaming; roaming may result in additional service charges, depending upon the carriers involved.

Your phone’s firmware will receive occasional automatic updates to its Preferred Roaming List (PRL) from the carrier; the PRL is a priority-ordered list of the other carrier networks and frequencies it should search for when it can’t locate its home carrier’s network. Updates to this list are sent via your phone’s cellular connection (called baseband updates, or over-the-air updates) or, in some cases, through firmware updates during normal operating system and firmware upgrades via synchronization.

CDMA devices may also receive product release instruction (PRI) updates, which modify a host of complex device settings. Don’t worry about specifics, here—these settings can pertain to the intricacies of many functions such as GPS, cellular connectivity, and messaging—but instead focus on the fact that carriers use these product release instructions to ready the device for deployment on their networks, enable the network to route calls or messages to the device, and more. As such, PRI updates may be needed if the network is evolving during the lifetime of a device, the device needs to be moved to a new network, or the device has a new owner.



EXAM TIP   PRL updates are handled automatically during firmware/OS updates. They are only for CDMA networks. No one but the nerdiest of nerds will ever see these updates.

IMEI, ICCID, and IMSI  There are three particular identifiers you will need to understand in order to effectively manage mobile devices. The International Mobile Equipment Identity (IMEI) number is a 15-digit number used to uniquely identify a mobile device. IMEI numbers are unique to devices using the Global System for Mobile Communications (GSM) family of technologies, including its present-day descendants: 4G LTE and 5G. You can typically find this number printed inside the battery compartment of the mobile device, but you may not need to take the device apart: some operating systems enable you to view it inside the device configuration settings (see Figure 24-28).



Figure 24-28  IMEI settings on an Android phone

The IMEI number can be used to identify a specific device and even to block that device from accessing the carrier’s network. If the device is lost or stolen, the user can notify her carrier, and the carrier can make sure the device can’t be used on the network.



NOTE   Always write down your IMEI number when you get a new phone, as it can prove you are the actual owner if the phone is stolen or lost.

The ICCID number, which stands for Integrated Circuit Card Identifier, uniquely identifies a subscriber identity module (SIM). The SIM contains information unique to the subscriber (the owner of the phone), and is used to authenticate the subscriber to the network. SIMs can be moved from phone to phone, usually with no problems.

The third number is the International Mobile Subscriber Identity (IMSI) number. It is also included on the SIM, but represents the actual user associated with the SIM. This number is not normally accessible from the phone, but is usually available from the carrier, to ensure that stolen phones are not misused. The IMSI number can also be used to unlock a phone.

You might want to record these numbers for each managed device in the enterprise, whether for inventory purposes or so that you have them handy when you work with your mobile device management (MDM) software (look for a more in-depth explanation about MDM software in Chapter 25). The MDM software typically collects these identifiers along with other device information (such as the telephone number or MAC address) during the provisioning process and stores them in the mobile device inventory for you. Figure 24-29 shows how IMEI and ICCID numbers are listed for a newer Android device in the device settings.



Figure 24-29  IMEI and ICCID numbers

Data
Many mobile devices can use the cellular data services discussed in Chapter 20 to access the Internet. This way you can use your smartphone, tablet, or other mobile devices to get e-mail or browse the Web pretty much anywhere.

By default, mobile devices that use cellular networks for Internet connectivity use data roaming, meaning they’ll jump from cell tower to cell tower and from your provider to another provider without obvious notice. This is no big deal when you travel within your own country where competing providers have inexpensive roaming agreements.

Watch out for data roaming outside your country! If you travel to another country, your mobile device will happily and seamlessly connect via another cell provider if one is available. This can lead to some shockingly huge bills from your cell phone company when you get back from that cruise or international trip. If you’re going outside your cell provider’s coverage area, get a plan that specifies that you’re traveling. It’ll still be more expensive than your regular plan, but not nearly as crazy as an accidental roaming charge.

If you don’t need to connect when out of country, turn data roaming off. You’ll find the feature in the Settings app, as you might expect. You can also turn off cellular data entirely or only turn off cellular services selectively if your device can do more than one type. You would want to turn off cellular data, for example, if you don’t have an unlimited data plan and are getting near your limits. There are also some security reasons to disable cellular connections while traveling, which we’ll explore further in Chapter 25.

E-mail
Every mobile device uses an e-mail service set up specifically from the mobile OS developer. Plus, you can configure devices to send and receive standard e-mail as well. Let’s look at the integrated options first.

All mobile devices offer e-mail services from the manufacturer or the OS developer. iOS and iPadOS devices integrate perfectly with iCloud, Apple’s one-stop shop for e-mail, messaging, and online storage. Android devices assume a Gmail account, so they feature a Gmail option front and center.

Aside from the integrated e-mail options, mobile devices enable you to set up standard corporate and ISP e-mail configurations as well. The process is similar to that of setting up e-mail accounts that you learned about in Chapter 21. Apple devices go through the Settings app, tap Mail, then tap the Accounts option (see Figure 24-30). Tap the Add Account option to bring up the default e-mail options (see Figure 24-31). If you want to connect to a Microsoft Exchange Server–based e-mail account, tap the appropriate option here and type in your e-mail address, domain, username, password, and description.



Figure 24-30  Accounts screen on iPhone



Figure 24-31  Default e-mail types on iPhone

Neither POP3 nor IMAP4 is one of Apple’s suggested options, so if you want to set up an account of either type, you’ll need to tap the Other option on the initial Add Account screen. Eventually you’ll get prompted to choose POP3 or IMAP and type in addresses for the sending (SMTP) and receiving servers.

Android-based devices assume you’ll have a Gmail account as your primary account, so you’ll find Gmail’s distinctive app icon on the home screen (see Figure 24-32). Gmail also can talk to other, non-Gmail e-mail services for setting up Exchange, POP3, or IMAP4 accounts; you configure it the same way as you would a desktop e-mail application, including putting in the port number and security type, in this case, TLS, if the server lacks autoconfigure (see Figure 24-33).



Figure 24-32  Gmail app



Figure 24-33  Setting up a secure IMAP account



EXAM TIP   The latest versions of Android simply query the e-mail server to configure port numbers and security types automatically, just like modern desktop-based e-mail clients. Even though current devices automate this process, the CompTIA A+ 1101 objectives include port numbers, so you need to know them.

The CompTIA A+ 1101 exam will hit you pretty hard on e-mail settings, specifically on TCP port numbers for the various e-mail protocols. We’ve covered these in earlier chapters, but here’s a quick cheat sheet and a few alternative numbers for real-world applications:

•   POP3 uses TCP port 110.

•   IMAP4 uses TCP port 143.

•   SMTP uses TCP port 25.

Many servers block these default ports; plus, when you move to more secure versions of the protocols, you need to use other port numbers. I have no clue whether CompTIA will quiz on the secure ports for POP3, IMAP4, and SMTP, but here they are:

•   Secure POP3 uses TCP port 995.

•   Secure IMAP4 uses TCP port 993.

•   Secure SMTP uses TCP port 465 or 587.

Finally, you may also have to configure other settings, such as Secure/Multipurpose Internet Mail Extensions (S/MIME) standard, used to configure digital signature settings for e-mail, and contacts from the corporate address book, depending on how the corporate e-mail server is set up.



EXAM TIP   Be familiar with corporate e-mail configuration settings for Gmail, Yahoo, Outlook, and iCloud (You’ll get a closer look at them in Chapter 25). Know the corporate and ISP e-mail configuration settings for POP3, IMAP4, port and security settings, and Exchange.

Synchronization
From the first day mobile devices came into existence there was a problem: synchronizing data. People don’t want their contacts on their mobile devices to be different than the contacts on their desktop—or online contacts. People don’t want to edit e-mail on their mobile device and then have to go online to make the same changes. People only want one calendar. If you have a mobile device, you’re going to want a method for all these different sets of data to synchronize so you only have one set of contacts, one e-mail inbox, one calendar, and so forth.

To keep files and data up to date, smartphones and tablets can synchronize, or sync, with cloud-based servers over the Internet or with local machines. These files and data include personal documents, Internet bookmarks, calendar appointments, social media data, e-books, and even location data. Older devices, such as BlackBerry and Palm Pilot, had a specialized sync program you installed on your computer to sync contacts, calendars, and so on. Today’s devices sync through the cloud or optionally use a dedicated program.

Various mobile devices sync differently, depending upon the device vendor and software required. iOS/iPadOS devices use Apple iCloud to sync iPhones, iPads, and Macs via the cloud. Android devices can use Google’s many services to sync certain configuration settings, apps, photos, texts, and so on. In some cases individual apps will synchronize directly; for example, a podcast app might synchronize data such as subscribed shows. Older versions of iOS needed to sync to a laptop or desktop computer via Apple’s iTunes application. While this is still fully supported, most users will just let iCloud handle everything in the background.



EXAM TIP   Synchronization enables mobile devices to keep up to date with a lot of essential information. You should know the types of data typically synced, including contacts, e-mail, photos, and calendar information for the exam, and other types of data to be a great tech. It’s a lot. You can do this!

Synchronize to the Automobile
Automobile makers know you will talk on the phone while driving. While inherently dangerous—a good conversation can distract you from surroundings, including other 3000-pound death machines—everyone does it. Modern automobiles come equipped with voice communication systems, hands-free calling that uses your smartphone via Bluetooth (see Figure 24-34). Synchronizing to the automobile enables voice-activated contact calling, among other things, and often hooks up with a car’s navigation system to help you get from point A to point B.



Figure 24-34  Calling via an iPhone using a car’s built-in entertainment system

Exchange ActiveSync
Exchange ActiveSync (EAS) is a Microsoft protocol used to synchronize Microsoft Exchange e-mail, contacts, and calendars that has become widely used across a range of mobile OS platforms and hardware vendors, including Apple and Android devices. It was originally developed as a synchronization protocol for Microsoft Exchange corporate users, but has evolved over time to include more device control and management features. EAS not only has the capability to set up and configure network connectivity and secure e-mail options for clients that connect to Microsoft Exchange corporate servers, but also has the capability to control a much wider range of functions. Some of these functions include the ability to set password policies, remotely wipe or lock a mobile device, and control some device settings.

Synchronization Methods
In the old days, mobile devices were synchronized to a desktop (uphill, both ways, in the snow!), using a specific type of synchronization software provided with the device. Also, the type of data was typically limited to contact information, but we liked it because it was all we had. Now, there are newfangled ways you can sync device contacts, media files, and even apps. You can also get updates and patches from the device manufacturer by syncing your device.

With faster cellular and Wi-Fi networking technologies, you can skip the desktop and sync even large amounts of data to the cloud. Each phone vendor has its own cloud technology that can tie to your user account and store personal data from your mobile device. Apple has iCloud, Microsoft has OneDrive, and Google has Google Drive, as do some of the individual manufacturers that make Android devices.

There are also independent cloud providers that enable you to store your personal data, and even share it with others. Dropbox is a prime example of this type of provider, although there are many others. Most cloud storage services require you to set up security measures to protect your data, such as requiring a username and password for authentication. Some cloud providers also allow you to encrypt data stored in their cloud.

Synchronizing your data to a personal computer (or laptop) has both advantages and disadvantages. Some advantages of syncing to a personal computer are that you can be in full control of storing and protecting your own data, encrypted any way you choose, and can also move it to portable storage in case you need a backup of it later. A disadvantage is that you must be able to connect to your computer—a small problem if you can’t bring it with you.

Syncing to the cloud also has its advantages and disadvantages. If you have a good cellular or wireless signal, you can sync from anywhere. You do have to be careful of syncing over insecure public wireless networks, however, since there is a possibility that your data could be intercepted and read over these insecure networks. Another disadvantage of syncing to the cloud is that once your data is in the cloud, you no longer fully control it. You are at the mercy of the security mechanisms and privacy policies of your provider. You have to accept whatever security mechanisms they use, such as encryption strength (or lack thereof), and you have to abide by their privacy policies, which may allow them to turn your data over to other companies for marketing, or even to law enforcement. Additionally, some cloud providers may limit the type and amount of data you are allowed to store in their cloud. These restrictions are typically in place to prevent software, movie, and music piracy.

These are all considerations you’ll have to think carefully about when choosing whether to sync to the desktop, the cloud, or both.



EXAM TIP   The CompTIA A+ 1102 objectives cover synchronization extensively, and this overlaps with an 1102 objective, single sign-on (SSO). Be aware that a properly coded application on a modern mobile device can enable you to log in with one of the other accounts you’re probably already logged into, such as Google, Apple ID, Facebook, Twitter, etc. The process for using your active authenticated session with one of these common services to sign you into other services is called single sign-on (SSO). This may come up on the 1101 exam in the context of mobile device synchronization or on the 1102 exam in the context of single sign-on.

Synchronization Issues
The most common synchronization issue is a connectivity, device, or remote infrastructure problem that leaves data partially synced. A partial sync could result in incompletely downloaded e-mail or even duplicate messages as the device tries over and over to successfully sync, repeatedly downloading the same e-mail messages. A device may attempt to sync to download an OS patch or update and may fail. The most likely culprit is connectivity issues with Wi-Fi or cellular connections, and the problem can usually be resolved by moving the device to an area with a stronger signal. This doesn’t prevent upstream connectivity issues, which may also have to be examined.

There are other problems that prevent synchronization, including authentication issues, OS version issues, or incorrect configuration settings. If a device won’t sync even after getting it to a stronger, more stable connection, these are some of the things you should examine. Another problem may be the remote end of the connection. This may be the enterprise e-mail server, or even the entry point into the enterprise network. Failure to properly authenticate or meet the requirements of the entry device may prevent a device from synchronizing.

Another issue you may want to examine when you have synchronization trouble is that multiple sources may be trying to sync the same data. A device can synchronize from an enterprise app store, for example, as well as the vendor app store; personal e-mail services, such as Gmail and Yahoo Mail; and even from third-party providers of “whatever-as-a-service” and cloud storage. This could be as simple as a configuration change you had to make for one service preventing another from working—or the sources might be independently trying to sync different data to the same location. In the enterprise environment, it’s the mobile device management team’s job to put together a management and technical strategy that will ensure minimal conflict between different synchronization sources.

Account Setup and Management
If you or someone you know uses mobile devices for work, you’ve most likely done or at least seen some form of account setup or management. Most productivity apps, like Microsoft 365, Google Workspace, and Apple’s suite of apps that use iCloud, are designed to be synchronized across multiple devices. This means that the document you were reviewing or the e-mail you were carefully writing on your laptop before you had to leave for an appointment can be paused, synchronized, and resumed on another computer or, you guessed it, a mobile device. This sort of cross-platform synchronization has become essential to businesses and it’s going to be something you’ll encounter on the CompTIA A+ exam, as well as on the job in IT.

The big question you probably have now is about how to synchronize these accounts. In this regard, mobile devices work mostly in the same way as a desktop or a laptop. The mobile versions of productivity apps generally mimic most of the functionality of their desktop counterparts, with optimized user interfaces to account for things like the smaller display, touchscreen, screen rotation, and other mobile device characteristics. They’re also optimized to make it as easy as possible to synchronize. In many cases, it’s as simple as installing the mobile version of an app like Microsoft 365, entering the e-mail and password associated with the account, and waiting a few seconds until your Teams chat or Outlook e-mails are available to you on the go.

Most of these apps give users or administrators the ability to make adjustments, including to synchronization settings. Some device synchronization settings may, for example, cause your device to save things you’re working on in local storage. If this happens, you may be happy about it, or you may wonder why your smartphone suddenly started displaying a notification that your storage is full. You may also notice that your accounts aren’t synchronizing. In this case, one of the first places you should look is your account settings; the fix may be as simple as turning on synchronization in your mobile app.

Mobile Device Communication and Ports
Mobile devices wouldn’t be nearly as useful if they didn’t have ways to interconnect with the outside world. This section looks at the many technologies and connections mobile devices use to get data flowing to the Internet and other devices.

MicroUSB/MiniUSB
If you have an Android device made before 2017, it’s very likely it has either a micro- or mini-USB port to charge, connect to laptops or desktops, and sync between those devices. MicroUSB or miniUSB connectors were standard on most Android devices. That’s not to say that you won’t be able to find devices using proprietary connectors; Google makes the OS available to multiple device manufacturers, and some manufacturers do maintain a proprietary connector.

Lightning Connector
With the iPhone 5, Apple introduced its most recent proprietary connector, known as the Lightning connector. It replaced the older 30-pin dock connector that Apple used on previous iPhones and iPads. The Lightning connector is an 8-pin connector (see Figure 24-35) that can be inserted without regard to proper orientation; in other words, it’s not “keyed” to insert a specific way (such as right-side up or upside down, as traditional USB connectors are) into the device.



Figure 24-35  Lightning connector



NOTE   Earlier-model iPads made use of the Lightning connector, but in 2018, Apple released the first USB-C iPad Pro. Since then, Apple has gradually transitioned its various other iPad models, like the Air and Mini, to USB-C. You’ll only find Lightning connectors in use on older models, or the basic iPad still sold by Apple at the time of writing.

The proprietary nature of the Lightning cable means it’s more expensive than a normal USB cable. It is licensed to other manufacturers through the Made for iPhone (MFi) program, but to prevent widespread production of fake Lightning connectors by unlicensed manufacturers, it contains a small chip that identifies it as a true Lightning connector, and cables without that chip typically won’t work or will only have limited use.



NOTE   The Apple Lightning standard is the epitome of proprietary vendor-specific ports and connectors. Only iOS devices use Lightning for communication and power. Android devices typically use industry-standard, vendor-neutral ports and connectors.

USB Type-C
USB Type-C (see Figure 24-36), the newest iteration of USB connectors, is quickly becoming the de facto standard port on Android devices today, which is awesome because you can use one charger for your laptop and phone. As we touched on earlier, Apple has gradually adopted USB-C for its iPad lineups since 2018 due to its compatibility with a huge number of peripherals and its higher power handling that provides faster charging.



Figure 24-36  USB Type-C connector

Like the Lightning connector, the USB Type-C connector is not keyed, allowing it to be inserted right-side up or upside down. It can (but doesn’t have to) support USB 3.1 technology with very fast data transfer rates of up to 10 Gbps. Don’t assume Type-C is synonymous with a specific version of USB—some devices using a Type-C connector are using it with USB 2.0.



EXAM TIP   You will likely see micro- and mini-USB, USB-C, and Lightning mobile device connection types on the exams. Know their characteristics and differences.

Bluetooth
While we discussed Bluetooth at some length, including configuring and pairing, in Chapter 20, let’s review an outline of how the process will work on a mobile device. You can pair a Bluetooth device with a mobile device using a simple process that begins with enabling Bluetooth on the mobile device (if it isn’t already enabled). Steps vary, but you can accomplish this in the quick settings menu or the full device settings menu. Next, power on the other Bluetooth device (or ensure Bluetooth is enabled if the device is already on). Return to the mobile device to discover and select the Bluetooth device for pairing, and then enter the appropriate personal identification number (PIN) code (see Figure 24-37). To add Bluetooth speakers, for example, the smartphone or tablet will display a set of characters for you to type on the keyboard. Once you type in the PIN code, the devices connect.



Figure 24-37  Prompting for PIN



EXAM TIP   Not all Bluetooth pairings require a PIN code, but there’s always some kind of pairing action to perform on both devices.

Always remember to test the connectivity between a mobile device and a newly added Bluetooth accessory. If you’ve added a speaker, open up your favorite music app or podcast and tap play to make sure it works.



EXAM TIP   Most mobile devices have Bluetooth discovery disabled by default to conserve battery life. An active search for devices to pair with uses electricity, as does completed pairing, so use Bluetooth only when you need to use it and be prepared for the battery hit.

NFC
Near Field Communication (NFC) uses chips embedded in mobile devices that create electromagnetic fields when these devices are close to each other. The typical range for NFC communications is anywhere from a very few centimeters to only a few inches. The devices must be very close to or touching each other, and can be used to exchange contact information, small files, and even payment transactions through stored credit cards using systems like Apple Pay and Google Pay. This technology is seeing widespread adoption in newer mobile devices, as well as the infrastructures and applications that support them. Tap pay devices are increasingly common, using NFC and your phone so your credit cards stay in your wallet or purse.

Magnetic Readers and Chip Readers
Merchants can attach a magnetic reader or a chip reader to a smartphone to enable very quick credit card transactions via the cellular network. Vendors appreciate the portability of credit card readers, for example, which take credit card payments from a mobile device for goods and/or services rendered (see Figure 24-38). It’s not unusual to see a food truck use a portable credit card reader plugged into the headphone port on an iPad, or being used at the Texas Renaissance Festival to take the Totalsem crew’s money when they dressed up and went to play (see Figure 24-39). Cheers!



Figure 24-38  Magnetic credit card reader attached to smartphone



Figure 24-39  Totalsem crew at the Texas Renaissance Festival

Infrared
Now largely replaced by other, faster technologies, such as Bluetooth and 802.11 wireless, infrared (IR) was previously used to transfer data between mobile devices, such as laptops and some older PDAs. Infrared was used to create the first real personal area networks (PANs). Infrared uses the wireless Infrared Data Association (IrDA) standard, and at one time was widely used to connect devices such as wireless remotes, printers, wireless mice, digitizers, and other serial devices. IrDA requires line of sight, meaning that devices have to be directly facing each other, requires very short distances (sometimes inches) between devices, and has very slow data rates.



EXAM TIP   You may have noticed that CompTIA included serial interfaces on the A+ 1101 objectives. A serial interface is a connection that sends data one bit at a time. The venerable RS232 port found on legacy devices is one example, but infrared is also a type of serial interface. You can also get adapters to convert another port into a serial port, and these exist for many different types of devices. Keep all of these possible types of serial interfaces in mind because you may see them on the exam.

Hotspots and Tethering
A mobile hotspot is a small device that shares access to cellular technologies such as 4G, 4G LTE via Wi-Fi, and 5G. Most of these devices can be purchased from wireless providers such as Verizon, Sprint, AT&T, T-Mobile, or other carriers, and are usually specific to their type of broadband network. A mobile hotspot is basically a wireless router that routes traffic between Wi-Fi devices and broadband technologies, providing wireless access for up to five to ten devices at a time.

Depending upon the carrier, many cellular phones, as well as tablets, can act as portable hotspots. You’ll recall this from Chapter 21. When used in this manner, it’s called tethering to the cell phone. While some devices configured as hotspots can use your existing data plan with your carrier, some carriers separate out and limit the amount of data that can be used for tethering.

To configure a device as a hotspot, you typically enable its cellular data connection and turn on an additional hotspot setting that causes the device to broadcast a Wi-Fi network. Now the mobile device serves as a router between the cellular network and the traditional Wi-Fi network it is broadcasting. Then any devices that you wish to tether to the hotspot simply see the device as a wireless router. You can also configure a password so that not just anyone can connect to the hotspot. Figure 24-40 shows a screenshot of an Android phone serving as a portable hotspot.



Figure 24-40  An Android phone acting as a portable hotspot

Accessories
Mobile device accessories come in a wide variety of types, packing a huge range of features. Some of the most common accessories that people want for their mobile device, particularly smartphones and tablets, include devices that wirelessly connect to them, typically using Bluetooth technologies. It’s not unusual to find Bluetooth headsets and high-quality external speakers for users to listen to music and chat with friends.

Game controllers, including gamepads and other accessories that plug into tablets via a USB port or connect via Bluetooth, are also common, effectively turning tablets into full-scale gaming platforms. Additionally, cloud gaming has started to materialize as a viable option, and people are now able to use some mobile devices to stream their console and PC games and play on the go.

One feature that some Android mobile devices offer is the ability to use removable external storage, such as miniSD or microSD memory cards, effectively upgrading the storage capacity of the device. This is something Apple hasn’t embraced with its devices, and in fact has become less common with Android devices as well.

There are also accessories no mobile device user should be without, including an external power bank or a phone or device charger. To recharge mobile devices, device chargers either plug into a wall outlet and the mobile device, or plug into a computer and the mobile device, while power banks are just portable batteries that you can charge up and plug your phone or tablet into to get some extra juice when you don’t have the ability to plug into the wall.

Some chargers don’t require connection to the device at all; they simply require you to lay the device on top of a special pad that recharges the battery wirelessly. Specifics differ a little depending on whether the device was designed for wireless charging or the capability is being added with an aftermarket kit—but in either case the pad creates an electromagnetic field for transmitting power to an antenna in the device. Despite being a wireless technology, the range is measured in centimeters and charging works best when the mobile device is on the pad.

The marketplace has settled on the Qi (pronounced “chee”) standard from the Wireless Power Consortium (WPC) as the wireless charging standard of choice. Apple’s 2017 decision to adopt the Qi standard and become a member of that consortium sealed the fate of early rival standards. Apple has even expanded wireless charging functionality to include power banks for some iPhone models.

Some devices also have specialized accessories, including docking stations (much like the docks discussed for portables in Chapter 23). Although these docking stations are typically used for tablets, they are also used for credit card readers.

Another important accessory is a case for the device. These include an almost unimaginable variety of designer cases, as well as hardened cases designed to withstand falls and other impacts. There also screen protectors—protective covers—that range from flimsy plastic all the way to hardened glass that can protect a mobile device screen from scratches and impact. You can find cases made of plastic, leather, rubber, wood, metal, and unicorn horn. Some of these cases are even waterproof, allowing the more adventurous folks to take their phones with them while they are diving in oceans or river-rafting.

We’ve covered only a few of the hundreds of accessories that are available for mobile devices. Many accessories also come with apps to help control or get the most out of the accessory.

Chapter Review
Questions
1.   Which of the following is used in mobile devices to convert analog video and sound to digital video and sound?

A.   Calibrator

B.   SDK

C.   Virtual assistant

D.   Digitizer

2.   John has a high-resolution image on his iPad of his two-year-old son and the family dog. The image initially displays smaller than the screen, so he wants to zoom in to get the details of his son’s expression. What gesture can he use to accomplish this task?

A.   Click the mouse in the middle of the picture to select it, then use the scroll wheel on the mouse to zoom in.

B.   Tap the picture with his index finger on his son’s face.

C.   Long-press on the image and select zoom from the pop-up menu.

D.   Touch his son’s face on the screen with his thumb and finger, then pinch outward to scroll in.

3.   Which mobile device screen technology uses no backlight?

A.   BYOD

B.   LCD

C.   LED

D.   OLED

4.   What can a government use to determine your location at a specific time as long as you’re using your mobile device?

A.   Multifactor authentication

B.   Geotracking

C.   Google Earth

D.   Authenticator applications

5.   What are the steps involved in pairing a Bluetooth speaker with a tablet?

A.   Enable Bluetooth on the tablet; turn on the Bluetooth speaker; find the device with the tablet; enter a PIN code or other pairing sequence.

B.   Turn on the Bluetooth speaker; find the device with the tablet; enter a PIN code or other pairing sequence.

C.   Search for the Bluetooth speaker from the tablet; select pair from the options to enable the speaker.

D.   Enable Bluetooth on the tablet; turn on the Bluetooth speaker; find the device with the tablet; select pair from the options to enable the speaker.

6.   Which of the following connectors is unique to Apple devices?

A.   Lightning

B.   USB-C

C.   Molex

D.   USB-A

7.   John returned from a cruise to the Bahamas and got a bill from his cell phone company (Sprint) that was over $1000. What could have happened?

A.   John connected to the Internet with his smartphone using the cruise ship company’s Wi-Fi.

B.   John’s smartphone connected to the Internet in the Bahamas via a cell provider that wasn’t Sprint.

C.   John used his smartphone to do Internet gambling, and Sprint frowns on that activity.

D.   Bills after international trips are always reported in the currency of the country visited. When translated from Bahamian dollars to U.S. dollars, the amount is the same he normally pays.

8.   Leonard just purchased a very expensive comic book and paid for it using the stored credit card information on his smartphone. What technology did he use to make the transaction?

A.   Swipe lock

B.   Wi-Fi calling

C.   NFC

D.   BitLocker To Go

9.   What information do you need to connect an Android-based tablet to an IMAP account?

A.   POP3 server DNS name

B.   Username and password

C.   Username, password, sending and receiving server addresses

D.   Exchange server name, username, and password

10.   Which mobile OS enables device manufacturers to customize it to better suit their specific devices?

A.   Android

B.   Blackberry

C.   iOS

D.   iPadOS

Answers
1.   D. Digitizers are used in mobile devices to convert analog video and sound to digital video and sound, or to interpret analog signals associated with touch movement on a screen into digital equivalents.

2.   D. John should touch his son’s face on the screen with his thumb and finger, then pinch outward to zoom in.

3.   D. OLED technology does not use a backlight.

4.   B. Geotracking can locate you and your GPS-equipped mobile device.

5.   A. To pair a Bluetooth speaker with a tablet, enable Bluetooth on the tablet, turn on the Bluetooth device, find the Bluetooth device in the tablet’s settings screen, then enter a PIN code or finalize the pairing.

6.   A. Lightning connectors are an Apple proprietary connector type developed to be used with Apple’s mobile devices.

7.   B. John’s smartphone connected to the Internet in the Bahamas via a cell provider that wasn’t Sprint, causing him to incur high data roaming charges.

8.   C. Leonard likely purchased his comic book using Near Field Communication (NFC) technology, which can be used for payment transactions through stored credit card information in mobile applications.

9.   C. To connect an Android-based tablet to an IMAP account, you need a username and password and the sending and receiving server addresses.

10.   A. Google Android is open source, enabling manufacturers to make modifications to better suit their specific devices.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 24 Mobile Devices
Chapter 25 Maintaining and Securing Mobile Devices
Chapter 26 Printers and Multifunction Devices
42h 21m remaining
CHAPTER 25
Maintaining and Securing Mobile Devices
In this chapter, you will learn how to

•   Troubleshoot common mobile device and application issues

•   Explain basic mobile device security

•   Describe typical mobile OS and application security issues

Mobile devices are packed with tightly integrated hardware, aren’t designed to be upgraded by their users, and come with mobile-oriented operating systems. Because of these major differences, the troubleshooting and security practices for mobile devices differ a lot from those for desktop computers, and somewhat from those for other portable devices. This chapter explores general troubleshooting of mobile devices and their apps first, then covers security features and capabilities of devices common in the mobile market. The chapter finishes by jumping into preventing, detecting, and addressing security issues with mobile operating systems and applications. CompTIA loves those performance-based scenario questions, so get ready for some real-world issues when it comes to security and application troubleshooting.

1101/1102
Troubleshooting Mobile Device Issues
The CompTIA A+ exam objectives divide mobile device problems into two groups: general issues with mobile device hardware and software (1101 exam), and security issues (1102 exam) with the mobile OS and apps. In this section we’re going to cover tools for troubleshooting general hardware, OS, and app issues, and apply these tools to common problems. These common problems happen across all varieties, types, and manufacturers of mobile devices. This chapter includes references to Apple’s iOS and iPadOS, as well as Google Android. We talked about the differences between iOS and iPadOS in Chapter 24, and while they are very similar, there are some areas where troubleshooting may differ, so keep both their similarities and differences in mind.



NOTE   Few mobile devices have components you can service in the field. In the event of a hardware problem, send the device to a service center for repair. Companies like iFixit (https://www.ifixit.com) are making some components field-replaceable, but usually only for skilled techs.

Troubleshooting Tools
Because mobile device hardware typically can’t be repaired or replaced by a user or field tech, mobile device troubleshooting focuses on ruling out software issues. The few things you can try are common to almost all mobile devices, and it’s best to start with ones that inconvenience the user least. Sometimes these tools will fix the problem, but other times they’ll just restore normal functionality until the problem recurs, or help you rule out causes.

Just because you’ll troubleshoot a mobile device a little differently doesn’t mean you should throw out what you already know. Reflect on the troubleshooting methodology covered in Chapter 1, and use the troubleshooting tools you learn about here to help you work through that process. If the troubleshooting process doesn’t fix the problem or identify a cause you can resolve in-house, the next step is to take or send the device to an authorized service center.

Keep in mind that the steps you’ll need to take to perform any of these operations will depend on the specific device, its operating system, and the OS version. Be prepared to consult manufacturer and OS resources for exact steps. Let’s dive in.



NOTE   Most of these tools either are guaranteed to erase data and customizations or have some risk of doing so under the right circumstances. Remember to communicate with the device’s user what steps you’ll be taking, including what kinds of data loss it can entail, and give the user a chance to back up his or her data.

Try This!

Practice on the Real Deal

If you have access to a smartphone or tablet, practice getting to the tools used for troubleshooting mobile devices. You’re going to read about a bunch of places to adjust things such as screen brightness, close or uninstall apps, and much more. Access the device’s Settings and explore. Just don’t do anything specifically to any device without proper permissions.

Check and Adjust Configuration/Settings
Modern mobile operating systems have tons of configurable settings, as do many of the apps users install on them. Always be on the lookout for “problems” that sound a lot like a simple configuration issue and investigate these early if they seem likely. It won’t cost you much (except time) to check relevant settings, but it might save you from having to perform later steps that require backing up and restoring user data.

If the issue isn’t likely related to configuration, save your time and revisit configuration after you’ve tried rebooting the device, which we’ll discuss in the upcoming “Soft Reset” section; you don’t want to waste tons of time toggling settings if a reboot could fix the problem. If you find a setting that doesn’t seem right and want to see if a change resolves the issue, make sure to keep track of what you changed and what the previous setting was!

Close Running Apps
All of the mobile operating systems provide at least one way to close running applications—the most common is to swipe the app in a particular direction from the device’s list of recent apps. If you come at this with a traditional mindset shaped by how desktop operating systems work, there’s a chance you’ll misunderstand when and why we close mobile apps, so let’s consider a much-simplified version of what goes on under the hood.

On a traditional computer, you open an application when you need it, and it will run until it completes its work, crashes, or you close it. Because mobile devices have more limited computing resources and battery power, you don’t want open apps eating up big chunks of resources and burning power while they aren’t in focus or the device isn’t even being used. To address this problem, modern mobile OS versions manage running apps to optimize performance and battery life.

The catch is that the way they manage apps makes the term “running” a little slippery. While your current app may be running in the traditional sense, the various processes that power your recent out-of-focus apps may keep running if they have work to do, be cached until you return to the app, or get killed if the OS needs its resources for other apps. For the most part the OS will do a good job of managing well-designed apps, but you may still need to close an app if it has frozen, begins to malfunction, or you suspect it is causing the device to misbehave.



NOTE   When closing an app, keep in mind that the user may lose unsaved data when you close it, and (depending on the app) that their device may lose certain functionality they expect it to have until the app is restarted.

Some apps may (intentionally or accidentally) leave background processes running even after the GUI has closed. In Android, the Application Manager will let you force stop an app, also killing its background processes (Figure 25-1). In iOS and iPadOS, a swipe will generally do the job.



Figure 25-1  Force stop in Android

Soft Reset
To maintain mobile devices, it’s important to understand the terminology surrounding resets, especially if you’re coming at this from a desktop-oriented mindset. On a desktop, you typically initiate a soft reboot from within the operating system or trigger it by pressing a button dedicated to restarting the system; the hallmark of a soft reboot is that the machine never powers all the way down. In contrast, you can perform a hard reboot by holding down the system’s power button for several seconds until it turns completely off; you don’t want to reboot this way if you can avoid it, but you’ll need to if the system is frozen.

On mobile devices, the term soft reset describes restarting the device, whether you do it from within the OS or with hardware buttons on the device. If the device still won’t restart, confirm the soft reset procedure in the manufacturer resources; if you know you’re performing it correctly, and the device allows for it, you can force a device with a removable battery to power down by removing the back cover and the battery.

Much like a reboot on a traditional computer, you can fix all kinds of strange behavior on a mobile device with a soft reset. I’m listening to Spotify on my Android device as I write this section, for example, and when I got started this morning the playback was stopping every few songs; I performed a soft reset and now it’s working fine. The soft reset is the easy reset, but there’s another reset you need to know; we’ll continue this discussion in the “Reset to Factory Default” section coming up in a moment.

Uninstall/Reinstall Apps
Uninstalling and reinstalling apps can be an important troubleshooting process. You can uninstall apps through either the app store they were installed with or the device’s application manager; you can also, of course, reinstall them via the app store. If the user started having trouble shortly after installing a new app, uninstalling it to see if the problem goes away is an obvious way to rule out a potential cause. If they’ve been successfully using the app, make sure to jot down important settings and back up their data if possible before you uninstall it.

The problems you can fix or troubleshoot by uninstalling and reinstalling aren’t always as obvious as this. If a user has had an app for a long time and it only recently started acting up, it’s possible the app’s developers released a bad update; after a bad update, the app might not work at all, or it might work fine if you uninstall and reinstall it. Sometimes this can be a no-win situation for a tech—what if the only fix to a user’s problem is removing an app they use daily until its developers fix a problem?

Reset to Factory Default
This other reset—known by many names such as hard reset, factory reset, or reset to factory default—will clear all user data and setting changes, returning the device (well, its software) to the state it was in when it left the factory. Take extra care not to confuse a hard reset with a hard reboot; if you’re reading documentation or a how-to page that uses the terms reboot and reset interchangeably, pay close attention to what the author intends you to do—and consider finding a less-ambiguous resource.

Because the hard reset removes all of a user’s data and settings changes, it’s the most disruptive option here—typically one you won’t perform until after backing up the user’s data (which we’ll discuss later in the chapter). The big exception is when you’re intentionally performing a factory reset in order to clear user data off a device before it is sold, recycled, or assigned to a new user.

Despite the inconvenience, resetting a device to factory defaults is an important troubleshooting step on the way to determining whether it should be sent to a service center. If a factory reset fixes the device’s issues but they return some time after restoring a backup of user data and programs, return to earlier steps for tracking down the troublemaking app.

Touchscreen and Display Issues
Modern mobile devices are almost all screen, and some provide little beyond a touchscreen and a power button for interacting with the device. While display issues tend to be urgent for most devices, the touchscreen’s integral role in controlling a modern mobile device makes it all the more so. We already touched on some important steps for troubleshooting a touchscreen in the “Input Problems” section at the end of Chapter 23, so be prepared to integrate those steps with the more mobile-centric issues discussed here.

Dim Display
Mobile devices have a brightness control that can be set to auto mode or controlled manually. These settings don’t always work perfectly, and sometimes apps that need special control over brightness settings can cause the device’s display to be too dark or bright for the user’s comfort.

A dim display might be a sign that there’s a problem with the panel, but first you need to check the display settings. Turn off any auto-adjustment setting and manually change the display brightness from the dimmest to brightest setting and observe whether it covers an appropriate range of output. If it doesn’t, there may be a problem with the display panel; if it does, there may be something keeping the auto-adjustment from working right.

The auto-adjustment is affected by how much light a sensor or camera on the front of the device can detect. Make sure the sensor isn’t covered with dirt or some other obstruction. If the display is too bright in a dim room, check the surroundings for bright light that isn’t close enough to illuminate the area, but that the sensor might pick up if pointed in the right direction.

Be on the lookout for apps that tinker with the display’s brightness. These apps may use distinct brightness settings, or they may modify system-wide brightness. Reading apps, like Amazon Kindle, are one example. See if a soft reset returns the display to normal operation, and then investigate whether using these apps causes the brightness issue to return. Every once in a while, Kindle on my Android tablet will interfere with the system’s auto-brightness, causing all sorts of strange brightness changes until I restart the tablet by performing a soft reset. The solution in this case may be as simple as teaching the user to reset their device when an app like this has caused a problem.

Autorotation Problems
Much like brightness controls, mobile devices also have automatic and manual controls for rotating the screen. The autorotate mode uses the device’s accelerometer to change the screen between portrait and landscape orientations when the user rotates the device. When the screen does not autorotate, usually either autorotation is off (the screen orientation is locked) or the app currently being used does not support both portrait and landscape orientations, which is necessary for autorotation to work.

You might also run into an autorotation problem caused by OS, resource, or hardware problems on the device. If autorotation doesn’t work after a soft reset, you may need to wait for an OS update or take the device in for service.

Touchscreen Responsiveness
When a user tries to interact with a mobile device but finds the touchscreen nonresponsive or gets an inaccurate touchscreen response, there are a few simple things to rule out first: dirt, accidental touches, and performance issues. Any of these can cause digitizer issues (we talked about what a digitizer is in more detail in Chapter 24), some of which can be resolved quickly, others require specialist diagnostic and repair. With those out of the way, we’ll turn to more catastrophic causes.

Accidental Touch  The simplest issue to resolve is an accidental touch. Sometimes a user will hold a device in such a way that its touchscreen detects some part of their arm or hand as an intentional touch, and it may not react at all when they try to manipulate it intentionally. Oversensitive sensors or bad design might exacerbate this, but the fix is always the same: show the user how the sensors pick up an accidental touch and teach them how to hold the device to avoid them.

Dirty Screen  Another simple issue to resolve is a dirty screen. Sometimes simply wiping the touchscreen down with a dry microfiber cloth to get rid of fingerprints, dust, dirt, grease, and other foreign objects will fix a responsiveness problem (see Figure 25-2).



Figure 25-2  Cleaning a smartphone

Performance Problems  Much like a mouse cursor may slow, freeze, or move erratically when a traditional computer is having performance issues, a touchscreen may appear not to work at all or have severe accuracy and response problems if the mobile device is performing poorly. Be patient with the device and look for signs it is struggling to keep up. Is it displaying the right time? If it has an animated lock screen or wallpaper, are the animations playing smoothly?

If the device appears to have network connectivity, are weather or stock widgets on the lock screen updating? Is it slow to respond when you press unrelated hardware buttons? If the device can receive them, see if it responds normally when you call or text it. If the problem seems to be performance related, perform a soft reset and see if the touchscreen starts working.

A lot of users add a screen protector to their mobile devices to give a little extra help in case of a drop. A poorly installed screen protector can cause touchscreens not to work properly. Check the guidelines from the manufacturer and remove and replace a subpar screen protector.

Calibration and Diagnostics  If a soft reset doesn’t get the touchscreen working, look online for information about whether the device has a hidden diagnostics menu or service menu. You might reach this menu by inputting a series of digits into the device’s dialer, or by holding specific buttons while the device is booting up during a soft reset. If the device has a touchscreen diagnostic here, it should help you decide whether the touchscreen itself is in good working order. Some Android devices may also have a setting in either the primary OS settings menu or a hidden device menu for calibrating the touchscreen.

Physical Damage  While we covered the previous issues when we discussed portable devices in Chapter 23, smaller mobile and wearable devices have a greater risk of some problems that are rarer with larger portables. Everyone knows a quick dip in a toilet, margarita glass, or swimming pool can kill a mobile device, but sometimes getting one wet or dropping it on a hard surface can cause trouble short of complete death. A smartphone in your pocket when you get caught in the rain, or on a table when you spill a drink, could end up with liquid in all sorts of nooks and crannies.

Although some mobile devices can handle a little bit of moisture, most can’t handle immersion at all. Dropping a smartphone in a toilet makes for a very bad day. Without removable batteries, there’s not much you can do to save a liquid-soaked mobile device, and as a result, this level of liquid damage is often a death sentence for mobile devices.

If you rule out the simplest explanations and fixes in this section and the touchscreen is still not responding properly, it’s time to inspect the device for evidence it has been dropped or gotten wet. There’s always the old-fashioned way—ask the user. Just be aware that it may be hard to get someone to admit their touchscreen stopped working after they sprayed milk through their nose because they tried to read XKCD while eating breakfast.



NOTE   For a good dose of tech-oriented humor, check out the comics at https://xkcd.org. Geeky fun at its finest!

A broken screen doesn’t require the glass itself to be cracked; drops or impacts can break internal connections, rendering the device difficult or impossible to use. Moisture can cause internal shorts, and lingering liquid could cause sensors to behave in really strange ways. Most mobile devices will contain a few liquid contact indicator (LCI) stickers that change color when exposed to water, as shown in Figure 25-3. While these are really so the carrier or manufacturer can refuse to cover water damage under warranty, look up their locations online and then check them on the device. There’s often one on the battery or in the battery compartment, if it’s accessible; it’ll usually be white if it hasn’t gotten wet.



Figure 25-3  Pristine LCI sticker (top) and LCI sticker absorbing a drop of water (bottom)

Apps Not Launching
A mobile device app may fail to launch or install correctly for a few reasons. First, the app may not be compatible with some combination of the mobile device’s hardware, operating system version, or vendor/carrier customizations to the OS. With Android devices, for example, different manufacturers can tweak the OS to suit their own needs, which may cause compatibility issues with other vendors’ apps.



NOTE   This section details reasons an app may always fail to launch or install correctly. Remember, an app may fail to install or launch correctly before you perform a soft reset, but do so fine afterward. Perform a soft reset and then try reinstalling and launching the app.

Another reason an app may not launch is that the device doesn’t meet the app’s hardware requirements. These might be more traditional requirements such as amount of available RAM, storage space, and processor type, but the app might also require a sensor or radio your device lacks or requires capabilities that your device’s camera doesn’t support. It’s always a good idea to review an app’s requirements before installing it (or when you run into trouble).

Both Apple and Android devices track errors with applications. You’ll need third-party tools to access app log errors—or what I assume are logs of app errors (thanks, CompTIA!). Something to keep in mind if a senior tech or app programmer (in the case of custom apps for an organization) needs help with troubleshooting.

Overheating
Just as with the portable devices discussed in Chapter 23, overheating can cause permanent damage to a mobile device; most of the recommendations given there still apply. That said, our relationship with mobile devices is a little different. They are usually on, spend more time in our hands and pockets, and we take them places we wouldn’t dream of taking a larger portable. A mobile device is more likely to get left on the car seat on a hot summer day or be nestled close to our body in well-insulated winter clothing.

Focus on overheating as a combination of the heat a mobile device produces itself, heat added to it by external sources like the sun or a lamp, and how well its environment dissipates or retains heat. Since we handle these devices more often, we have a lot of chances to notice what’s normal and what isn’t; when a device is hot, combine these three factors and see how well they explain the device’s temperature. The process of looking for a good explanation can help you catch performance problems before they drain the battery, prevent heat damage to components, or identify problems with the battery or power systems before they become dangerous.

Charging, large data transfers, frozen apps, recording HD video, and other intensive tasks can all make a mobile device much hotter than normal; avoid letting the device do intense work in hot or well-insulated spaces. If you can avoid it, don’t bring mobile devices into very hot environments; if you can’t, minimize risk by turning the device off altogether. If the device is hot to the touch in a cool environment, you can put it into airplane mode, close all running programs, and see if it cools down. If it doesn’t, turn it off until it cools and then try again.

Your biggest concerns are a device that overheats for no obvious reason or gets hot enough that it could burn someone. These problems are usually caused by some sort of hardware issue, possibly a defective battery or other power circuit within the device. There’s really not much you can do; turn it off to protect the device from further damage and take it to a service center.

The dangers of not addressing an overheating mobile device—even one that is overheating for otherwise benign reasons—are, at best, an eventual device failure and requisite data loss. At worst, a severely overheating device can become a safety risk with the potential to burn or shock a user and, especially if the battery ruptures, cause a fire or explosion.

Update Failures
Ideas like app stores and regular automatic updates are now common on computer operating systems, but these things cut their teeth in the world of iPhone, Android, and even the failed Windows Phone. Ease of use rules this world, so installing software and updates on a mobile device is dead simple. But don’t think it’s too simple to fail! If you manage enough mobile devices, you’ll see a case where the OS fails to update or an application fails to update.

Usually, the reason an update fails is that the device doesn’t have enough free space to install the update. It might auto-purge some files to make room, but you’ll have to jump in to remove some apps or files (back them up first) if it fails. Corrupt downloads won’t install; check your device’s documentation on how to delete the bad update and retry with a strong connection. Running out of battery mid-update can cause big trouble; it’s best to plug in the device before updating the OS.

Slow Response
Mobile devices can be slow to respond like regular desktop computers and laptops, and often for the same reasons. Response issues can be caused by storage space being almost filled up on a mobile device, making it unable to save data or install apps efficiently. Mobile devices can also be slow to respond when there are too many apps running at the same time, eating up RAM.

Usually, the mobile device’s OS has configuration settings that enable you to stop apps or view their resource usage, including memory and storage space. If storage space is an issue, you may have to uninstall some apps, or reinstall them so that they are stored on removable storage devices, such as microSD or miniSD memory cards.

A device with response issues will often be running hot, and this heat can be a big clue. Use the recommendations in the previous section to evaluate whether the device or the environment is the source of this heat. A hot, sluggish device could be using thermal throttling to protect the device’s CPU from heat damage by reducing its power; in this case, performance should pick up as it cools.

One of the first troubleshooting steps you can take in resolving response issues is to perform a soft reset of the device; this clears running apps—perhaps even ones that are frozen or malfunctioning—from RAM. As far as troubleshooting tools go, you can use the device settings or third-party apps to measure the device’s performance. Sometimes those apps can help point the way to what’s causing the performance problems. If you ultimately determine that a hardware issue is causing performance problems, you should take the device to an authorized repair facility.

Battery Life
Just like the portable devices discussed in Chapter 23, modern mobile devices use Lithium-Ion (Li-Ion) batteries. It’s usually not too hard to make use of a more traditional portable computer while it’s charging, but the ergonomics of mobile devices can make it miserable to use one while it’s charging—so it’s even more important to make sure your device has power when you need it. Our purpose here is to look at how you can manage any battery to get the most out of it, but first we need to talk about the cornerstone of good battery management.

Meeting User Power Needs
Mobile devices are rated in terms of how long their battery should power a device during “normal” use, how long the device can go between battery charges, and the levels of power that both the battery provides and requires in order to charge. Make sure you and your users have mobile devices that have a chance to last long enough to perform normal activities for an adequate amount of time.

The battery life numbers advertised by a device’s maker are a good start, but be suspicious of these figures. Mobile device review sites will benchmark the performance of more popular mobile devices and tell you how long they survived while performing some battery-sucking tasks like playing HD video. Know how long a given user’s device will need to last on a charge, and try to make sure they get a device that can last at least 20 percent longer to account for how the battery’s capacity will dwindle over its lifetime, known as its battery life.

If there’s no existing device that can meet the user’s needs most of the time, make sure they either have a device with a removable battery and a spare or have a portable external battery recharger. You can plug a mobile device into a portable battery recharger (sometimes called external battery, power pack, or portable charger) to recharge when there’s no available outlet.

Managing Battery Life
There are two ways to think about battery life: how long it will last on each charge, and how long the battery can meet your needs before you have to replace it. Luckily, you can optimize both of these at the same time. When you waste battery life on device features you aren’t using, not only will your device need to recharge sooner than necessary, but the extra recharge cycles will also shorten the useful life of your battery, also known as your battery health. Let’s take a look at the biggest battery drains while keeping in mind that these are generalizations: check your device’s battery usage monitor to see what is consuming most of its power.

Display  While it depends somewhat on how big your device’s screen is and what kind of display it uses, the fastest way to drain most modern mobile devices is leaving the screen on. Keep the display off when you can, and use the lowest acceptable brightness setting. Because the screens look so much more vibrant at full brightness, there’s a good chance this will be their default setting. The battery savings from using the lowest setting may be enticing, but the best compromise is usually to configure the device to control brightness automatically. Figure 25-4 displays the battery usage for an iPhone 13 Pro. Notice how much of the battery is being drained by the screen alone!



Figure 25-4  Battery usage for a smartphone

There are more options for optimizing how much power your display uses, though some of these differ by device or manufacturer. You can usually adjust how long the screen will stay on without input, and whether it will turn on when you receive a notification. Some devices have power-saving modes and may even be able to save power by displaying grayscale instead of full color. OLED displays use less power to display darker colors; if your device uses an OLED panel, you can also reduce power consumption by using black wallpapers and configuring apps to use a dark theme if the option is available.

Wireless Communication  To paint with a very broad brush, another big battery drain is the process of communicating without wires. It’s good to keep in mind that every form of wireless communication your mobile device is capable of (such as cellular voice, cellular data, Wi-Fi, Bluetooth, Near-Field Communication [NFC], etc.) corresponds to a radio inside the device. In order to use that type of communication, the radio needs to be on and drawing power. If you aren’t actively using that mode of communication but the radio is on, you’re wasting power. Each communication technology draws varying amounts of energy under different circumstances, but here are two helpful guidelines: searching for signals is power intensive, and your device’s apps will do more work in the background when connections are available.

Especially when traveling outside of populated areas, a mobile device can use lots of power talking with distant towers and base stations; this constant search can significantly drain battery power. You may be able to control this power drain through configuration changes that limit device roaming or searching for new wireless networks, but another approach is disabling these communications technologies until you need them or are back in an area with good coverage. You don’t want to get stuck in the snow on a rural highway only to discover that your phone has almost completely drained its battery searching for cellular signals.

Even when the device maintains a strong connection, it constantly uses power to transmit and receive data. Having the connection available is often worth this slow drain, but beware that some of your apps will lightly sip power while disconnected and burn through much more doing background work when a connection is present. The easy way to rein this in is to disable communication, but the operating system (and sometimes the app itself) will have settings for controlling when an app can send and receive data in the background, and what connections it can use.

Location  While you can apply the same guidelines for managing GPS or location services, some small differences make it worth discussing separately. When location services are on, the device’s apps can query the location of the device. Depending on how you’ve configured the device, it may approximate your location using low-power (less-accurate) methods like nearby cellular and Wi-Fi networks, higher-accuracy (higher-power) methods like GPS, or combine both of these. This could be for apps that require location data in the background, or for active apps, such as mapping software, that use the GPS receiver. The power drain here can vary widely between an app occasionally checking approximate location in the background, and one constantly requesting high-quality updates.

The simplest solution is to keep location services off when they aren’t required, but you may be able to find a happy medium by setting per-app restrictions. When an app requires location data (common examples are apps for navigating, mapping, geocaching, or finding nearby users, restaurants, garage sales, or movie theaters) but location is disabled, the device will usually prompt you to turn it on.

Because apps for which location data is less critical may happily use a stale location, the best combination of trade-offs will ultimately depend on how you use your device and what apps you have running. If you regularly use the device to take location-tagged pictures cataloging graffiti or potholes, you may want the highest quality location data available at all times, regardless of the battery drain. Another tip is to review configuration settings for apps that use location services and disable the ones that don’t need to have immediate location data.



EXAM TIP   Be familiar with the factors that can reduce battery power and battery life.

Charging Issues
Charging a mobile device is one of the most regular interactions a user will have with it. As a result, charging issues can arise, leading to inconvenience and frustration. There are a range of possible causes for improper charging, from something as simple as having too many apps running in the background, all the way to broken hardware in the device. Depending on the source of the problem, the device may charge slowly or not at all. Let’s have a look at some of the main causes, how to identify them, and most importantly, how to fix them.

If your device is charging more slowly than usual, there are a few possibilities. The first thing to check is whether anything is using an unusually high amount of battery. Sometimes, resolving the issue is as simple as closing out of some background apps.

Slow charging can also be caused by issues with your charger or cable. If the charger you’re using wasn’t designed with the device in mind, or you’re just using a cable you grabbed out of a drawer, it may not be able to provide enough power. You’ll know fairly quickly if the phone is charging slowly; most devices display the estimated charging time somewhere, either on the home screen or in the battery menu in Settings. If you encounter slow charging and you’ve ruled out background apps, grab a different charger, preferably one that you know works with the device. If it charges normally, the issue was almost certainly with the charger or cable. If it doesn’t, you may have bigger problems and should look to the device hardware.



NOTE   In Chapter 24 we talked about different types of ports you’ll find on smartphones and tablets. Issues related to charging cables are especially common, particularly for smartphones, because people often use their devices while they are plugged in. The result is that the cables can end up fraying, or the connector can become damaged. If a charging cable that worked well suddenly starts charging slowly, it’s very possible that it just didn’t hold up to the higher amount of wear and tear mobile devices experience. If the cable is micro-USB, the odds of this being the problem are especially high.

If you’ve already ruled out issues with background battery usage, chargers, and cables, it’s time to explore the possibility that the charging port itself has a problem. For example, you may have a physically damaged port. This is the worst-case scenario, because, as we discussed when we addressed field repair, mobile device hardware repair is very difficult without access to specialized tools and parts. If you closed out the extraneous apps, restarted the device, tested a few different charging cables, and the device still won’t charge, there’s really one more thing that you can test before its time to take it to a specialist. It may sound silly but try plugging the charger into a different outlet. I’ve plugged in my charger to one outlet, felt the creeping despair that comes with potential hardware issues, moved it to another outlet, and had the device charge normally. Sometimes the issue isn’t with the device at all. If none of these steps work though, the device may require some form of specialized diagnostic or repair.

Swollen Battery
As we discussed in Chapter 23, one of the more insidious problems you’ll see in mobile devices is a swollen battery. The main cause is overcharging, usually when the circuits designed to prevent overcharging fail. Non-OEM chargers or batteries, especially if they aren’t rated for the correct voltage and wattage, represent an additional risk, as does overheating. Sometimes the battery is just bad. Overcharging has become less common as mobile device manufacturers continue to improve their hardware and implement software that helps to prevent it, but swollen batteries can still be a serious problem.

Prevention may be the best cure. Don’t let batteries overheat, especially while charging. Prefer OEM chargers and batteries. Check the manufacturer’s documentation for specific actions to take or avoid. Regardless, prevention can’t always work, and swollen batteries may rupture, leak, and catch fire. It’s important to be aware it can happen, vigilant for signs it is occurring, and careful when disposing swollen batteries.

Look for subtle clues, like changes in how the device’s frame and screen come together, how it sits on a flat surface, how the back cover sits on the device, weird creaking or popping, inexplicable heat, and so forth. If the device has a removable cover, it’s pretty simple to check the battery. If it doesn’t, you may need to find a service center or a mobile technician who is comfortable taking the device apart to check.

When you encounter a swollen battery, dispose of it according to the recommendations in the “Try This! Recycling Old Portable Device Batteries” section of Chapter 23 and replace it with a known-good battery, preferably from the original device vendor.



CAUTION   You should never try to repair a battery under any circumstances, let alone when it’s swollen, as it can cause bodily harm and damage to equipment.

Random Reboots and Freezes
A mobile device can randomly reboot or freeze up just like a desktop system (and for the same reasons). The main difference is that there aren’t as many ways to successfully deal with a frozen mobile device. In that case, the immediate goal is getting the device back to a usable state. If the device isn’t responding, you’ll need to perform a soft reset, and without access to the OS you’ll have to follow the manufacturer’s steps for performing a soft reset—probably either by holding the power button for a few seconds or removing the battery.



NOTE   When a device seems to be frozen, there’s also a chance the touchscreen just isn’t responding. Check if the device responds normally to hardware button presses or enabled voice and gesture commands before assuming it is frozen.

If the device is still at least partially responsive, you can try to close an offending process from your list of recent apps. Even if you get the app to close, you may find the device unstable again as soon as you reopen the app. It’s often best to save yourself wasted time: close the offending app, save any work in other open apps, and perform a soft reset.

When the device is usable again, there may be more steps to take. If you know the device rebooted or froze when you opened a newly installed or updated app, you may need to uninstall it and consider waiting for an update or looking for a replacement. Sometimes operating system issues can cause reboots and freezes, especially right after a device update, so look for follow-up OS patches correcting these types of issues. If the device randomly (and with increased frequency) reboots or freezes up, whenever using apps performing similar tasks (any app that uses the GPS or camera, for example), then your device likely has a hardware issue and needs service.

There’s also a chance you’ll find that the device is still unusable after the soft reset, in which case you’ll need to look for the manufacturer’s documentation on how to boot the device into any special modes that enable you to either remove an offending app, repair the OS installation, or reset the device to factory default. If this process also fails to render the device stable, you’ll need to send it to a service center.

Cannot Broadcast to an External Monitor
Back in Chapter 24 we saw that some mobile devices have video output that enables you to broadcast the display onto an external monitor or projector. When done correctly, this is usually an almost automatic process: plug some adapter into your mobile device, plug that adapter into your external monitor’s VGA, DVI, DP, or HDMI port, and it all just works.

Well, that’s the theory. In reality, broadcasting your mobile device’s screen to an external monitor is fraught with problems. While these vary by type of device, here are a few tried-and-true things to check when your device cannot broadcast to an external monitor:

•   Is your source correct on the external monitor? All monitors, TVs, and projectors have lots of inputs. Is the external monitor pointing at the right source?

•   Do you have the right adapter for your device? Apple alone has come out with five different types of video adapters in the last few years—and don’t even get me started on the many adapters for Android! Make sure you have an adapter that is known to work for your device.

•   Does your adapter need its own power source?

•   For HDMI: Did the HDMI recognize your device and your external monitor? Depending on the make and model, you may need to reset one or both devices to give the HDMI time to see connections and set itself up.

No Sound from Speakers
Sound issues are also common on mobile devices. The most obvious (and probably most common) is that the volume was turned down or muted through software configuration or an app. This is easy to fix, but sometimes you have to go through many configuration settings for both the device and apps to figure out which one is controlling the volume at the moment or which one may actually be muting the speakers. A device may have separate settings for media, call volume, notifications, and more—and sometimes it’s easy to change the wrong one.

The versatile nature of mobile devices means that we are often switching from one use to another. This can sometimes lead to people forgetting that their device was paired with some peripheral. One of the most common peripherals you’ll see with mobile devices are wireless Bluetooth headphones. If you aren’t getting any sound from the speakers, it may be a good idea to double-check for paired audio devices—the sound may just be coming from somewhere you didn’t expect.

Some mobile devices also have hardware volume controls on them, so check them. If that doesn’t work, then start going into the configuration settings for the device and apps. If none of these steps works, then you may have a hardware issue: the speakers have been damaged or come disconnected inside the device. As with all other hardware issues, you’ll likely have to take the device to a service center for repair.

Connectivity and Data Usage Issues
General network connectivity issues—the kind that can affect all devices—have been covered elsewhere within the book. For mobile devices in particular, you should be aware of some additional network connectivity issues that you will likely encounter at some point. We’ll discuss these in respect to cellular signals, but the first issue applies to Wi-Fi and Bluetooth network connections as well. For the most part you can’t directly fix these connection issues, but you’ll inevitably find a connection issue is responsible for some problem, or at least need to rule it out on the way to the ultimate cause.

One of the most prominent connection issues plaguing mobile devices is weak signal. The signal might be weak because you’re deep inside a building, nestled between skyscrapers, crossing the no-man’s-land between cell towers in sparsely populated areas, or any of a wide array of similar situations. The primary symptoms of a weak signal are dropped connections, delays, slow transmission speeds, battery drain, and frequent indications that the device is searching for a signal.

There isn’t much you can do to troubleshoot a weak signal except monitor it. There are cellular signal boosters you can purchase, but these are of dubious value in some situations. These are most effective when the user is stationary in a location far from the cell tower, and usually aren’t useful while the user is on the move.



NOTE   In addition to signal issues, performance problems on the device itself can cause the symptoms of slow data connectivity. We’ve covered these already, but they include high utilization of resources such as CPU, RAM, and network bandwidth, and a device’s struggle to maintain a solid network connection.

Even if your signal is good, you may still run into connectivity problems—and they may be tricky to spot if you aren’t aware of them. The first of these is an overloaded network, which is common during large public gatherings (such as a sporting event) or a widespread emergency that causes a surge in network use. Your device might have full bars but be unable to place calls, send texts, or transfer data. Another explanation for connectivity problems despite a strong signal are restrictions and limits the carrier enforces. You may experience slow data speeds while roaming just because the carrier of the network you are roaming on limits data rates for nonsubscribers. Exceeding the data usage limits that your carrier sets can also lead to slow data speeds.

The carrier will usually notify the user by e-mail or text message, but the user might not notice. What happens next is up to the carrier and the terms of the user’s plan. Some carriers stop cellular data use beyond the preset limits, bill the user for additional data, or throttle the speed of the connection. Each causes complications, but you can minimize them by recognizing data caps. Configure data hogs like cloud storage apps to synchronize only on Wi-Fi, monitor data use and disable cellular data usage in the configuration settings of the device (see Figure 25-5) as needed, or pay to raise the data cap.



Figure 25-5  Option to disable cellular data in iOS

While the abstract side of data usage limits is important, the essential part is that you think about how these various scenarios could manifest on real devices. If you have a corporate plan, knowing the data limits and what happens when they’re exceeded will give you a big leg up. What should you suspect when a user turns up at the end of the month with a device that suddenly has terrible call quality in Skype while using cellular data but works fine over Wi-Fi? Or a traveling employee says she keeps getting calls from colleagues asking why she hasn’t weighed in on an important e-mail discussion that hasn’t turned up on her device, despite a good connection? A quick check to see whether the user is over the plan limit could spare both of you hours of troubleshooting.

GPS and Location Services Problems
Sometimes the location services on mobile devices will be better at finding where you aren’t than where you are. Some inaccuracy can be explained by the hardware a device has available; a Wi-Fi-only tablet with no GPS can get only a general location.

Symptoms of location issues can vary depending on what apps are trying to use location services. Photos might end up tagged with the wrong location, or the coffee shop you picked because it was closest might actually be further away than your device suggests. A navigation app might have trouble identifying your location at all, or it might be sure it knows where you are even when you know you’re blocks away. Other symptoms can include prompts and error or informational messages from the OS or apps that rely on location data (see Figure 25-6).



Figure 25-6  GPS prompt

Troubleshooting location problems begins with simple actions such as making sure that your GPS, cellular data, and Wi-Fi are turned on and functioning properly, as sometimes these services can be inadvertently turned off by the user or by an app, and have to be periodically reactivated. Typically, a warning message will indicate that GPS or data services are turned off, so this is easy to identify and fix. Specific apps may have trouble if they are configured not to access or use location services. This is usually a matter of going into the app configuration or location settings and allowing the app to make use of those services.



EXAM TIP   If you run into GPS error questions on the exam, remember that all apps will tell you if GPS is turned off and usually ask you if want to turn on GPS. Otherwise, before digging deeper, first consider simple issues such as whether you are in a place where you can get a good GPS signal.

Once you’ve checked the obvious software reasons for location trouble, it’s a good idea to think about the physical environment before you go on a wild-goose chase. GPS won’t work underground, will probably be spotty indoors unless you’re near a window, and can really struggle in dense urban areas with tall buildings. Don’t be spooked into a long search for subtle GPS problems if your device occasionally has trouble deciding which downtown street you’re strolling along.

When you’re sure there are frequent location problems unexplained by the environment, it’s time to dig deeper. Along with the OS issues discussed previously, incorrect OS configuration settings for GPS, cellular, and Wi-Fi services may prevent location services from functioning properly. These configuration items should be checked when multiple apps are having location issues.

If the issues persist, there’s a good chance the problem is in the actual GPS or network hardware inside the device, or the OS code that interfaces with it. Look online to see if other device owners report similar trouble on the same device software versions. If you don’t see other reports of trouble, the device likely needs a trip to the service center. Although mobile devices may have removable network or GPS modules in them, most of these components are not user serviceable and have to be replaced or repaired by authorized service technicians.

Encryption Problems
Methods to secure e-mail messages from anyone but the intended recipient generally fall well outside the accepted parameters of the CompTIA A+ certification, but it’s useful to know how to troubleshoot mobile device encryption issues. To understand the issue, we’d need to dive into a number of topics you won’t see until you take the CompTIA Security+ exam. Instead, let’s focus on the basics.

For an e-mail message to be secure, it must be encrypted—scrambled according to some kind of standard, such as Pretty Good Privacy (PGP) or Secure/Multipurpose Internet Mail Extensions (S/MIME). For the recipient to read the e-mail message, he or she needs to have software that can unscramble or decrypt the message. To ensure the sender and recipient alone can access the contents of the e-mail message, both people need specific keys that enable encryption and decryption. A key is a string of bits used by a computer program to encrypt or decrypt data.

In practice, there are a few reasons a mobile device won’t be able to decrypt an e-mail. The simplest of these is that the e-mail client or application doesn’t support the encryption standard used to encrypt the message; the fix may be a plug-in or an entirely new client. Once you confirm that the e-mail client or app supports this encryption method, follow any steps for configuring the client to use it. Finally, the e-mail client will need access to keys for decrypting the message. With some standards, keys may always be exchanged manually; someone will need to contact the sender to exchange keys. In other cases, keys may be exchanged automatically in at least some circumstances (if you’re part of the same organization, for example).

Securing Mobile Devices
Just like any computer we use to input or access sensitive data and network resources, we need to secure our mobile devices. Whether the device is company owned or personal, we still need to protect ourselves from the needless inconvenience of easily prevented damage, theft, or malware infections, as well as from the chance of important data being lost completely or falling into the wrong hands.

BYOD Versus Corporate-Owned Devices
The bring your own device (BYOD) war was briefly fought and lost by organizations hoping to continue the long-held tradition that IT assets belonged to (and were strictly controlled by) the company, not the individual. As mobile devices proliferated, however, IT folks realized the genie was out of the bottle; they couldn’t control these new technologies completely. Some companies enforce a policy prohibiting the use of personal devices to access corporate data and resources, particularly in high-security environments. Companies at the other end of the spectrum allow (and even encourage) the use of personal devices to save corporate IT dollars and keep employees happy.

Most organizations fall in the middle of the spectrum and have a mixed environment with both corporate-owned and employee-owned mobile devices. Some organizations institute a cost-sharing program, subsidizing an employee’s personally owned device with a monthly phone stipend or discount agreement with mobile device and telecommunications vendors. Regardless of how comfortable an organization is with BYOD, there are important questions to answer.

One question is how much control the corporation has versus the individual. If corporate data is processed or stored on the device, the organization should have some degree of control over it. On the other hand, if the device also belongs to the employee, then the employee should have some control. Another question is who pays for the device and its use. If the organization allows the user to use her own device for company work, does the organization help pay for the monthly bill or compensate the user for its use? Again, this issue is best solved via formal policy and procedures. Yet another important question in a BYOD environment is how to handle employee privacy. If policy allows the organization some degree of control over the device, what degree of privacy does the user maintain on her own device? Can the organization see private data, or have the ability to remotely access a user’s personal device and control its use?

The proliferation of mobile devices in the workplace has led to the development of mobile device management (MDM) policies that often combine a specialized app on the devices and specialized infrastructure to deal with those devices. These policies also inform corporate versus end-user device configuration options; in other words, who should make configuration decisions on things such as e-mail, wireless access, and so forth. As you might imagine, MDM policies are a big deal at the big organization level (the enterprise) because of the scale and complexity of the issues. A CompTIA A+ technician comes in to facilitate the installation of the MDM app, for example, or to help fix key infrastructure problems (like an overloaded WAP because all 25 members of a department bought Apple Watches at the same time). Mobile device management isn’t always necessary. Sometimes, the organization is concerned just with a specific app or group of apps. In this case, you’ll find the use of mobile application management (MAM).



EXAM TIP   Both mobile device management and mobile application management are included in the CompTIA A+ exam objectives for a reason. They sound similar but serve different purposes. MDM is for entire devices, while MAM is for specific applications used by the organization. Keep this in mind so that you don’t get them mixed up on the exams.

Profile Security Requirements
A profile is a collection of configuration and security settings that an administrator has created in order to apply those settings to particular categories of users or devices. A profile can be created in several different ways, including through the MDM software, or in a program such as the Apple Configurator, for example. Profiles are typically text-based files, usually in an eXtensible Markup Language (XML) format, and are pushed out to the different devices that require them. Profiles should be developed based on the needs of the organization. You can develop a profile specific to certain platforms, operating systems, or devices, so that a particular type of device will get certain settings.

You can also develop profiles that are specific to different user categories or management groupings (such as mobile sales representatives, middle managers, senior managers, and executives). Your senior organizational executives might have a specific profile applied to their devices granting them additional permissions and access to special apps or connections.

You might also apply group-specific profiles to external users, such as consultants or business partners. These users may require limited access to organizational resources using their own mobile device, their organization’s mobile devices, or even mobile devices temporarily issued by your organization. A group-specific profile applied to these external users may give them particular network configuration and security settings so that they can access a business extranet, for example, or use specific VPN settings. They may also require access to particular enterprise or business-to-business (B2B) apps hosted on your organization’s servers. In any case, both device- and user-specific profiles can be very helpful in managing larger groups of users, delivering uniform security and configuration settings to their devices based on different mission or business requirements.

Depending on your organizational needs, you could conceivably apply several different profiles to a device at once, based on platform, user group, and so forth. When multiple profiles are applied, there’s a chance some settings will conflict. For example, some restrictive settings for a device profile may not be consistent with some less-restrictive ones in a group or user profile. When both are applied to the device, the different configuration settings may conflict and overwrite each other. The solution is to pay special attention to profile precedence and configure the MDM server to resolve conflicts using criteria such as user group membership or security requirements.

You should also develop profiles that apply to corporate-owned versus employee-owned devices. A profile applied to a device in a BYOD environment may be considerably different than one applied to a company-owned device. This would be based on policy settings affecting privacy, acceptable use of the device, and so on. Figure 25-7 shows how you can conceptually apply different profiles to different device and user groups.



Figure 25-7  Applying profiles to different device and user groups

Preventing Physical Damage
For something shaped a lot like a bar of soap and sometimes almost as slippery, mobile phones can cost a lot of money. That means you need to take steps to prevent damage. The first step you should take to protect your slippery investment is a case, protective cover, or sleeve for the mobile device. It doesn’t help the HD camcorder in your new iPad if you get a scratch across the lens! You’ll get a scratched, blurry movie even though the camcorder is capable of much, much more. Apple makes very nice covers for iPhones and iPads, plus you can get many third-party covers and sleeves (see Figure 25-8).



Figure 25-8  Putting an Apple Smart cover on an iPad

Depending on the amount of money you’re willing to spend, you can get a cover that helps protect your screen from scratches, impacts, and small amounts of water. Like to scuba with your Android device? Get a specialty waterproof case and go post your deep thoughts to Facebook from 40 feet underwater.

Do the obvious to protect your devices. Don’t get them anywhere near liquids. Don’t run your smartphone through the wash in your trousers. Don’t even think about placing heavy objects on that ~$600 tablet! Use common sense.

Combating Malware
Malware on mobile devices is an interesting issue. Tight controls on the OS and apps make traditional malware infections almost impossible on iOS and Android devices. When malware strikes, the OS maker supplies periodic OS updates, automatic updates and operating system patches. Android’s more open nature means there are third-party antivirus and anti-malware single-user (user-level) and enterprise-level solutions available if you have corporate regulations that require such software. Figure 25-9 shows an example of user-level antivirus software for an Android device.



Figure 25-9  Antivirus app for Android



NOTE   We discuss operating system updates and their importance to security in detail in Chapter 27. Be aware that OS updates are just as important for mobile device security as they are for desktops and laptops.

In an ideal world, your mobile anti-malware software will cover all threats and work on all the devices used in your corporate network. In a heterogeneous real-world infrastructure, because there may be a variety of mobile devices from different vendors using different operating systems, a one-size-fits-all anti-malware solution probably won’t work. Multiple solutions may be necessary for the different devices present on a network, or different modules covering specific types of devices may be available from the vendor to integrate with an enterprise-level anti-malware solution.

In any case, the most important part of an enterprise-level anti-malware solution is delivering timely updates to the devices on a routine basis. Network access control (NAC) solutions can ensure a device is checked for the latest anti-malware signatures and updated as necessary when it attempts to connect to the network. In the case of user-managed devices, you may need policy, NAC, and other technical solutions to ensure users are updating their own devices in a timely manner.



NOTE   Chapter 27 goes into much depth on malware, including the types of malware as well as the most common sources and symptoms of malware infections.

Dealing with Loss
The best way to make sure you’re ready to survive losing a mobile device is to assume it’s inevitable. Say it to yourself: every mobile device will get lost at least once. I hope most of your users will prove you wrong, but the odds are good we’ll all misplace every device we own at least once. Most of us will be lucky and find it right where we left it, but it could just as easily go the other way.

When you start with the assumption that your device will end up at the mercy, kindness, or ignorance of strangers at least once, it’s obvious: you should protect your data from access by putting a good screen lock on the device. Most mobile devices enable you to set a screen lock through Settings (see Figure 25-10). Do it right now! There are many types of these locks; the most common require you to input a password, PIN code, pattern, fingerprint, or successful facial recognition to unlock the mobile device so you can use it. Modern iOS and Android use device encryption to protect the built-in storage, so even a “finder” who dismantles the device to access the drive will not get your documents.



Figure 25-10  Passcode (screen lock) option in Settings

As we discussed in the “System Lockout” section earlier, mobile devices may also have failed login attempt restrictions which restrict the number of login attempts that can fail before system lockout occurs. This system lockout slows down someone trying to guess the passcode of a found mobile device while you use locator applications or services to recover or remotely wipe it.



EXAM TIP   For the purposes of the CompTIA A+ 1102 exam, know that fingerprint lock, facial recognition, pattern lock, swipe lock, and PIN code are screen lock methods used to secure mobile devices.

Apple and Google offer locator services for discovering the whereabouts of a misplaced mobile device. Using Apple’s iCloud as an example, log in to your iCloud account and click the Find My iPhone button (despite the name, it also works for iPads). As soon as the device in question accesses the Internet (and thus receives an IP address and posts its MAC address), iCloud will pinpoint the location within a few yards (see Figure 25-11). Very slick!



Figure 25-11  Locating a phone in iCloud

Recovering from Theft
If your mobile device gets stolen and contains sensitive information, then you have a couple of options for dealing with it. Locator applications and services help, but if you have credit card information or other risky data on your mobile device, you need to act quickly.

First, make sure you keep your data backed up. You should have everything synced to a local machine and, if possible, backed up to one of the remote backup applications—like Microsoft’s OneDrive cloud service—to put your data beyond the reach of even a disaster that takes out your house. With Apple devices, for example, you back up and restore with one of several services, such as iCloud or iTunes, or use the Apple Configurator to handle a fleet of iOS devices. Android devices use the Google Sync feature to back up and restore.

Second, you can remotely wipe your mobile device. Apple, for example, makes it supremely easy through your Apple account. Log in, locate, and nuke your device (see Figure 25-12). You may never get the device back, but at least the bad guys won’t have your data. It’s equally simple with Android devices. Log in and follow the same process—locate and nuke.



Figure 25-12  Erase iPad

Securing Your Data
Every security scenario we’ve discussed so far (remote wipe excepted) was designed to secure the device itself. Let’s turn to how we can protect our actual data.

Multifactor Authentication
The terms multifactor and single-factor authentication make the difference obvious enough: the number of factors used to authenticate the user. What the terms don’t make obvious is what exactly an authentication factor is, and why one of the most popular authentication schemes—a username and password—is a kind of single-factor authentication. Let’s start with the factors. First, there is the knowledge factor: something the user knows, such as a username, password, date of birth, Social Security number, and so on. The second factor is ownership or possession: something the user has in her possession, such as a smart card or token. A third factor is inherence: something the user either is or something they do. An example of an inherence factor is a biometric identifier, such as a fingerprint or retinal pattern. You commonly hear these three factors referred to as something the user knows, something the user has, and something the user is.

Other authentication factors exist but are not as commonly considered in security authentication. For example, there’s the location factor: somewhere you are. This can be used if the individual’s location can be pinpointed via GPS or some other method. The individual may be required to be at a certain location in order to log in to the system, for example. Yet another is the temporal factor. As the name implies, schemes using the temporal factor may require logon at a certain time of day, or even within so many seconds or minutes of another event. Token methods of authentication also use time factors, as the PIN displayed on a token is only good for a finite amount of time.

Armed with the factors, let’s consider authenticating with a single factor. The most common schemes require a username and password; both are something you know, so the scheme uses a single factor. You can also think of a traditional door lock as single-factor authentication; the key it requires is something the user has—a possession factor.

During the initial push to move beyond single-factor authentication, the term two-factor authentication grew common—and you’ll still hear people use this term. Over the years, however, authentication methods using more than two factors have grown increasingly common, so it has become more correct to say multifactor authentication. Multifactor authentication (MFA) can use a variety of methods, as long as it uses more than one.

Just because the term sounds fancy and might make us think of complex systems at secret government installations, don’t assume multifactor authentication hasn’t played a role in everyday life for decades. For example, when you use a bank’s ATM, you’re using MFA: something you possess (the ATM card) and something you know (the correct PIN).



EXAM TIP   Don’t confuse the username and password combination with multifactor authentication. Only one factor is being used here, the knowledge factor, making this a form of single-factor authentication.

Biometric Authentication
Combined with other authentication factors, biometric elements can provide a very secure multifactor authentication mechanism. An example of biometric authentication is presenting a smartcard to a proximity badge reader and then placing your finger on a fingerprint reader to access a secure area.



NOTE   Not every type of biometric authentication is a good fit for mobile devices. You’ll get a closer look at the different types and other uses for them in Chapter 27.

Mobile devices use biometrics, too. Laptops have included fingerprint readers for several years already, and they are common in other mobile devices such as smartphones. A prime example is Apple’s Touch ID; starting with the iPhone 5s, the iPhone can unlock with a fingerprint. Current iOS devices use facial recognition to identify and authenticate users. Check out Figure 25-13.



Figure 25-13  Face ID options

Authenticator Applications
Access to third-party or corporate networks often requires strong authentication methods. Access to a corporate VPN, for example, may require a specific app, approved and published by the organization, configured with the correct security settings. Generic apps have the ability to use multiple sets of credentials to access different Web sites, networks, or network-based services (for example, corporate e-mail, VPN access, and so forth). There are also apps that can act as tokens or issue temporary session PINs for multifactor authentication. The key to these apps is configuration; settings vary per app, but might include network configuration, authentication or encryption settings, and properly registering a given service with the authenticator app. You’ll get a further look at authenticator applications in Chapter 27 as well.

Trusted Sources Versus Untrusted Sources
For the most part, getting software from trusted sources—legitimate app stores run by the major vendors, such as Apple, Google, Microsoft, and Amazon—is both easy and secure. Different vendors have their own requirements (including security) that developers must meet in order to get an app into the vendor’s store. Most differences stem from the development and support model used by the vendor.

Apple strictly controls all aspects of the device and the apps available in the App Store (though organizations have some freedom to distribute apps developed in-house to their own devices). For example, Apple has exact requirements for how developers must create an app sold via the App Store. Android, on the other hand, has much less central control. One way Android’s relaxed controls manifest is the ability to install apps from untrusted sources.

The operating system flavors developed by different Android device makers can change which sources are and aren’t trusted. What may run on devices sold by one vendor isn’t necessarily guaranteed to run on another vendor’s device, even though they all use variations of the Android operating system. A prime example is Amazon’s line of Fire devices (including products like Fire TV and Fire Tablet), which can only get apps from the Amazon Appstore. Additionally, even apps from the Google Play store aren’t subject to guidelines as strict as the ones Apple uses. That doesn’t mean they are necessarily less secure, but it does make security issues more likely.

The security weakness third-party app stores create is essentially apps from unapproved or unofficial sources. There are definitely legitimate app sources outside of Google Play, such as device manufacturers, communications carriers, and in-house corporate development sources. Some sources are not so legitimate, and are usually unapproved by the vendors, manufacturers, and corporate customers. You may also need to modify your mobile OS to run some apps you obtain through unofficial channels. These third-party apps may be perfectly fine, or they may be malicious and pose a security risk to your device or organization. See “Unauthorized Root Access, Developer Mode, and Sideloading,” later in the chapter, for more details.

When getting apps from questionable sources, risks include apps that contain malware or steal personal data and transmit it to a third party. Additionally, some apps require replacing the operating system with one that’s not approved by the vendor; this not only invalidates the warranty on most devices, but could cause the device to be unstable and not operate properly.

Firewalls
While we’ll discuss them in greater depth in Chapter 27, for now it’s enough to know that software firewalls on individual hosts protect them from network-based threats. It isn’t completely clear what CompTIA expects you to know about firewalling mobile devices. Generally, mobile devices don’t use a firewall, because they don’t have lots of services listening on open ports (like a traditional computer would). But, because they aren’t listening, you can think of them as having a de facto firewall. The cellular and Wi-Fi networks mobile devices use also employ firewalls to protect all networked devices.

Depending on the OS, you may be able to find and install more traditional software firewall packages. One example of a software firewall for Android is shown in Figure 25-14. Android software firewall packages include basic rule elements for constructing rules to filter specific traffic coming into the host. Many of these packages also include solutions for anti-malware and basic intrusion detection.



Figure 25-14  An Android firewall app

Some of these software firewall solutions are standalone and must be configured and managed by the user, whereas some are enterprise-level solutions and can be centrally configured, updated, and managed by the systems administrator. Keep in mind that software firewall packages work at a very basic level and can’t possibly contain every single network threat. Still, they serve as a second line of defense for the host, and are part of any good, layered, defense-in-depth security design.

Mobile OS and Application Security Issues
Security is a complicated, ever-evolving topic. We’ve already discussed aspects of mobile device security at various points in the chapter, but there are some additional security issues the user and organization need to be aware of and take steps to prevent. We’ll begin with a discussion of tools you can use to troubleshoot mobile OS and application security issues broadly, and then turn to some of the common risks, symptoms, and clues related to mobile security issues.

Troubleshooting Tools
While the foundation of good security is staying informed of new threats and being vigilant about the patches, configuration updates, policy changes, anti-malware updates, and user re-education required to address these new threats, this foundation boils down to not giving attackers an easy win. Beyond this, we have to cope with security issues that require constant vigilance: novel threats, avoiding insecure applications, and irresolvable vulnerabilities.

Though your greatest assets are your own curiosity, instincts, and persistence, you can augment these with a variety of technical tools for troubleshooting mobile security issues. Let’s look at some of these tools, grouped in terms of the issues they are most useful in addressing: network attacks and app security.

Network Attacks
Device makers originally designed mobile devices to be gregarious by nature—they are more useful this way—but network attacks can exploit such openness. We’ll consider specific issues a little later in the “Unintended Connections” section and focus now on tools for identifying and mitigating risks: device security settings, user training, Wi-Fi analyzers, and cell tower analyzers.

Device Security Settings  Because network attacks generally prey on devices that are overeager to connect, the first step to mitigating these threats is to make sure your devices won’t automatically connect to any open Wi-Fi network or nearby Bluetooth device. You can apply these settings manually on each device, but you can also use MDM software or similar software made for managing more than one device, such as Apple Configurator.

User Training  It won’t help (much) to configure your devices to avoid automatic connections if your users still select any open Wi-Fi network or agree to any pairing request without considering the consequences. Similarly, your network will be at risk if your users don’t recognize any of the warning signs that their connection to your organization’s secure Wi-Fi network has been intercepted by an evil-twin wireless access point (WAP). Teach them what is normal, and train them to stop and report anything that seems out of place.

Wi-Fi Analyzer  In addition to using a Wi-Fi analyzer for tasks such as figuring out what channel a network should use, optimizing WAP placement, or finding dead spots, you can use one to map out nearby networks (see Figure 25-15). Most of these are probably genuine networks in neighboring buildings or offices, but there’s always a chance someone will set up a WAP for the wrong reasons.



Figure 25-15  A Wi-Fi analyzer app on Android showing several SSIDs in the area

Cell Tower Analyzer  Like a Wi-Fi analyzer, a cell tower analyzer helps identify nearby cellular signals, estimate their distance and direction (see Figure 25-16), measure their signal strength, and collect other information such as the technologies they are using, network names, and more. A simple use might be to confirm signal quality for a user having trouble connecting, or to map out access in the building. There’s also a chance you’ll spot an illegitimate tower operating nearby—and your organization might be the target.



Figure 25-16  My Android-based cell tower analyzer estimating the location of a cell tower

App Security
One of the important things to understand about malware is that the “best” malware accomplishes its objective without anyone detecting it. Almost anyone could figure out that malware is to blame for a device that runs like it’s full of molasses and constantly redirects your searches or Web requests to sites that announce that you’ve won a round-trip to Mars. Because the most dangerous malware is subtle, you need to use tools to help you catch the easy stuff, freeing your attention to see subtle signs something is amiss.

Anti-Malware and App Scanners  Mobile anti-malware apps, much like their desktop counterparts, use signatures and lists to scan a device in order to identify, block, remove, or warn about known malware. An app scanner, by contrast, looks through the permissions requested by your installed apps to assess the risk they pose to security and privacy. You may find some separate apps for performing each of these tasks, or combined apps that can do both. You won’t find these apps available for iOS, but many of the same features are available through the Settings app.

App scanners typically run before an app is installed or updated and can give you information such as what network connectivity the app requires, what permissions it needs, and what access the app has to certain hardware and functions on your device. App scanners can also tell you what type of data access the app has to your personal information, such as contacts and media files (see Figure 25-17).



Figure 25-17  Combined anti-malware and app scanner

The usefulness of app scanners as a security tool becomes more apparent if you think of every installed app as posing a few different risks. First, there’s the direct risk that the app is designed to spy on you or steal your data. Next, there’s the risk that the app maker will lose control of your personal information once it leaves your device. Finally, there’s the risk that a vulnerability in the app will allow an attacker to use it against you.

Some users are savvy enough to avoid directly installing malware. But how many of those users know enough to assess the risk that an attacker in the future will be able to exploit a vulnerability in an app they’re installing today? And what about malware that doesn’t require the user to do anything at all for it to find its way onto their device?



NOTE   Malware is always evolving, and always being developed. Sometimes, the software isn’t necessarily intended to be used maliciously. A high-profile example of this was software known as Pegasus. Originally designed to be used by law enforcement agencies to address terrorism and organized crime, it also ended up being used to spy on journalists, activists, and even world leaders. The scariest part was that it didn’t require the user to click or install anything in order to get to a mobile device and start spying. This is an example both of how insidious malware can be and how important it is to stay vigilant in securing and monitoring devices.

Remote Backup Applications  Maintaining a current backup of your device is one measure you need to take in case all else fails. Different tools used to perform remote backups and restore data include MDM software, iTunes, and the various synchronization tools for Android; another option is to back up the data to the manufacturer’s or third-party user cloud storage, such as Microsoft OneDrive or Apple iCloud.

Some malware can put down deep roots and be hard to expunge. A recent full backup predating the infestation can give you the confidence to focus on making sure you get rid of the malware, rather than focusing on being sure you don’t lose important data.

App Troubleshooting Tools  We’ve already looked at tools for troubleshooting general mobile device and app issues: force stop, uninstalling and reinstalling apps, and a factory reset. You can also use these tools to pinpoint and address app security issues.

Whenever you see clues or symptoms of malware or another app security issue, remember that one way you can isolate the cause is to stop apps until you identify the cause. When you know what is causing the symptoms, uninstall it. If the app is reputable and the symptoms could be non-malicious, reinstall it to see if this fixes the problem. If these steps don’t resolve the behavior, use a factory reset to cleanse the device.

Risks, Symptoms, and Clues
The value of your curiosity, intuition, and persistence begins to show in a big way when we look at the risks, symptoms, and clues that malware or some other security problem is present. When you read about a potential risk here, don’t assume you’ll only see it by itself. Because malware and other attacks can be creative, complex, and multifaceted, view the scenarios discussed in the following sections as risks to understand and manage, symptoms of malware or an attack, or merely clues of an attack underway.

Much like you shouldn’t assume you’ll see these things as isolated incidents, you shouldn’t assume when you encounter one or more of them that malware or an attack is necessarily present. In fact, we’ve already discussed many of the issues in this section as they relate to other kinds of mobile device problems.

Unexpected Resource Use
If you think about it, malware is just software or a program that uses your device for work or tasks you don’t want it to do. Like any program working hard, malware can cause resource issues. Because resource issues can also be relatively benign problems fixed by a soft reset, it’s easy to shrug them off. Be suspicious, especially if you see patterns and can’t find an obvious explanation; the first clues of an ongoing attempt to spy on your company may well be an uptick in data outbound from affected cellular devices.

Sluggish Response Time  A hot phone, high resource use, and excessive power drain can be common signs that an app is frozen or malfunctioning, but they might also be symptoms that your device is doing precisely what a malware developer intends. The device might be hot, have sluggish response time, or be low on battery because it’s a live recording device uploading everything it records in real time, or because it’s copying files available on the network to a remote location.

High Network Traffic  Likewise, high network traffic can cause network issues, signal-quality problems, frozen apps, regular syncing of large files—or a sign the device is busy uploading or downloading something without your knowledge. High network traffic may also clue you in to one or more devices that are attempting to use an illegitimate WAP or cell tower that has a lower capacity than its official counterpart.

Data-Usage Limit Notification  As discussed earlier, a data transmission limit is a line in the sand that indicates when a device has used more data than its plan or carrier allots for it. Perhaps the user drove across the country while listening to Spotify, or perhaps the device is uploading stolen data from the device and other networked locations. If you see an inexplicable data-usage limit notification, it may be time to start checking the mobile device for malware.

Unexpected Behaviors
Security threats don’t only cause unexpected resource usage, they can also cause unexpected device and application behavior. Much like their desktop counterparts, mobile devices can start to behave strangely when they are infected with malware. A high number of ads, fake security warnings, and unexpected application behavior from individual apps can all be indicators of a security issue, whether it’s malware or breached credentials. These issues will be explored in greater detail in Chapter 27, but be aware when you take the CompTIA A+ exams that these issues can also indicate that your mobile device is compromised. As with other computing devices, if you start to see any of these signs, consider scanning for malware as part of your troubleshooting efforts.

Unintended Connections
A major security issue is unintended network connections (such as cellular, Wi-Fi, and Bluetooth). Unintended cellular network connections aren’t common since these are preprogrammed into the phone by the carrier and periodically updated, but there is a technique called tower spoofing that involves setting up equipment to spoof a carrier’s tower and infrastructure and cause a cellular device to use it instead of the normal tower equipment. It requires overpowering the nearest legitimate cell signal, causing the cellular device to lock onto it instead. Equipment used in tower spoofing can also eavesdrop on any conversation, even if it is encrypted. In some cases, the equipment can fool the device into turning off encryption completely—and sophisticated attacks can even install malware on the device.

Just as hackers have been using this technique for a few years, law enforcement officials have been reportedly using it as well. Since 2010, there have been numerous court cases highlighted in the media questioning the admissibility of evidence obtained from cell signal interception. Media reports say various federal, state, and local law enforcement agencies use a device called a “Stingray” to intercept a suspect’s cell traffic using tower spoofing equipment and techniques. There’s even an aircraft-mounted version, known as a “Dirtbox.”



NOTE   Though much of the news coverage on tower spoofing focuses on U.S. law enforcement agencies using the Stingray, you could just as easily encounter malicious cellular or Wi-Fi networks run (for a variety of reasons) by individuals, businesses, organized crime, and governments anywhere in the world.

Unintended Wi-Fi connections and unintended Bluetooth pairings can enable malicious people to access, steal, or modify data. Configure your mobile device not to connect to unknown Wi-Fi networks or automatically pair with other Bluetooth devices. This will require you to manually connect to known and trusted Wi-Fi networks, and manually pair with Bluetooth devices—but it’s worth it. If the device is centrally managed, MDM software can enforce these protections via profile settings.

Connectivity Issues
Earlier, we looked at dropped and weak signals in terms of their impact on battery life, power management, and running apps. Sometimes these signal issues go unnoticed or are only a minor inconvenience. When it comes to cellular signals, they can also be one of the few clues you’ll get that your device is interacting with a spoofed cell tower.

If you or your users are in an area where the signal quality should be (and usually is) excellent, be curious—especially if you have multiple reports of difficulty. Check with the relevant cellular providers to see if they have any known tower issues in the area. Fire up a cell tower analyzer and compare nearby signals with what you’ve seen in the past, or with third-party resources online.

If users are suddenly reporting that Wi-Fi quality is low in an area where it was high, or you notice your device sees a network with a strong signal and the correct SSID in what used to be a dead spot, check it out. There may be a rogue WAP on the loose. Limited or no Internet connectivity can be a tricky problem to troubleshoot. As you’ve seen both earlier in the book and here in this chapter, there are many potential causes, but if you’ve ruled out hardware problems and provider issues and are still having limited or no connectivity, it may be time to investigate a security issue as the potential culprit.

Unauthorized Data Access
Securing data stored on a mobile device is hard. The building’s security guards might stop a courier from walking out with a desktop under his arm, but they probably won’t notice an extra phone in his pocket. Even if they do, he might just confidently claim he has to carry an extra phone for work and go on his way. If I accidentally leave my phone behind at lunch, there’s a chance I won’t notice until I head to my car that evening. Device locks and remote wipe can usually prevent unauthorized users from accessing data on a mobile device—as long as you wipe the device before it is compromised.

Data can leak out other ways, though, such as removable memory storage cards, and data sharing settings in the device’s OS or applications. Removable memory cards should be encrypted if they contain sensitive data, so an unauthorized person can’t access data if they are removed from the device. Security and privacy settings on the device can help protect personal data, and the same settings can be configured in different apps that need to access personal data.

One of the more obvious risks to every networked app with access to data is the possibility that it will leak some of that data (whether intentionally or not). In some cases, it can be hard to figure out where the leak is. If an attacker used tax returns you stuck in Dropbox to obtain a loan in your name, where and when did the data go? You had local copies on your phone, laptop, and desktop, plus what was available if your Dropbox credentials were compromised, and any copies that transited over the network. Perhaps the attacker stole them directly from the company that did your taxes.

The point is that leaked files are a risk, a potential symptom of an ongoing security issue, and a possible clue to what that issue might be. A full audit of the many ways an important file could’ve leaked out of a networked environment is beyond what can be expected of a CompTIA A+ tech, but he or she may well get the first chance to escalate the issue or write it off as a compromised login and make the user change passwords.



EXAM TIP   Portable and mobile devices present amazing opportunities for your personal information to become much less personal and a lot more public. The CompTIA A+ 1102 exam calls this “leaked personal files/data,” but it could just as easily be translated as “your phone password wasn’t strong and you left the phone in a kiosk at the ski resort.” (Not that this has ever happened to me.)

Unauthorized Account Access
Unauthorized account access is a big deal not only for the mobile device itself, but also for all organizational networks it can connect to. If someone steals the account credentials or is able to access a mobile device configured to remember the credentials, then they have an entry point into an organizational network. As discussed earlier, you should plan based on the assumption every device will be lost.

To keep VPN and e-mail connections secure, the device should not store usernames and passwords for connecting automatically. This way, lost or stolen devices can’t be used to access these services (at least not without also stealing credentials) because they still require authentication. Unauthorized account access can lead to a malicious person stealing or accessing data not only on the device, but also on the larger network.

When a device is lost, act with an abundance of caution. Treat the previously described precaution as something to protect you until the device is reported missing. Once you know it is missing, change the user’s credentials. Keep in mind that compromised account credentials could also be a clue that one of the user’s devices itself has been compromised and may be an ongoing threat to the organization.

Unauthorized Root Access, Developer Mode, and Sideloading
To help secure the device, mobile operating systems all restrict the actions (such as installing apps or changing settings) that a user can normally perform. There are ways around these restrictions, though the name of each method differs by OS, depending on how the OS restricts what the user can do. To fully remove these restrictions, a user may have to jailbreak (iOS) or root (Android) the device. Android also has two less intrusive options: developer mode and sideloading. Let’s take a look at each.



EXAM TIP   Know jailbreak, root access, and the OS associated with each, but keep in mind that it’s common to see both of these terms used in relation to removing access restrictions from any given device.

Jailbreaking means the user installs a program on the iOS device that changes settings Apple didn’t intend for users to change. Jailbreaking allows a user to install blocked software, such as apps that don’t come from the App Store or apps that don’t meet Apple’s legal and quality requirements. Jailbreaking also enables a user to unlock functionality on the device.

Rooting an Android device is a similar procedure to grant the user full administrative access to the lower-level functionality of the device. As in the case of jailbreaking, this is also done to install software or enable functions that could not otherwise be used on the device. Although none of the popular Android device vendors condone rooting, they have little recourse beyond voiding the warranty if the user owns the device.

Developer mode is another Android-specific mode, but unlike rooting, it doesn’t present the same level of catastrophic risk that rooting can. You don’t void your warranty, you don’t leave your phone unusable if you make a mistake, and you don’t introduce major security risks. However, a user who isn’t familiar with developer mode options may end up changing settings that make using the device more difficult. Developer mode gives users access to features like USB debugging, more advanced resource monitoring, and the ability to go a step farther by rooting the device. As a result, developer mode doesn’t present its own security risks, but it does give Android users access to functionality that might.

In the same vein, another unique aspect of Android when compared to Apple’s mobile OSs is the ability to sideload applications without using a dedicated app store. Sideloading allows an Android user to use a file called an Android package (APK) to install an app that they got from a Web site or source other than the Google Play store onto their device. Sideloading can have some advantages like allowing a user to bypass geographic limitations or install software that was previously available on the app store and removed for whatever reason.

Sideloading also comes with security risks. Some APKs can be bootleg applications, which can pose legal issues. Other APKs may be malicious applications, designed to act similarly to a Trojan horse (explained in more detail in Chapter 27). Application spoofing can be a very dangerous attack method when used against mobile devices, as many people wrongly assume that mobile devices aren’t vulnerable the same way desktop and laptop computers are. As with any other class of devices, a false sense of security can lead to real-world security problems.

The important thing to keep in mind with jailbreaking, rooting, and sideloading is that they give the user more power at the expense of disabling protections that limit the damage malicious apps can do to the device. There are some things you just can’t use a device for without removing these restrictions, but the benefit should always be weighed against the risk, especially when it comes to deciding whether to allow jailbroken/rooted devices on your network.



NOTE   Organizational networks may use MDM software to detect and block devices that have used one of these methods to remove restrictions.

The manufacturer or service provider may prevent a device from connecting to their services if they detect the change. There are also immediate risks: a failed attempt could brick the device, or perhaps just render it unusable until you restore it completely from a backup (removing the jailbreaking/rooting software in the process).

Unauthorized Location Tracking
We discussed the benefits of GPS and location tracking earlier, but there are also risks involved. Configuration settings in the OS and apps may allow a user’s location to be sent to third parties, sometimes without explicit consent or knowledge. The best way to prevent this is to turn off the GPS function or location services unless they are needed. Another way is to configure the device and apps that use geotracking to prevent unauthorized tracking, if the device allows it. Some apps—or specific features—simply won’t work until geotracking is enabled (see Figure 25-18).



Figure 25-18  Four Android apps prompting the user to enable location services

Keep in mind that the GPS functionality in a mobile device is not the only way to track its location; cellular networks and Wi-Fi are also used to track device location, although not as precisely as GPS. Some of the network attacks in the “Unintended Connections” section can also be used to locate or track a device.

Unauthorized Camera and Microphone Activation
App features, malware, and unauthorized network connections can potentially be used to activate (or disable!) some features on a mobile device. Any built-in cameras and microphones are of particular concern, because they enable an attacker to move beyond sensitive data on the device and effectively spy on anyone near it.



NOTE   Some of the most sophisticated attacks using methods discussed in the earlier “Unintended Connections” section can reportedly cause a device to appear to power down while still leaving its microphone active. Attacks of this quality may be unavoidable until carriers and device makers secure their networks and devices against them, but you can still be on the lookout for strange behavior.

The ways to prevent these exploits are by restricting camera and microphone permissions in apps or operating systems (when they allow it), taking steps previously described to prevent unauthorized network connections, and using anti-malware solutions on the device. Even when you’re looking at a popular app by a trustworthy developer, such as the iOS apps with camera permissions in Figure 25-19, keep in mind that any vulnerabilities in a networked app with camera and microphone permissions could allow an attacker to listen in.



Figure 25-19  Apps with permission to access my iPhone’s camera

Chapter Review
Questions
1.   After five minutes of struggling with a painfully sluggish device, you finally manage to close the offending application. What’s the best next step?

A.   Reopen the application and hope it doesn’t freeze again.

B.   Uninstall the application and look for a replacement.

C.   Perform a soft reset and see if the app runs smoothly afterward.

D.   Close all open applications and attempt to reopen the application to see if it freezes again.

2.   Which of the following would be a legitimate reason a mobile device is running slowly?

A.   Incorrect calibration

B.   RAM too slow

C.   Lack of storage space

D.   Incorrect version of application

3.   Joyce notices her GPS map app gives the error “GPS coordinates not available.” What should she try first?

A.   Run another GPS app.

B.   Stop and start GPS on the mobile device.

C.   Move to a place where she can get a good GPS signal.

D.   Update the mobile device’s firmware.

4.   You’ve lost your iPhone. What would you use to try to find it?

A.   iTunes

B.   iFind

C.   Location Services

D.   iCloud

5.   Fred wants to play World of Warcraft on his desktop system. He logs in and then the game asks for a code that is generated by an authenticator app on his Android phone. This is an example of ___________.

A.   Multifactor authentication

B.   Factor authorization

C.   Multifactor authorization

D.   Factor authentication

6.   Jailbreaking an iPhone gives access to ____________.

A.   The administrator account

B.   The root account

C.   The /bin folder

D.   The system BIOS

7.   A great way to protect data on a removable media card is to ___________.

A.   Encrypt it

B.   Lock it

C.   Remove it when unneeded

D.   Format it

8.   What type of file would you use to sideload an app onto an Android device?

A.   APK

B.   ZIP

C.   GIF

D.   EXE

9.   Users bringing personally owned mobile devices into an enterprise environment is called ___________.

A.   Importing

B.   CYMK

C.   Providing

D.   BYOD

10.   What do app scanners do?

A.   Scan QR codes and barcodes for hidden codes

B.   Analyze the traffic into and out of an application for suspicious behavior

C.   Analyze the permissions used by installed applications to highlight security risks

D.   Analyze Wi-Fi signals to identify evil-twin WAPs

Answers
1.   C. After five minutes of struggling with a painfully sluggish device, definitely perform a soft reset and see if the app runs smoothly afterward.

2.   C. Lack of storage space would be a legitimate reason a mobile device is running slowly.

3.   C. Joyce needs to move to a place where she can get a good GPS signal.

4.   D. Apple’s iPhone uses the Find My iPhone feature of iCloud.

5.   A. Using both a password and a security code is an example of multifactor authentication.

6.   B. Jailbreaking is unique to iOS to provide access to the root account.

7.   A. A great way to protect data on a removable media card is to encrypt it.

8.   A. An Android Package (APK) is the file type that is used to sideload applications onto Android devices.

9.   D. Users bringing personally owned mobile device into an enterprise environment is known as bring your own device (BYOD).

10.   C. App scanners analyze the permissions used by installed applications to highlight security risks.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 25 Maintaining and Securing Mobile Devices
Chapter 26 Printers and Multifunction Devices
Chapter 27 Securing Computers
42h 21m remaining
CHAPTER 26
Printers and Multifunction Devices
In this chapter, you will learn how to

•   Describe current printer and multifunction device consumables

•   Explain the laser printing process

•   Install and configure a printer or multifunction device consumable

•   Recognize and fix basic printer and multifunction device problems

Despite all the talk about the “paperless office,” paper documents continue to be a vital part of the typical office. Some computers are used exclusively for the purpose of producing paper documents. Many people simply still prefer dealing with a hard copy, even as portable devices have proliferated. Developers cater to this preference by using metaphors such as page, workbook, and binder in their applications.

In the past, your average office had an array of electronic and mechanical devices dedicated to performing a single task with paper documents. Think printers, copiers, scanners, and fax machines. Back in the 1990s, the multifunction device (MFD), also known as a multifunction printer (MFP), tried to consolidate multiple functions (often printing and scanning) into a single device. At first these devices weren’t terribly great at any of their functions, but today’s mature multifunction devices get their many jobs done well.

The CompTIA A+ certification strongly stresses the area of printing and expects a high degree of technical knowledge of the function, components, maintenance, and repair of all types of printers and multifunction devices.

This chapter examines the common varieties of printers and scanners, then looks at specifics of how a laser printer works. The chapter continues with the steps for installing a multifunction device in a typical personal computer and concludes with troubleshooting issues.

1101
Printer and Multifunction Device Consumables
The multifunction devices commonly used in SOHO environments typically sit on a desk, shelf, or countertop, and they tend to be fairly similar in appearance. Because of this, when most of us think about MFDs, we picture small desktop all-in-one devices (which can usually be used as a printer, scanner, copier, and fax machine) connected to a nearby computer (see Figure 26-1 for an example).



Figure 26-1  All-in-one printer/scanner/fax machine/copier/iPhone dock

The reality is that these desktop devices, descendants of the desktop printer and scanner, are just the low end of the market. As you head upmarket, multifunction printers look more like the descendants of copy machines and even small printing presses. Despite how different from SOHO MFDs these high-end devices may look, they still share a core set of components—a printer and scanner of some sort—with the all-in-ones you’re probably familiar with. As you go upmarket, the greatest improvements tend to be in speed/capacity, durability, and document handling/finishing features such as sorting, stapling, binding, and so on.

Because MFDs are so varied, we’ll look at some of the individual components and technologies you may find inside them separately—be prepared to encounter these components as both standalone devices and included with other components in an MFD. I’ve added 3-D printers to this section; you won’t find these as anything but standalone devices, not MFDs.

Printers
No other piece of your computer system is available in a wider range of styles, configurations, and feature sets than a printer, or at such a wide price variation. What a printer can and can’t do is largely determined by the type of printer technology it uses—that is, how it gets the image onto the paper. Modern printers can be categorized into several types: impact, inkjet, thermal, laser, 3-D, and virtual.

Impact Printers
Printers that create an image on paper by physically striking an ink ribbon against the paper’s surface are known as impact printers. Although daisy-wheel printers (essentially an electric typewriter attached to the computer instead of directly to a keyboard) have largely disappeared, their cousins, dot-matrix printers, still soldier on in many offices. Although dot-matrix printers don’t deliver what most home users want—high quality and flexibility at a low cost—they’re still widely found in businesses for two reasons: dot-matrix printers have a large installed base in businesses, and they can be used for multipart forms because they actually strike the paper. Impact printers tend to be relatively slow and noisy, but when speed, flexibility, and print quality are not critical, they provide acceptable results. Computers that print multipart forms, such as point of sale (POS) machines, use special impact paper that can print receipts in duplicate, triplicate, or more. These POS machines represent the major market for new impact printers, although some older dot-matrix printers remain in use.

Dot-matrix printers use a grid, or matrix, of tiny pins, also known as printwires, to strike an inked printer ribbon and produce images on paper (see Figure 26-2). The case that holds the printwires is called a printhead. Using either 9 or 24 pins, dot-matrix printers treat each page as a picture broken up into a dot-based raster image. The 9-pin dot-matrix printers are generically called draft quality, while the 24-pin printers are known as letter quality or near-letter quality (NLQ). The BIOS for the printer (either built into the printer or a printer driver) interprets the raster image in the same way a monitor does, “painting” the image as individual dots. Naturally, the more pins, the higher the resolution. Figure 26-3 illustrates the components common to dot-matrix printers. Some dot-matrix printers use continuous-feed paper with holes on its sides that are engaged by metal sprockets to pull the paper through—this is known as tractor-feed paper because the sprockets are reminiscent of the wheels on a tractor.



Figure 26-2  An Epson FX-880+ dot-matrix printer (photo courtesy of Epson America, Inc.)



Figure 26-3  Inside a dot-matrix printer

Inkjet Printers
Inkjet printers (also called ink-dispersion printers) like the one shown in Figure 26-4 are relatively simple devices. An inkjet printer uses a printhead connected to a carriage that contains the ink. A carriage belt and motor move the carriage back and forth so the ink can cover the whole page. A roller grabs paper from a paper tray (usually under or inside the printer) or feeder (usually on the back of the printer) and advances it through the printer (see Figure 26-5).



Figure 26-4  Typical inkjet printer



Figure 26-5  Inside an inkjet printer

The ink is ejected through tiny tubes. Most inkjet printers use heat to move the ink, while a few use a mechanical method. The heat-method printers use tiny resistors or electroconductive plates at the end of each tube that literally boil the ink; this creates a tiny air bubble that ejects a droplet of ink onto the paper, thus creating a portion of the image (see Figure 26-6).



Figure 26-6  Detail of the inkjet printhead

The ink is stored in special small containers called ink cartridges. Older inkjet printers had two cartridges: one for black ink and another for colored ink. The color cartridge had separate compartments for cyan (blue), magenta (red), and yellow ink, to print colors by using a method known as CMYK (you’ll read more about CMYK later in this chapter). If your color cartridge ran out of one of the colors, you had to purchase a whole new color cartridge or deal with a messy refill kit.

Printer manufacturers began to separate the ink colors into three separate cartridges so that printers came with four cartridges: one for each color and a fourth for black (see Figure 26-7). This not only was more cost-effective for the user, but it also resulted in higher-quality printouts. Today you can find color inkjet printers with six, eight, or more color cartridges. In addition to the basic CMYK inks, the additional cartridges provide for green, blue, gray, light cyan, dark cyan, and more. Typically, printers using more ink cartridges produce higher-quality printed images—and cost more.



Figure 26-7  Inkjet ink cartridges

In recent years, manufacturers such as Epson and Canon have introduced ink-jet printers with refillable ink tanks, radically changing the economics of printing. Rather than selling printers inexpensively and raking in money on throw-away ink cartridges, consumers and businesses can print in glorious color without the hassle (or guilt). The printers, such as the Epson EcoTank line, cost a lot more than previous models (think $300–$700 rather than $60–$120), but come with a couple of years’ worth of ink fresh out of the box. Let the color flow.

The two key features of an inkjet printer are the print resolution—how densely the printer lays down ink on the page—and the print speed. Resolution is measured in horizontal and vertical dots per inch (dpi), such as 2400 × 2400 dpi. Higher numbers mean that the ink dots on the page are closer together, so your printed documents will look better. Resolution is most important when you’re printing complex images such as full-color photos, or when you’re printing for duplication and you care that your printouts look good. Print speed is measured in pages per minute (ppm), and this specification is normally indicated right on the printer’s box. Most printers have one (faster) speed for monochrome printing—that is, using only black ink—and another for full-color printing.

Another feature of inkjet printers is that they can support a staggering array of print media. Using an inkjet printer, you can print on a variety of matte or glossy photo papers, iron-on transfers, and other specialty media; some printers can print directly onto specially coated optical discs, or even fabric. Imagine running a T-shirt through your printer with your own custom slogan (how about “I’m CompTIA A+ Certified!”). The inks have improved over the years, too, now delivering better quality and longevity than ever. Where older inks would smudge if the paper got wet or start to fade after a short time, modern inks are smudge-proof and of archival quality—for example, some inks by Epson are projected to last up to 200 years.

For best results with all this variety of media available, you need to make sure the print settings match the paper/media type. In Windows 10, for example, go to Settings | Devices | Printers & scanners. Select the printer installed, click Manage, and go to Printer preferences. There you can change the media type to match.



NOTE   Print resolution is measured in dots per inch (dpi) and print speed is measured in pages per minute (ppm).

Try This!

Pages per Minute Versus Price

Printer speed is a key determinant of a printer’s price, and this is an easy assertion to prove, so try this!

1.   Open a browser and head over to the Web site for HP (https://www.hp.com), Canon (https://www.canon.com), Epson (https://www.epson.com), Brother (https://www.brother.com), or Samsung (https://www.samsung.com). These five companies make most of the printers on the market today.

2.   Pick a printer technology and check the price, from the cheapest to the most expensive. Then look for printers that have the same resolution but different ppm rates.

3.   Check the prices and see how the ppm rate affects the price of two otherwise identical printers.

Thermal Printers
Thermal printers use a heated printhead to create a high-quality image on special or plain paper. You’ll see two kinds of thermal printers in use. The first is the direct thermal printer, and the other is the thermal wax transfer printer. Direct thermal printers use a heating element to burn dots into the surface of special heat-sensitive thermal paper. If you remember the first generation of fax machines, you’re already familiar with this type of printer. Many retail businesses still use it as a receipt printer, using large rolls of thermal paper housed in a feed assembly that automatically draws the paper past the heating element; some receipt printers can even cut the paper off the roll for you.

Laser Printers
Using a process called electro-photographic imaging, laser printers produce high-quality and high-speed output of both text and graphics. Figure 26-8 shows a typical laser printer. Laser printers rely on the photoconductive properties of certain organic compounds. Photoconductive means that particles of these compounds, when exposed to light (that’s the “photo” part), will conduct electricity. Laser printers usually use lasers as a light source because of their precision. Some lower-cost printers use LED arrays instead.



Figure 26-8  Typical laser printer

The first laser printers created only monochrome images; you can also buy a color laser printer, but most laser printers produced today are still monochrome. Although a color laser printer can produce complex full-color images such as photographs, they really shine for printing what’s known as spot color—for example, eye-catching headings, lines, charts, or other graphical elements that dress up an otherwise plain printed presentation.



NOTE   Some printers use consumables—such as ink—at a faster rate than others, prompting the industry to rank printers in terms of their cost per page. Using an inexpensive printer (laser or inkjet) costs around 4 cents per page, while an expensive printer can cost more than 20 cents per page—a huge difference if you do any volume printing. This hidden cost is particularly pernicious in the sub-$100 inkjet printers on the market. Their low prices often entice buyers, who then discover that the cost of consumables is outrageous—these days, a single set of color and black inkjet cartridges can cost as much as the printer itself, if not more!

The CompTIA A+ certification exams take a keen interest in the particulars of the laser printing process—or specifically, the imaging process—so it pays to know your way around a laser printer (see Figure 26-9). Let’s take a look at the many components of laser printers and their functions. The imaging process is described in detail later in the chapter in the section “The Laser Printing Process.”



Figure 26-9  Components inside a laser printer

Toner Cartridge  The toner cartridge in a laser printer is so named because of its most obvious activity: supplying the toner that creates the image on the page (see Figure 26-10). To reduce maintenance costs, however, many other laser printer parts, especially those that suffer the most wear and tear, have been incorporated into the toner cartridge. Although this makes replacement of individual parts nearly impossible, it greatly reduces the need for replacement; those parts that are most likely to break are replaced every time you replace the toner cartridge.



Figure 26-10  Laser printer’s toner cartridge



NOTE   Color laser printers have four toner cartridges: black, cyan, magenta, and yellow.

Imaging Drum  The imaging drum (also called the photosensitive drum) is an aluminum cylinder coated with particles of photosensitive compounds. The drum itself is grounded to the power supply, but the coating is not. When light hits these particles, whatever electrical charge they may have “drains” out through the grounded cylinder.

Erase Lamp  The erase lamp exposes the entire surface of the imaging drum to light, making the photosensitive coating conductive. Any electrical charge present in the particles bleeds away into the grounded drum, leaving the surface particles electrically neutral.

Primary Corona/Charge Roller  The primary corona wire (or primary charge roller, in newer laser printers), located close to the imaging drum, never touches the drum. When the primary corona or primary charge roller is charged with an extremely high voltage, an electric field (or corona) forms, enabling voltage to pass to the drum and charge the photosensitive particles on its surface. The primary grid regulates the transfer of voltage, ensuring that the surface of the drum receives a uniform negative voltage of between ~600 and ~1000 volts.

Laser  The laser acts as the writing mechanism of the printer. Any particle on the drum struck by the laser becomes conductive and its charge is drained away into the grounded core of the drum. The entire surface of the drum has a uniform negative charge of between ~600 and ~1000 volts following its charging by the primary corona wire or charge roller. When particles are struck by the laser, they are discharged and left with a ~100-volt negative charge. Using the laser, we can “write” an image onto the drum. Note that the laser writes a positive image to the drum.

Toner  The toner in a laser printer is a fine powder made up of plastic particles bonded to pigment particles. The toner cylinder charges the toner with a negative charge of between ~200 and ~500 volts. Because that charge falls between the original uniform negative charge of the imaging drum (~600 to ~1000 volts) and the charge of the particles on the drum’s surface hit by the laser (~100 volts), particles of toner are attracted to the areas of the imaging drum that have been hit by the laser (that is, areas that have a relatively positive charge with reference to the toner particles).



EXAM TIP   The black toner used in laser printers is typically carbon mixed into polyester resin, while color toner trades carbon for other pigments.

Transfer Corona/Transfer Roller  To transfer the image from the imaging drum to the paper, the paper must be given a charge that will attract the toner particles off of the drum and onto the paper. In older printers, the transfer corona, a thin wire, applied a positive charge to the paper, drawing the negatively charged toner particles to the paper. Newer printers accomplish the same feat using a transfer roller that draws the toner onto the paper. The paper, with its positive charge, is also attracted to the negatively charged drum. To prevent the paper from wrapping around the drum, a static charge eliminator removes the charge from the paper.

In most laser printers, the transfer corona/roller is outside the toner cartridge, especially in large, commercial-grade machines. The transfer corona/roller is prone to a build-up of dirt, toner, and debris through electrostatic attraction, and it must be cleaned. It is also quite fragile—usually finer than a human hair. Most printers with an exposed transfer corona/roller provide a special tool to clean it, but you can also—very delicately—use a cotton swab soaked in denatured alcohol (don’t use rubbing alcohol because it contains emollients). As always, never service any printer without first turning it off and unplugging it from its power source.

Fuser Assembly  The fuser assembly is almost always separate from the toner cartridge. It is usually quite easy to locate, as it is close to the bottom of the toner cartridge and usually has two rollers to fuse the toner. Sometimes the fuser is somewhat enclosed and difficult to recognize because the rollers are hidden from view. To help you determine the location of the fuser, think about the path of the paper and the fact that fusing is the final step of printing.

The toner is merely resting on top of the paper after the static charge eliminator has removed the paper’s static charge. The toner must be melted to the paper to make the image permanent. Two rollers, a pressure roller and a heated roller, are used to fuse the toner to the paper. The pressure roller presses against the bottom of the page, and the heated roller presses down on the top of the page, melting the toner into the paper. The heated roller has a nonstick coating such as Teflon to prevent the toner from sticking to it.

Power Supplies  All of the devices described in this chapter have power supplies, but when dealing with laser printers, techs should take extra caution. The corona in a laser printer requires extremely high voltage from the power supply, making a laser printer power supply one of the most dangerous devices in computing! Turn off and unplug the printer as a safety precaution before performing any maintenance.

Turning Gears  A laser printer has many mechanical functions. First, the paper must be grabbed by the pickup roller and passed over the separation pad, which is a small piece of cork or rubber that separates the sheets as they are pulled from the paper feed tray. A separation pad uses friction to separate a single sheet from any others that were picked up. Next, the photosensitive roller must be turned and the laser, or a mirror, must be moved back and forth. The toner must be evenly distributed, and the fuser assembly must squish the toner into the paper. Finally, the paper must be kicked out of the printer and the assembly must be cleaned to prepare for the next page.



EXAM TIP   Be sure you are familiar with laser printer components, particularly the imaging drum, fuser assembly, transfer belt, transfer roller, pickup rollers, separation pads, and duplexing assembly.

More sophisticated laser printers enable duplex printing, meaning they can print on both sides of the paper. This is another mechanical function with a dedicated duplexing assembly for reversing the paper.

All of these functions are served by complex gear systems. In most laser printers, these gear systems are packed together in discrete units generically called gear packs or gearboxes. Most laser printers have two or three gearboxes that you can remove relatively easily in the rare case one of them fails. Most gearboxes also have their own motor or solenoid to move the gears.

All of these mechanical features can wear out or break and require service or replacement. See the “Troubleshooting Printers” section, later in this chapter, for more details.

System Board  Every laser printer contains at least one electronic board. On this board is the main processor, the printer’s ROM, and the RAM used to store the image before it is printed. Many printers divide these functions among two or three boards dispersed around the printer (also known as sub-logic boards, as shown back in Figure 26-10). An older printer may also have an extra ROM chip and/or a special slot where you can install an extra ROM chip, usually for special functions such as PostScript.

On some printer models, you can upgrade the contents of these ROM chips (the firmware) by performing a process called flashing the ROM. Flashing is a lot like upgrading the system BIOS, which you learned about in Chapter 5. Upgrading the firmware can help fix bugs, add new features, or update the fonts in the printer.

Of particular importance is the printer’s RAM. When the printer doesn’t have enough RAM to store the image before it prints, you get a memory overflow problem. Also, some printers store other information in the RAM, including fonts or special commands. Adding RAM is usually a simple job—just snapping in a SIMM or DIMM stick or two—but getting the right RAM is important. Call or check the printer manufacturer’s Web site to see what type of RAM you need. Although most printer companies will happily sell you their expensive RAM, most printers can use generic DRAM like the kind you use in a computer.

Ozone Filter  The coronas inside laser printers generate ozone (O3). Although not harmful to humans in small amounts, even tiny concentrations of ozone will cause damage to printer components. To counter this problem, most laser printers have a special ozone filter that needs to be vacuumed or replaced periodically.

Sensors and Switches  Every laser printer has a large number of sensors and switches spread throughout the machine. The sensors are used to detect a broad range of conditions such as paper jams, empty paper trays, or low toner levels. Many of these sensors are really tiny switches that detect open doors and so on. Most of the time these sensors/switches work reliably, yet occasionally they become dirty or broken, sending a false signal to the printer. Simple inspection is usually sufficient to determine if a problem is real or just the result of a faulty sensor/switch.

3-D Printers
3-D printers (see Figure 26-11) use melted material to create prints of three-dimensional objects. The flat surface from which the 3-D printer deposits this melted material to build an object is called the print bed. The most common 3-D printers use plastic filament or resin on spools (see Figure 26-12). Some 3-D printers enable you to print with multiple colors.



Figure 26-11  3-D printer



Figure 26-12  3-D printer plastic filament

A typical 3-D printer is made of many distinct parts. Take a look at Figure 26-13 for a breakdown of some of the more important components.



Figure 26-13  3-D printer

3-D printers take a 3-D illustration and build it in tiny layers or slices, one by one. 3-D filament printers work by melting the plastic and allowing it to cool as the 3-D image builds. 3-D resin printers work by placing liquid resin down and curing it with UV light. Simple printers can create relatively simple shapes, such as blocks, pyramids, and so on. Better printers can create more exciting shapes, such as the stylized replacement game pieces for the popular board game Settlers of Catan pictured in Figure 26-14. Even better 3-D printers can make elaborate structures, with lots of holes and gaps within the layers.



Figure 26-14  3-D-printed game pieces (photo courtesy of Donny Jansen)

Installation of 3-D printers requires more than the typical printer installation. The connections (USB) and drivers are typical, but 3-D printers also need manual connection of the plastic filament(s) to the print device. You’ll also need specialized software designed to print in 3-D. Most manufacturers’ 3-D printing software enables you to use standard 3-D drawings, such as STL, OBJ, and CAD files. Figure 26-15 shows the Ultimaker Cura software pushing a print job to a 3-D printer. Sweet!



Figure 26-15  Managing a new 3-D print job

Virtual Printers
The most quizzical printer of all, the virtual printer, doesn’t look like much, but it’s actually still pretty similar to physical or “real” printing. When you print to a virtual printer, your system goes through all the steps to prepare a document for printing and sends it off to a virtual printer—a program that converts the output from your computer into a specific format and saves the result to a portable file that looks like the printed page would have. You can print this file later if you like, or maybe send it to someone else to print, but you can also just keep it in digital format. Virtual printers provide a nice way to save anything you can print, and they’re particularly good for saving reference copies of information found on the Web.

Print to PDF  One of the most popular virtual printing options is the ability to print to PDF, a feature every operating system supports out of the box these days. Windows didn’t join the party until Windows 10, however, so be aware that you’ll need to install a virtual PDF printer on older versions of Windows. You can get these through official Adobe software, but there are also some third-party options.

Cloud and Remote Printing  Blurring the line between traditional and virtual printing, a variety of cloud services, such as Google Cloud Print, will install a virtual printer on your system that wraps up your document and sends it out over the Internet or other network to a cloud server, which eventually ends up routing it to a real printer for printing—all without needing to have a driver installed for it.

Printer Languages
Now that you’ve learned about the different types of print devices and techniques, it’s time to take a look at how they communicate with the computer. How do you tell a printer to make a letter A or to print a picture of your pet iguana? Printers are designed to accept predefined printer languages that handle both characters and graphics. Your software must use the proper language when communicating with your printer, in order to output paper documents. Following are the more common printer languages.



EXAM TIP   One thing to remember for the exam is the importance of choosing the appropriate driver for the OS. A common printing mistake, for example, is that you may be printing to a PostScript printer with a PCL driver.



NOTE   You might think of the American Standard Code for Information Interchange (ASCII) language as nothing more than a standard set of characters. ASCII actually contains a variety of control codes for transferring data, some of which can be used to control printers. For example, ASCII code 10 (or 0A in hex) means “Line Feed,” and ASCII code 12 (0C) means “Form Feed.” These commands have been standard since before the creation of IBM computers, and all printers respond to them. If they did not, the PRT SCR (print screen) key would not work with every printer. Being highly standardized has advantages, but the control codes are extremely limited. Printing high-end graphics and a wide variety of fonts requires more advanced languages.

PostScript  Adobe Systems developed the PostScript page description language in the early 1980s as a device-independent printer language capable of high-resolution graphics and scalable fonts. PostScript interpreters are embedded in the printing device. Because PostScript is understood by printers at a hardware level, the majority of the image processing is done by the printer and not the computer’s CPU, so PostScript printers print faster. PostScript defines the page as a single raster image; this makes PostScript files extremely portable—they can be created on one machine or platform and reliably printed out on another machine or platform (including, for example, high-end typesetters).

HP Printer Command Language  HP developed its Printer Command Language (PCL) as a more advanced printer language to supersede simple ASCII codes. PCL features a set of printer commands greatly expanded from ASCII. HP designed PCL with text-based output in mind; it does not support advanced graphical functions. The most recent version of PCL, PCL6, features scalable fonts and additional line-drawing commands. Unlike PostScript, however, PCL is not a true page description language; it uses a series of commands to define the characters on the page. Those commands must be supported by each individual printer model, making PCL files less portable than PostScript files.



EXAM TIP   The CompTIA A+ Acronym list identifies PCL as Printer Control Language. Control or Command is rather irrelevant at this point in time. HP refers to PCL as simply PCL in all its documentation.

Windows GDI and XPS  Windows uses the graphical device interface (GDI) component of the operating system to handle print functions. Although you can use an external printer language such as PostScript, most users simply install printer drivers and let Windows do all the work. The GDI uses the CPU rather than the printer to process a print job and then sends the completed job to the printer. When you print a letter with a TrueType font in Windows, for example, the GDI processes the print job and then sends bitmapped images of each page to the printer. The printer sees a page of TrueType text, therefore, as a picture, not as text. As long as the printer has a capable enough raster image processor (explained later in this chapter) and plenty of RAM, you don’t need to worry about the printer language in most situations. We’ll revisit printing in Windows in more detail later in this chapter.

Windows Vista also introduced a new printing subsystem called the XML Paper Specification (XPS) print path in 2006. In 2009, the ECMA-388 standard formally named XPS the Open XML Paper Specification (OpenXPS), although Microsoft and others continue to use only XPS in documentation and screen elements. XPS provides several improvements over GDI, including enhanced color management (which works with Windows Color System, introduced in the “Optimizing Print Performance” section later in the chapter) and better print layout fidelity. The XPS print path requires a driver that supports XPS. Additionally, some printers natively support XPS, eliminating the requirement that the output be converted to a device-specific printer control language before printing.



EXAM TIP   Laser and inkjet printers can also use duplexing assemblies, which enable the printer to automatically print on both sides of the paper. Some printers include this built-in feature, while others require a piece of additional hardware that flips the paper for the printer.

Scanners
You can use a scanner to make digital copies of existing paper photos, documents, drawings, and more. Better scanners give you the option of copying directly from a photographic negative or slide, providing images of stunning visual quality—assuming the original photo was halfway decent, of course! In this section, you’ll look at how scanners work and then turn to what you need to know to select the correct scanner for you or your clients.

How Scanners Work
All flatbed scanners, the most common variety of scanner, work the same way. You place a photo or other object face down on the glass (called the platen), close the lid, and then use software to initiate the scan. The scanner runs a bright light along the length of the platen once or more to capture the image. Figure 26-16 shows an open scanner.



Figure 26-16  Scanner open with photograph face down



NOTE   Many serious flatbed scanners and multifunction devices will have an automatic document feeder (ADF) to remove most of the manual labor from this process. Check out the upcoming “Automatic Document Feeder” section for more details.

The scanning software that controls the hardware can manifest in a variety of ways. Nearly every manufacturer has some combination of drivers and other software to create an interface between your computer and the scanner. When you push the front button on the Epson Perfection scanner, for example, the Epson software loads, ready to start scanning (see Figure 26-17).



Figure 26-17  Epson software

You can also open your favorite image-editing software first and choose to acquire a file from a scanner. Figure 26-18 shows the process of acquiring an image from a scanner in the popular free image-editing software, GNU Image Manipulation Program (otherwise known as GIMP). As in most such software, you choose File | Create and then select Scanner. In this case, the scanner uses the traditional TWAIN drivers. TWAIN stands for Technology Without an Interesting Name—I’m not making this up!—and has been the default driver type for scanners for a long time.



Figure 26-18  Acquiring an image in GNU Image Manipulation Program (GIMP)

At this point, the drivers and other software controlling the scanner pop up, providing an interface with the scanner (as shown in Figure 26-17). Here you can set the resolution of the image as well as many other options.



NOTE   In addition to loading pictures into your computer, many scanners offer a feature called optical character recognition (OCR), a way to scan a document and have the computer turn the picture into text that you can manipulate by using a word processing program.

How to Choose a Scanner
You must consider four primary variables when choosing a scanner: resolution, color depth, grayscale depth, and scan speed. You can and will adjust the first three during the scanning process, although probably only down from their maximum. The scan speed relates to all four of the other variables, and the maximum speed is hard-coded into the scanner.

Configurable Variables  Scanners convert the scanned image into a grid of pixels (often referred to as dots). The maximum number of pixels determines how well you can capture an image and how the image will look when scaled up in size. Most folks use the term resolution to define the grid size. As you might imagine, the higher-resolution images capture more fine detail.

Older scanners can create images of only 600 × 600 dots per inch (dpi), while newer models commonly achieve four times that density, and high-end machines do much more. Manufacturers cite two sets of numbers for a scanner’s resolution: the resolution it achieves mechanically—called the optical resolution—and the enhanced resolution it can achieve with assistance from some onboard software.

The enhanced resolution numbers are useless. I recommend at least 2400 × 2400 dpi optical resolution or better, although you can get by with a lower resolution for purely Web-destined images.

The color depth of a scan defines the number of bits of information the scanner can use to describe each individual pixel. This number determines color, shade, hue, and so forth, so color depth makes a dramatic difference in how easily you can adjust the color and tone in your photo editor. With binary numbers, each extra bit of information doubles the color detail in the scan. The most common color depth options you will run across in scanners today are 24-bit and 48-bit. A 24-bit scan, for example, can save up to 256 shades for each of the red, green, and blue sub-pixels that make up an individual pixel. This gives you a total of 16,777,216 color variations in the scanned image, which explains why some scanners refer to this as “millions of colors” in their settings. A 48-bit scan, in contrast, can save up to 65,536 shades per subpixel, giving you a scan that holds a massive 281,474,976,710,656 color variations. All this extra color does come with a downside: images scanned at 48 bits are twice the size of 24-bit scans and can easily be hundreds of megabytes per file!

These days, 48-bit scanners are common enough that you shouldn’t have to settle for less, even on a budget. Figures 26-19, 26-20, and 26-21 show pretty clearly the difference resolution makes when scanning.



Figure 26-19  Earring scanned at 72 dpi and 24-bit color



Figure 26-20  Same earring, scanned at 300 dpi and 24-bit color



Figure 26-21  Same earring, scanned at 1200 dpi and 24-bit color

Scanners differ a lot in grayscale depth, a number that defines how many shades of gray the scanner can save per pixel. This matters if you work with black-and-white images in any significant way, because grayscale depth may be advertised with a much lower number than color depth. Current consumer-level scanners come in 8-bit, 12-bit, and 16-bit grayscale varieties. You might recognize these three numbers from the previous color depth discussion, because grayscale images only need a third the information it takes to represent the red, green, and blue values that make up a color image. I recommend 16-bit.

Scanning Speed  Scanners have a maximum scanning speed defined by the manufacturer. The time required to complete a scan is also affected by the parameters you set; the time increases as you increase the amount of detail captured. A typical low-end scanner, for example, takes upward of 30 seconds to scan a 4 × 6 photo at 300 dpi. A faster scanner, in contrast, can crank out the same scan in 10 seconds.

Raise the resolution of the scan to 600 dpi at 48-bit resolution, and that faster scanner can take a full minute to complete the scan. Adjust your scanning settings to optimize for your project. Don’t always go for the highest quality scan if you don’t need the resolution and color depth.

Network Scan Services
If you’ve ever had to fill out a paper document and upload it, you’ve used a scanner, but you may not be aware of how many ways networking can make scanning easier. You can use cloud services like we talked about for printers earlier in the chapter, but that’s not all. Remember the SMB protocol from Chapter 19? It’s not just for print sharing.

You can also use SMB for scan sharing, enabling the scanning of a lot of data directly to a networked folder that other people on the network can access. It can save a few steps by removing the need to scan locally and then manually move the scanned files to the file share; but be careful, using SMB can introduce security vulnerabilities (you’ll learn all about security and vulnerabilities in the next chapter). Many multifunction devices are older, and as a result, may only support older versions of the protocol. If the device only supports SMB 1.0, then you’ll probably want to find an alternative way to get your scanned documents onto a network share.

Scanning can even make use of the humble email. Many multifunction devices include a scan to e-mail feature, which lets you scan a document and have it automatically e-mailed from you to someone else. This is useful when you want to send a scanned document to an individual or small group rather than to a dedicated network share.

Scanning Tips
As a general rule, you should obtain the highest quality scan you can manage, and then play with the size and image quality when it’s time to print it or share it over the Web. The amount of RAM in your system—and to a lesser extent, the processor speed—dictates how big a file you can handle.



NOTE   If you’re set to do some heavy scanning—like archiving all those old family photos—check out Wayne Fulton’s Web site, https://www.scantips.com. The site has a simple, direct interface, and a treasure trove of excellent information on scanners and scanning. I’ve used his knowledge for years now and recommend it highly.

If you travel a lot, you’ll want to make sure to use the locking mechanism for the scanner light assembly. Just be sure to unlock before you try to use it or you’ll get a light that’s stuck in one position. That won’t make for very good scans!

Copy and Fax Components
The scanning and printing capabilities of a multifunction device enable manufacturers to add copy-machine features easily. To copy a document or photo, you essentially scan a document or photo and then print it, but all with a single press of the Copy button.

Faxing generally requires separate functions in the machine, such as a document feed and a connection to a traditional, analog phone line. Assuming you have those and an account with the local telecom company, the process of faxing is pretty simple. You put a document in the feeder, plug in the fax number, and press the Send button (or whatever the manufacturer labels it).

Automatic Document Feeders
An MFD uses an automatic document feeder (ADF) to grab pages to copy, scan, or fax. An ADF is typically on top of the MFD and you place a stack of pages in the tray (see Figure 26-22). Different machines require documents face up or face down; they’ll typically have some marking to show which way to feed the pages (see Figure 26-23).



Figure 26-22  Typical automatic document feed loaded with pages to copy



Figure 26-23  Wonderfully descriptive markings on MFD telling user to load pages face up in ADF

Connectivity
Most printers, scanners, and multifunction devices connect to a computer via a USB port, but Wi-Fi or Ethernet network connections are also very popular. You’ll need to know how to support network connections as well as the plug-and-play USB ones.

USB Connections
New printers and multifunction devices use USB connections that you can plug into any USB port on your computer. USB printers may not come with a USB cable, so you need to purchase one when you purchase a printer. (It’s quite a disappointment to come home with your new printer only to find you can’t connect it because it didn’t come with a USB cable.) Most printers use the standard USB type A connector on one end and the smaller USB type B connector on the other end, although some use two type A connectors. Whichever configuration your USB printer has, just plug in the USB cable—it’s that easy!

Network Connections
Connecting a printer or multifunction device to a network isn’t just for offices anymore. More and more homes and home offices are enjoying the benefits of network printing. It used to be that you would physically connect the printer to a single computer and then share the printer on the network. The downside to this was that the computer connected to the printer had to be left on for others to use the printer.

Today, the typical network printer comes with its own built-in 802.11 (a, b, g, n, ac, ax) Wi-Fi adapter to enable wireless printing over infrastructure, though you should avoid ad hoc connections for security reasons when possible (see Chapter 20 for more on setting up an ad hoc wireless network).

Other printers include an onboard network adapter that uses a standard RJ-45 Ethernet cable to connect the printer directly to the network by way of a router. The printer can typically be assigned a static IP address, or it can acquire one dynamically from a DHCP server. (Don’t know what a router, IP address, or DHCP server is? Take a look back at Chapter 18 and Chapter 19.) Once connected to the network, the printer acts independently of any single computer. Alternatively, some printers offer a Bluetooth interface for networking.



NOTE   Since printers tend to have longer lives than most other computing devices, be aware that printers with a built-in wireless print connection may be using older Wi-Fi or Bluetooth standards than you’re used to encountering.

Even if a printer does not come with built-in Ethernet, Wi-Fi, or Bluetooth, you can purchase a standalone network device known as a print server to connect your printer to the network—but beware that you may not be able to use all features of an MFD connected to a print server. These print servers, which can be Ethernet or Wi-Fi, enable one or several printers to attach via USB cable (or even parallel port, if you still have a printer that old). You may not need to go to the store to find a print server, though—check your router, first, to see if it has an integrated print server. If it does, you may be able to plug your printer into a USB port on the router. So take that ancient ImageWriter dot-matrix printer and network it—I dare you!



EXAM TIP   As discussed in Chapter 18 in the context of the roles of networked hosts, print servers aren’t necessarily physical devices. You’ll find print servers outside network devices. In fact, your Windows system is capable of operating as a print server. Anytime you plug a printer into a computer and share the printer (printer share) over the network, the sharing system can be referred to as a print server.

Physical Installation
Ooh! Few things are more exciting than installing a new printer, scanner, or MDF in your office! While fun (and always a crowd pleaser), you should consider several factors before you pull out the box cutters!

Location
So where do you put this thing? Not only does your new device need to be in a location that is convenient for everyone who needs to use it, but that location should also provide good power and ventilation. Equally, the device ought to be in a place that’s not in anyone’s way, like a hallway or a person’s office, so that no one is constantly interrupted by people grabbing print jobs.

Unboxing
Unboxing a printer or MFD, especially a large office printer or MDF, is a tricky business and one that should be considered with great care. In particular, read the instructions included with the device before you start unboxing it. The instructions should provide very specific steps in which to unbox the various components of the device.



NOTE   All printers and scanners come with internal packaging that must be removed before use. Again, read the documentation to make sure you don’t overlook removing from the device a piece of Styrofoam or cardboard.

The Laser Printing Process
The imaging process with a laser printer breaks down into seven steps, and the CompTIA A+ 1101 exam expects you to know them all. As a tech, you should be familiar with these phases, as this can help you troubleshoot printing problems. If an odd line is printed down the middle of every page, for example, you know there’s a problem with the imaging drum or cleaning mechanism and the toner cartridge needs to be replaced.

The seven steps to the laser printing process may be performed in a different order, depending on the printer, but it usually goes like this:

1.   Processing

2.   Charging

3.   Exposing

4.   Developing

5.   Transferring

6.   Fusing

7.   Cleaning

Processing
When you click the Print button in an application, several things happen. First, the CPU processes your request and sends a print job to an area of memory called the print spooler. The print spooler enables you to queue up multiple print jobs that the printer will handle sequentially. Next, Windows sends the first print job to the printer. That’s your first potential bottleneck—if it’s a big job, the OS has to dole out a piece at a time and you’ll see the little printer icon in the notification area at the bottom right of your screen. Once the printer icon goes away, you know the print queue is empty—all jobs have gone to the printer.

Once the printer receives some or all of a print job, the hardware of the printer takes over and processes the image. That’s your second potential bottleneck, and it has multiple components.

Raster Images
Impact printers transfer data to the printer one character or one line at a time, whereas laser printers transfer entire pages at a time to the printer. A laser printer generates a raster image (a pattern of dots) of the page, representing what the final product should look like. It uses a device (the laser imaging unit) to “paint” a raster image on the imaging drum. Because a laser printer has to paint the entire surface of the imaging drum before it can begin to transfer the image to paper, it processes the image one page at a time.

A laser printer uses a chip called the raster image processor (RIP) to translate the raster image into commands to the laser. The RIP takes the digital information about fonts and graphics and converts it to a rasterized image made up of dots that can then be printed. An inkjet printer also has a RIP, but it’s part of the software driver instead of onboard hardware circuitry. The RIP needs memory (RAM) to store the data that it must process.

A laser printer must have enough memory to process an entire page. Some pages printed at high resolution and containing very complex designs (lots of fonts, complex formatting, high-resolution graphics, and so on) require more memory. Insufficient memory will usually be indicated by a memory overflow (“MEM OVERFLOW”) error. If you get a memory overflow or low memory error, try reducing the resolution, printing smaller graphics, reducing the complexity, or turning off RET (see the following section for the last option). Of course, the best solution to a memory overflow error is simply to add more RAM to the laser printer.

Do not assume that every error with the word memory in it can be fixed simply by adding more RAM to the printer. Just as adding more RAM chips will not solve every conventional computer memory problem, adding more RAM will not solve every laser printer memory problem. The message “21 ERROR” on an HP LaserJet, for example, indicates that “the printer is unable to process very complex data fast enough for the print engine.” This means that the data is simply too complex for the RIP to handle. Adding more memory would not solve this problem; it would only make your wallet lighter. The only answer in this case is to reduce the complexity of the page image.

Resolution
Laser printers can print at different resolutions, just as monitors can display different resolutions. The maximum resolution a laser printer can handle is determined by its physical characteristics. Laser printer resolution is expressed in dots per inch (dpi), such as 2400 × 600 dpi or 1200 × 1200 dpi. The first number, the horizontal resolution, is determined by how fine a focus can be achieved by the laser. The second number is determined by the smallest increment by which the drum can be turned.

Higher resolutions produce higher-quality output, but keep in mind that higher resolutions also require more memory. In some instances, complex images can be printed only at lower resolutions because of their high memory demands. Even printing at 300 × 300 dpi, laser printers produce far better quality than dot-matrix printers because of resolution enhancement technology (RET).

RET enables the printer to insert smaller dots among the characters, smoothing out the jagged curves that are typical of printers that do not use RET (see Figure 26-24). Using RET enables laser printers to output high-quality print jobs, but it also requires a portion of the printer’s RAM. If you get a MEM OVERFLOW error, disabling RET will sometimes free up enough memory to complete the print job.



Figure 26-24  RET fills in gaps with smaller dots to smooth out jagged characters.

Charging
Now we turn to the physical side of the printing process. To make the drum receptive to new images, it must be charged (see Figure 26-25). Using the primary corona wire or primary charge roller, a uniform negative charge is applied to the entire surface of the drum (usually between ~600 and ~1000 volts).



Figure 26-25  Charging the drum with a uniform negative charge

Exposing
A laser is used to create a positive image on the surface of the drum. Every particle on the drum hit by the laser releases most of its negative charge into the drum.

Developing
Those particles with a lesser negative charge are positively charged relative to the toner particles and attract them, creating a developed image (see Figure 26-26).



Figure 26-26  Writing the image and applying the toner

Transferring
The printer must transfer the image from the drum onto the paper. The transfer corona or transfer roller gives the paper a positive charge; then the negatively charged toner particles leap from the drum to the paper. At this point, the particles are merely resting on the paper and must still be permanently fused to the paper.

Fusing
The particles have been attracted to the paper because of the paper’s positive charge, but if the process stopped here, the toner particles would fall off the page as soon as you lift it. Because the toner particles are mostly composed of plastic, they can be melted to the page. Two rollers—a heated roller coated in a nonstick material and a pressure roller—melt the toner to the paper, permanently affixing it. Finally, a static charge eliminator removes the paper’s positive charge (see Figure 26-27). Once the page is complete, the printer ejects the printed copy and the process begins again with the physical and electrical cleaning of the printer.



Figure 26-27  Transferring the image to the paper and fusing the final image



CAUTION   The heated roller produces enough heat to melt some types of plastic media, particularly overhead transparency materials. This could damage your laser printer (and void your warranty), so make sure you print on transparencies designed for laser printers!

Cleaning
The printing process ends with the physical and electrical cleaning of the imaging drum (see Figure 26-28). Before printing another new page, the drum must be returned to a clean, fresh condition. All residual toner left over from printing the previous page must be removed, usually by scraping the surface of the drum with a rubber cleaning blade. If residual particles remain on the drum, they will appear as random black spots and streaks on the next page. The physical cleaning mechanism either deposits the residual toner in a debris cavity or recycles it by returning it to the toner supply in the toner cartridge. The physical cleaning must be done carefully—a damaged drum will cause a mark to be printed on every page until it is replaced.



Figure 26-28  Cleaning and erasing the drum

The printer must also be electrically cleaned. One or more erase lamps bombard the surface of the drum with the appropriate wavelengths of light, causing the surface particles to discharge into the grounded drum. After the cleaning process, the drum should be completely free of toner and have a neutral charge.



NOTE   Color laser printers use four different colors of toner (cyan, magenta, yellow, and black) to create their printouts. Most models send each page through four different passes, adding one color at each pass to create the needed results, while others place all the colors onto a special transfer belt and then transfer them to the page in one pass. In some cases, the printer uses four separate toner cartridges and four lasers for the four toner colors, and in others the printer simply lays down one color after the other on the same drum, cleaning after each of four passes per page.

Installing a Multifunction Device
Installing a multifunction device differs a lot from installing single-function devices. In the consumer space, the process is messy because of the complexity of the devices. Here’s the scoop.

First, most multifunction devices today connect via USB and wirelessly, so you need to consider connectivity. Second, you need to install drivers for each of the various functions of the MFD. Initially, that seems fine, because you can use the driver disc/download that came with the MFD and can install everything for the OS you choose.

That default process can rapidly turn into a mess, though, because of several factors. The drivers are often outdated. Updating specific drivers takes time and clicking. Worse, manufacturers often add absurdly bad applications to “support” specific functions of MFDs, such as special photo organization tools that bog down the system and function far worse than readily available tools like Lightroom from Adobe (not free, but reasonably priced).

Third, you’re dealing with a very complex machine that can break in interesting ways. Maintenance and troubleshooting take on new dimensions by the sheer number of options to consider, from ink levels to scanner mechanics to dogged-out phone lines. Although none of these fall into the category of installation, you can minimize the problems by practicing a more compartmentalized installation.

Rather than focus on the multifunction aspect of MFDs, you will often fare better for you and your customers if you think about each function as a separate action. Pull the machine apart in essence, for example, and install a printer, a scanner, a copy machine, and a fax machine. Share these individual parts as needed on a network. Update drivers for each component separately. Conceptualize each function as a separate device to simplify troubleshooting. This way, if your print output goes south, for example, think about the printer aspects of the MFD. You don’t have to worry about the scanner, copy, or fax aspects of the machine.

The next sections cover installation of single-function devices, though the bulk of information is on printers. That’s both what the CompTIA A+ exams cover and what you’ll have to deal with as a tech for the most part.



EXAM TIP   The CompTIA A+ exams test you on installing and troubleshooting printers, so read these sections carefully!

Setting Up Printers in Windows
You need to take a moment to understand how Windows handles printing, and then you’ll see how to install, configure, and troubleshoot printers.

To Windows, a printer is not a physical device; it is a program that controls one or more physical printers. The physical printer is called a print device by Windows (although I continue to use the term “printer” for most purposes, just like almost every tech on the planet). Printer drivers and a spooler are still present, but in Windows, they are integrated into the printer itself (see Figure 26-29). This arrangement gives Windows amazing flexibility. For example, one printer can support multiple print devices, enabling a system to act as a print server. If one print device goes down, the printer automatically redirects the output to a working print device.



Figure 26-29  Printer driver and spooler in Windows

The general installation, configuration, and troubleshooting issues are basically identical in all modern versions of Windows. Here’s a review of a typical Windows printer installation. Setting up a printer is quite easy. Most printers are plug and play, so installing a printer is reduced to simply plugging it in and loading the driver if needed. With USB printers, Windows won’t even wait for you to do anything; Windows immediately detects and installs a printer once you connect it.

If Windows does not immediately detect the printer, you can use the classic Devices and Printers applet in the Control Panel (introduced in the “Sharing Printers” section of Chapter 19), but most users will opt for the simpler Settings | Devices | Printers & scanners interface for setting up a printer (see Figure 26-30). Click the Add a printer or scanner option to find a connectable printer.



Figure 26-30  Printers & scanners in Settings

Standard Users and Printers

A standard user—that is, not an administrator—can install a printer just fine in Windows. The user can also use one of the built-in printer drivers and print fine.

Windows will balk with an “Unable to install printer. Operation could not be completed” error message and accompanying code when the user tries to install software and drivers from an optical disc or downloaded from the Internet. For those options, you need administrative rights.

If you’re stuck in that position, such as rolling out corporate laptops to company employees who will want to install printers at home, you can work around the problem. Microsoft suggests changing the Group Policy Driver Installation policy to allow non-administrators to install drivers for printers.

You should be able to find detailed instructions on this if need be at https://docs.microsoft.com. We’ll discuss Group Policy editing in Chapter 27.

The Add Printer Wizard and the Settings app both let you install a local printer or a network printer. This distinction is actually a little misleading. Windows divides printer installation into two scenarios: a printer connected directly to a computer (your local system or another one on a network), or a standalone printer directly connected to a switch or router. While you might expect the local and network installation options to divide these scenarios nicely, they don’t. Let’s take a quick look at both local and network installations so you know when to use each.

Installing a Local Printer
At first glance, you might think the local printer installation option is used to install your standard USB printer, but don’t forget that Windows will automatically detect and install USB printers (or any other plug-and-play printer). So what do you use it for? This option is most commonly used to install standalone network printers using an IP address. Using current versions of Windows and a modern printer, you shouldn’t need the IP address to install a standalone network printer, but it can be a helpful alternative if Windows refuses to detect it any other way.

If you need to install a standalone network printer, use its hostname or IP address. In Windows, click Add a printer or scanner (shown in Figure 26-30). If Windows doesn’t automatically detect your new printer, click The printer that I want isn’t listed and select Add a printer using TCP/IP address or hostname. In Windows 10 and 11, both the Settings app and the Control Panel app give you the same choices.

Whether you use a USB port or a TCP/IP port, you’ll need to select the proper driver manually (see Figure 26-31). Windows includes a lot of printer drivers, but you can also use the handy Have Disk option to use the disc that came with the printer. If you use the driver included on the disc, Windows will require administrator privileges to proceed; otherwise, you won’t be able to finish the installation. The Windows Update button enables you to grab the latest printer drivers via the Internet.



Figure 26-31  Selecting drivers

After clicking the Next button, you’ll be asked if the new local printer should be the default printer and whether you want to share it with other computers on the network. And before you ask, yes, you can share a standalone network printer connected to your computer via a TCP/IP port using the File and printer sharing option located at Control Panel | Network and Sharing Center | Change advanced sharing settings, though the printer would be disabled for other users any time you turned off your computer. You’ll be asked to print a test page to make sure everything works. Then you’re done!



NOTE   Windows-based printer sharing isn’t the only game in town. Apple’s AirPrint functionality can be used in conjunction with its Bonjour Print Service (installed separately, or along with iTunes) to share a printer connected to a Windows system with AirPrint-compatible macOS and Apple iOS devices.

Installing a Network Printer
Setting up network printers in a typical SOHO LAN doesn’t require much more effort than setting up local printers. When you try to install a network printer, the Settings app or Add Printer Wizard will scan for any available printers on your local network. More often than not, the printer you are looking for will pop up in a list (see Figure 26-32). When you select that printer and click Add device or Next, Windows will search for drivers. If you need to, you can pick from a list of available drivers or use the disc that came with the printer. Either way, you’re already done.



Figure 26-32  List of available shared printers on a network

If Windows fails to find your printer, you’ll need to configure the network printer manually. Every version of Windows includes multiple methods of doing this. These methods change depending on whether you are connected to a domain or a workgroup.



NOTE   Remember printer sharing from Chapter 19? Here’s the other side of the operation. Keep in mind that after you install a shared printer onto your computer, you can actually share it with others. Windows considers it your printer, so you can do what you want with it, including sharing it again.

If you are on a workgroup, you can browse for a printer on your network, connect to a specific printer (using its name or URL), or use a TCP/IP address or hostname, as you see in Figure 26-33. In a domain, most of these options remain the same, except that instead of browsing the workgroup, you can search and browse the domain using several search parameters, including printer features, printer location, and more. Once you’ve found your printer, you might be prompted for drivers. Provide them using the usual methods described earlier and then you are finished!



Figure 26-33  Options for finding network printers

Remember that Windows doesn’t always see your network’s printers exactly how they are physically arranged. Imagine you have a network with three computers. Andy’s computer has a printer connected via USB, whereas Beth’s computer and Carol’s computer have no printers. There is, however, a second printer connected directly to their router via Ethernet. Beth has configured her system to connect directly to the network printer using an IP address. As a result, she can actually share that printer with the rest of her network, even though it’s not attached to her computer—Windows doesn’t care where it is. The process for sharing a local printer and a network printer is identical because Windows considers both printers to be installed on your computer and under your control. So now Andy and Beth both share printers. When Carol goes looking for shared printers to use, the network printer attached to the router will look like Beth’s printer, as if it were directly connected to Beth’s machine.

Figure 26-34 shows the Printers & scanners screen on a system with multiple printers installed. Note the text Default below the printer’s name; this shows that the device is the default printer. If you have multiple printers, you can change the default printer by right-clicking the printer’s icon and selecting Set as default printer.



Figure 26-34  Installed default printer in Printers & scanners in Settings

In addition to the regular driver installation outlined previously, some installations use printer emulation. Printer emulation simply means using a substitute printer driver for a printer, as opposed to using one made exclusively for that printer. You’ll run into printer emulation in two circumstances. First, some new printers do not come with their own drivers. They instead emulate a well-known printer (such as an HP LaserJet) and run perfectly well on that printer driver. Second, you may see emulation in the “I don’t have the right driver!” scenario. I keep about three different HP LaserJet and Epson inkjet printers installed on my computer because I know that with these printer drivers, I can print to almost any printer. Some printers may require you to set them into an emulation mode to handle a driver other than their native one.

1102
As you might imagine, setting up printers and MFDs in an enterprise environment differs from the process in a SOHO environment. Here’s a scenario. Bayland Widgets Corporation has 30 users who share access to two high-end color laser printers, two very fast black-and-white laser printers, one MFD (mainly used for scanning and copying purposes, but it also prints), and a trio of very nice inkjet printers. The printers and MFD are located in various places for convenience and managed by a single print server.

To make things a lot simpler than going to each client machine and installing these networked printers, Tony the Admin deploys the printers and MFD using Windows group policy to map the correct printers for all 30 workstations (plus several laptops as well). As users log in each morning, the group policy maps the MFD and the closest color laser printer to all of the workstations and laptops. It only maps the high-quality inkjet printers to the marketing department workstations, however, and the fast black-and-white laser printers to accounting. This all happens automatically with the correct drivers loaded as necessary.



NOTE   Sharing a printer or MFD in a SOHO LAN is pretty easy. It’s also easy to install a shared network printer. Once you scale up, though, management of many workstations and printers/MFDs becomes a pain unless you map via a group policy that applies to a lot of computers or users. You can also automate printer mapping via an Active Directory domain logon script, as discussed back in Chapter 19.

We’ll hit group policy in Chapter 27. But deploying or mapping printers and multifunction devices in this way enables much faster rollout, updates, replacements, and so on.



NOTE   In addition to the Devices and Printers applet, Windows also includes the Print Management console. This tool enables you to view and modify the printers and drivers on your system, connected to your network, or manage any Windows print servers connected to the network. Many of Print Management’s advanced features go beyond the scope of the CompTIA A+ exams, but know that it centralizes (and in a few cases, enhances) the standard printer controls in Windows. You can find Print Management in Control Panel | Administrative Tools | Print Management. However, note that Windows 10 Home doesn’t offer Print Management.

Configuring Print Settings
Once your printer is installed, a good first stop is the Printing preferences menu, accessible by right-clicking the desired printer in the Devices and Printers applet in the Control Panel. This is where you’ll be able to control how your printer will print your documents. Be aware that these settings can vary depending on features available on your printer or multifunction device, but let’s take a look at some of the ones you’re most likely to find.

Layout
The settings you’re most likely to change from time to time are probably the layout settings, which control how the printer determines what to print where.

•   The duplex setting lets you specify whether and how to use each side of a printed page. Simple duplexing will just use the front and back of each sheet sequentially, but you may find more advanced options for laying out booklets.

•   The orientation setting lets you specify whether to print in landscape or portrait mode.

•   The multiple page setting will let you print multiple document pages on each physical page.

•   The scaling setting, not to be confused with the multiple page setting, is usually for fitting a large document to a single page or scaling a small document up to the size of a full page.

•   Reverse or invert options let you print the mirror image of your document, which is useful for printing on transfer paper and other special-use cases.

Paper
Many of the settings you’ll find are for telling your printer what kind of paper it will be using, and (especially if the printer has multiple paper trays) where to find it.

•   Set the paper size to one of several common paper sizes or define a custom one.

•   Specify the paper type, which may involve setting thickness, coating, and special formats such as envelopes and labels.

•   A paper source setting will let you select any available paper settings, and possibly manual feed, in which case the printer will wait for you to feed it each sheet individually. This is useful if you need to feed in one-off items or paper that won’t fit in the tray.

•   Tray settings allow you to select the printer tray to input the paper (if there are multiple trays). Many printers have the option to choose “automatically select” which also tells the printer to pull the paper from the main tray. When the main tray is out of paper, the printer will automatically choose another tray that has existing paper.

Quality
There are usually a number of different settings that have bearing on quality, but you should be aware that the name or description of some settings that affect quality may discuss ink or toner use (and may as such be located with other ink/toner-related settings).

•   The most obvious of these, resolution, specifies what dpi the document should be printed at.

•   Some printers may let you choose some mode or quality presets that optimize printing for graphics or text or choose to manually configure your own advanced settings.

•   Some printers may have settings that reduce ink or toner used, for economic and environmental reasons.

Other Common Settings
Some print devices offer options useful in specific, but limited, occasions.

•   The apply a watermark setting will let you choose from presets or define your own. A watermark is a lightly printed mark across every page. Use a watermark to designate a draft copy of a document, for example, rather than a final copy.

•   Header/footer settings can be used to add information about when a document was printed and who printed it.

•   A collate option lets you specify the order in which multiple copies of a multi-page document are printed. If the option is unchecked and you print ten copies, each page will be printed ten times before the printer moves on. If the option is checked, the printer will print the full document before starting over.

Optimizing Print Performance
Although a quality printer is the first step toward quality output, your output relies on factors other than the printer itself. If you’ve ever tweaked a photograph until it looked perfect on your screen only to discover the final printout was darker than you hoped, you made an important discovery. What you see on the screen may not match what comes out of the printer unless both devices are properly calibrated.

Color calibration uses hardware to generate an International Color Consortium (ICC) color profile, a file that defines the color characteristics of a hardware device. The operating system then uses this profile to correct any color shifts in your monitor. With a calibrated monitor, you know any color shifts in your photograph are really in the photo, not an artifact of your monitor.



EXAM TIP   Calibration is a general term for a manual or automatic process that corrects differences between how a device or component currently works and how it should work. All kinds of devices need calibration, but the CompTIA A+ 1101 objectives focus on calibrating inkjet and laser printers. This section describes one kind of calibration—but keep an eye out for additional calibration steps in the “Inkjet Printer Maintenance” and “Laser Printer Maintenance” sections later in this chapter.

Where these ICC color profiles really start to get interesting is that they can be created for printers as well. Just like with a monitor, they let the computer know the unique color quirks of a specific printer on a specific paper. When your printer and monitor have been properly calibrated and the profiles installed, your prints and monitor display should match. Color profiles are sometimes included on the installation media with a printer, but you can create or purchase custom profiles as well. Windows includes Windows Color System (WCS) to help build color profiles for use across devices. WCS is based on a newer component Microsoft calls the color infrastructure and translation engine (CITE).



NOTE   Two of the best monitor calibration hardware manufacturers are Datacolor Spyder—that’s the one I use most—and X-Rite ColorMunki Display. Get one. You’ll be much happier with your print outcome! Here are the main URLs: https://www.datacolor.com and https://www.xrite.com.

Managing Public/Shared/Networked Devices
While we’ve looked at a few of the ways you can share a printer or multifunction device over a network, there’s more to know about sharing these devices than just how to set them up. A few big issues are network security and data privacy.

Network Print Security
The ease of access that makes wired or wireless network printers and multifunction devices so useful is also a big risk; networked printers are subject to unique security issues. Luckily for us, the CompTIA A+ exams concentrate on just a few basic but important security issues with printer and multifunction devices, so let’s look at these.

User Authentication  Allowing only the right people to use a device is an old issue and one that’s been covered in one way through user permissions in Windows, but there’s more to user authentication. For example, what if you have an expensive color laser printer? Many color laser printers use user authentication to determine, for example, if a user can print color or only black and white. These types of user authentications are based in the printer or printer server but happily work with Windows domains. In Windows 10, printer authentication can be configured in Printers and scanners.

Badging  Who hasn’t seen the classic episode of The Office where Dwight requires everyone to use a badge to access the photocopier? While individual codes are rare, user badges that enable you to scan or photocopy are still quite common. These badges use every kind of technology, although NFT is the most common.

Audit Logs  Printers and scanners have audit logs just like any other device. These logs commonly reside in the printer itself, although other solutions work with Windows Event Viewer or Linux Syslog. The bottom line is that if you want to know what happened to a printer, check the logs!

Secured Prints  Ever find yourself printing something you don’t want others to see? Do you ever find yourself running to the printer to grab it before anyone can see? That’s what secure printing is all about.

Secure printing works by first requiring the user to enter a password or PIN code before a print job starts. After the job is sent to the printer (or print server), the job doesn’t automatically print. To make the job print, the user must enter the passcode again at the printer, therefore making sure no one but that user can see the confidential print job.

If you think about it, a lot of sensitive information can pass through a printer or MFD in most organizations, especially in places like schools and hospitals where privacy is strictly regulated. When all of this information passes through the printer or MFD, it’s important to make sure it isn’t leaking out. Unfortunately, it’s common for modern devices to contain a hard drive or other storage media used to cache copies of documents the device prints, scans, copies, or faxes. Depending on the device, you may be able to disable this feature, schedule regular deletion of the cache, or manually clear the cache regularly to limit the amount of damage a compromise could cause. It’s also important to clear this information before disposing of the device.

Disabling features like this wouldn’t be much good if anyone who could use the device could also change the settings, so enterprise models often allow for user authentication on the device. This can address a number of the risks these devices present by limiting use to authenticated users and restricting the features each user can access to only what they need.

Just because the data on your device is secure doesn’t mean documents rolling off of it are free from prying eyes. User authentication can also help out by letting users send documents to the printer but waiting to print them until the user authenticates at the device. It can also minimize some of the risk to unsupervised documents by restricting the ability of less-trusted users to scan/copy/e-mail a document from the device, limiting the ease with which they could steal a copy of an unattended document and leave the original.



NOTE   Every printer is different. Read the documentation included with your printer to learn how you can perform the tasks listed in this section.

1101
Maintaining and Troubleshooting Printers
Once set up, printers tend to run with few issues, assuming that you install the proper drivers and keep the printer well maintained. But printer errors do occasionally develop. This section provides an overview of troubleshooting the most common print problems, as well as problems that crop up with specific printer types.

Maintaining and Troubleshooting General Issues
Printers of all stripes share some common problems, such as print jobs that don’t print, strangely sized prints, and misalignment. Other issues include disposing of consumables, sharing multiple printers, and crashing on power-up. Let’s take a look at these general troubleshooting issues, but start with a recap of the tools of the trade.



NOTE   Don’t forget to check the obvious. Many printers include tiny displays that can clue you in to what’s wrong. Most brands use a series of error codes that indicate the problem. Use the manual or the manufacturer’s Web site to translate the error code into meaningful information.

Tools of the Trade
Before you jump in and start to work on a printer that’s giving you fits, you’ll need some tools. You can use the standard computer tech tools in your toolkit, plus a couple of printer-specific devices. Here are some that will come in handy:

•   A multimeter for troubleshooting electrical problems such as faulty wall outlets

•   Various cleaning solutions, such as denatured alcohol

•   An extension magnet for grabbing loose screws in tight spaces and cleaning up iron-based toner

•   An optical disc or USB thumb drive with test patterns for checking print quality

•   Your trusty screwdrivers—both a Phillips-head and flat-head, because if you bring just one kind, it’s a sure bet that you’ll need the other

Print Job Never Prints
If you click Print but the printer will not print, first check all the obvious explanations. Is the printer on? Is it connected? Is it online? Is there an error message on its display? Does it have paper? Is your computer online?

If the printer is on, the display might have a useful message. It’ll usually let you know if the printer is out of paper, has a paper jam that needs to be resolved, or has had a memory full/low memory error. If so, refill the paper, resolve the jam, or try reprinting the job at a lower quality, accordingly.

If you can’t connect to the printer, check all cables, ports, and power involved. If everything is plugged in and ready to go, check the printer’s display for any indication that it has no connectivity (you may need to navigate its menu system to view its connectivity status). If the printer was previously connected, turn it off for a moment, and then turn it back on and see if it successfully connects. If it doesn’t, the menu system will typically have an option to manually configure network settings. Try resetting or manually configuring them.

If the printer does have connectivity, double-check the appropriate printer applet for your version of Windows. If you don’t see the printer you are looking for, you’ll need to reinstall it.

If you attempt to use a printer shared by another computer but Windows pops up with an “Access Denied” error, you might not have permission to use the printer. Go to the host system and check the Security tab of the Printer Properties dialog box. Make sure your user account is allowed to use the printer.

Assuming the printer is in good order, it’s time to look at the spooler. You can see the spooler status either by double-clicking the printer’s icon in the appropriate printer Control Panel applet or by double-clicking the tiny printer icon in the notification area if it’s present. If you’re having a problem, the printer icon will almost always be there. Figure 26-35 shows the print spooler status window open.



Figure 26-35  Print spooler status

Multiple prints pending in a queue can easily overflow or become corrupt due to a lack of disk space, too many print jobs, or one of a thousand other factors. The status window shows all of the pending print jobs and enables you to delete, start, or pause jobs. I usually just delete the affected print job(s) and try again.

Print spoolers are handy. If the printer goes down, you can just leave the print jobs in the spooler until the printer comes back online. If you have a printer that isn’t coming on anytime soon, you can simply delete the print job in the spooler window and try another printer.

If you have problems with the print spooler, you can get around them by changing your print spool settings. Go into the Printers/Devices and Printers applet, right-click the icon of the printer in question, and choose Printer properties. In the resulting Properties dialog box (see Figure 26-36), choose the Print directly to the printer radio button on the Advanced tab and click OK; then try sending your print job again. Note that this window also offers you the choice of printing immediately—that is, starting to print pages as soon as the spooler has enough information to feed to the printer—or holding off on printing until the entire job is spooled.



Figure 26-36  Print spool settings

If that isn’t enough, try restarting the print spooler service. Right-click the Start button and select Computer Management. In the column on the left, double-click Services and Applications, and then click Services. The Services console should appear in the center of the Computer Management window. Scroll down and find the service named Print Spooler. Right-click the service and simply click Restart, if available; otherwise, click Stop, wait for it to stop, right-click the service again, and select Start. You should be able to print using the print spooler again.

Another possible cause for a stalled print job is incorrect paper size—the printer is simply waiting for the correct paper! Laser printers in particular have settings that tell them what size paper is in their standard paper tray or trays. If the application sending a print job specifies a different paper size—for example, it wants to print a standard No. 10 envelope, or perhaps a legal sheet, but the standard paper tray holds only 8.5 × 11 letter paper—the printer usually pauses and holds up the queue until someone switches out the tray or manually feeds the type of paper that this print job requires. You can usually override this pause, even without having the specified paper, by pressing the OK or GO button on the printer.

The printer’s default paper tray and paper size options will differ greatly depending on the printer type and model. To find these settings, go into the printer’s Properties dialog box from the Printers/Devices and Printers applet, and then select the Device Settings tab. This list of settings includes Form to Tray Assignment, where you can specify which tray (in the case of a printer with multiple paper trays) holds which size paper.

Strange Sizes
A print job that comes out an unexpected size usually points to a user mistake in setting up the print job. All applications have a Print command and a Page Setup interface. The Page Setup interface enables you to define a number of print options, which vary from application to application. Figure 26-37 shows the Page Setup options for Microsoft Word. Make sure the page is set up properly before you blame the printer for a problem.



Figure 26-37  Page Setup options for Microsoft Word

If you know the page is set up correctly, recheck the printer drivers. If necessary, uninstall and reinstall the printer drivers. If the problem persists, you may have a serious problem with the printer’s print engine, but that comes up as a likely answer only when you continually get the same strangely sized printouts using a variety of applications.

Grinding Noises
The only noise you want to hear from your printer is the printing of a document. Sometimes, however, we may try to either stuff too much paper in the tray, or the paper feeder is misaligned and you hear awful grinding noises. All you have to do is realign the paper in the paper feeder. You may also want to take a look at the rollers to see if they need some cleaning.

Finishing Issues/Staple Jams and Hole Punches
Some of the more high-end printers have built-in staplers and capabilities to place hole punches into documents—which is fantastic. However, what is not so great is when you experience a staple jam or hole punch error on your control panel. Fixing a staple jam in a printer is much like fixing a staple jam in a stapler. You open up the stapling mailbox, remove the stapler cartridge and any jammed staples, insert the cartridge back into the stapling mailbox and your stapler jam is fixed. With a hole punch print option there may be compatibility issues when you combine printing options (stapling and hole punch). Also, feeding the paper in horizontally (rather than vertically) sometimes creates some issues.

Incorrect Page Orientation
Have you ever tried to print a document that you intended to output as portrait, but instead came out as a landscape orientation? Incorrect page orientation settings can be easily fixed by going to your Printer settings | Printing preferences | Orientation and selecting which page orientation you would prefer before you print.

Misaligned or Garbage Prints
Misaligned or garbage printouts (CompTIA calls this garbled print) often point to a corrupted or incorrect driver, but it’s worth trying to reboot the printer before jumping to conclusions. If that doesn’t help, make sure you’re using the right driver (it’s hard to mess this up, but not impossible) and then uninstall and reinstall the printer driver. If the problem persists, you may be asking the printer to do something it cannot do. For example, you may be printing to a PostScript printer with a PCL driver. Check the printer type to verify that you haven’t installed the wrong type of driver for that printer!

If none of these solutions help, it’s also worth making sure there isn’t a data cable or power issue. Swap out the data cable for one you know is good. Move the printer to another outlet (with no power strip or surge protector). If the printer supports more than one type of connection, try a different one.

Dealing with Consumables
All printers tend to generate a lot of trash in the form of consumables. Impact printers use paper and ribbons, inkjet printers use paper and ink cartridges, and laser printers use paper and toner cartridges. In today’s environmentally sensitive world, many laws regulate the proper disposal of most printer components. Be sure to check with the local sanitation department or disposal services company before throwing away any component. Of course, you should never throw away toner cartridges—certain companies will pay for used cartridges!

Both laser printers and computers require more power during their initial power-up (the POST on a computer and the warm-up on a laser printer) than once they are running. HP recommends a reverse power-up. Turn on the laser printer first and allow it to finish its warm-up before turning on the computer. This avoids having two devices drawing their peak loads simultaneously.



NOTE   When in doubt about how to dispose of any computer component, check a material safety data sheet (MSDS). These standardized forms provide detailed information about potential environmental hazards associated with different components but also proper disposal methods. For example, surf to https://epson.com/support/sds to find the latest MSDS for all Epson products. This isn’t just a printer issue—you can find an MSDS for most computer components.



EXAM TIP   MSDSs contain important information regarding hazardous materials such as safe use procedures and emergency response instructions. An MSDS is typically posted anywhere a hazardous chemical is used.



NOTE   Used toner cartridges are toxic to the environment, so you need to dispose of them properly. There are some different ways to do this and do your part in saving our earth and water. You can take them to a supply store like Office Depot; place them in a plastic bag and deposit into a green recycle bin; or send them back to the manufacturer.

Incorrect Chroma Display
If you print in color, sooner or later something is going to come out in the wrong color. A good first step is printing out the appropriate diagnostic/test page—this should help separate problems with the printer from problems with what or how you’re printing.

Some pretty simple things can cause an incorrect chroma display, so let’s check those first. If you print a document with color and it comes out in black and white, double-check both the app you used to print and your print settings to make sure they aren’t configured to use grayscale. Double-check the color ink/toner levels.

If something you expected to come out black comes out an odd tone, your printer may be low on black ink/toner. Colors that appear black may be a rich black with other colors mixed in—if there isn’t enough black in the mix, you might end up with something unexpected.

If your printer’s color registration is out of whack, you might see a sliver of unexpected color (usually cyan, magenta, or yellow) to either side of larger elements. This can be less obvious with text—it may just look blurry, discolored, or appear to have an unexpected shadow. If so, run your printer’s registration or alignment routine.

Check the print settings on your system and the printer itself to see if it’s configured to adjust any colors. If so, it may be misconfigured. If your printer has a color calibration routine, run it to see if the issue improves. It’s also possible your system is using the wrong color profile for either the printer or the monitor. In the first case, your printer might be right and your monitor might be wrong. Make sure your system isn’t using an incorrect color profile for either device. If the profiles are correct and you have the right tools to color calibrate either device, go ahead and do so.

Some reasons for color problems are a lot less fun. If your printer has separate cartridges or tanks for different colors, it’s possible someone installed the wrong color in one of the slots/tanks. If it’s an inkjet, someone will need to spend a good bit of time cleaning the incorrect ink out of the tubing and printheads. If the right colors are in the right slots, a gunked-up printhead may be keeping the printer from laying down the right amount of a color—but the solution will still be cleaning.

No Image on Printer Display
The small menu display screens included on many modern printers and multifunction devices can, like any other display screen, have a number of issues. The display might freeze or get stuck on a specific screen; it might not come on at all; it might light up but never show an image; it might only display a single color, have artifacts such as lines showing on the display, or even just slowly fade from decades of steady use. Unfortunately, there’s not a lot you can do about these problems. Turning the device off and back on is a good start, and some manufacturers recommend completely unplugging it for a few minutes. If the screen is still misbehaving but the device is otherwise functional and the problem didn’t appear immediately after a firmware update, it’s time to take the device to a service center.

Maintaining and Troubleshooting Impact Printers
Maintaining an impact printer is a lot like scheduling regular maintenance on your car. When you treat your car with care and love, it will return the love by not having as many problems and visits to the mechanic. Although maintaining an impact printer may seem overwhelming, this regular maintenance is offset by the few problems you’ll encounter with them.

Impact Printer Maintenance
Impact printers require regular maintenance but will run forever as long as you’re diligent. Keep the platen (the roller or plate on which the pins impact) and the printhead clean with denatured alcohol. Be sure to lubricate gears and pulleys according to the manufacturer’s specifications. Never lubricate the printhead, however, because the lubricant will smear and stain the paper. Don’t forget to replace the ink ribbon every so often.

Most impact printers use paper continuously fed from a roll or ream, so changing or replacing the paper is a little more involved than adding sheets to the tray. First you’ll need to swap out the rolls or move the new ream into position, and then you’ll need to feed the new paper. If there is already paper in the printer, you’ll need to finish feeding it out first. Like with other printers, paper quality, debris, and improperly fed paper can all lead to jams, which you’ll typically clear by feeding the paper one way or the other.

For all of these processes, look up the printer’s documentation; if you don’t follow the instructions, there’s a chance you’ll damage the printer. There’s often a manual feeding wheel or roller, or you may just need to pull the paper firmly from one side of the printer; both of these can break the feeding system if performed improperly.

Impact Printer Problems
The primary issues to troubleshoot are bad-looking text and bad-looking pages. White bars going through the text point to a dirty or damaged printhead. Try cleaning the printhead with a little denatured alcohol. If the problem persists, replace the printhead. Printheads for most printers are readily available from the manufacturer or from companies that rebuild them. If the characters look chopped off at the top or bottom, the printhead probably needs to be adjusted. Refer to the manufacturer’s instructions for proper adjustment. If the characters have simply degraded or grown faint over time and your printer is used frequently, the printhead may be wearing out; replace it.

Bad-Looking Page
If the page is covered with dots and small smudges—the “pepper look”—the platen is dirty. Clean the platen with denatured alcohol. If the print is faded, and you know the ribbon is good, try adjusting the printhead closer to the platen. If the print is okay on one side of the paper but fades as you move to the other, the platen is out of adjustment. Platens are generally difficult to adjust, so your best plan is to take it to the manufacturer’s local warranty/repair center.

Maintaining and Troubleshooting Thermal Printers
Compared to other printer styles, thermal printers are simple to troubleshoot and maintain. With direct thermal printers, you only need to worry about three things: the heating element, the rollers, and the paper. With thermal wax printers, you also need to care for the wax ribbon.

Thermal Printer Maintenance
To clean the heating element, turn off the thermal printer and open it according to the manufacturer’s instructions. Use denatured alcohol and a lint-free cloth to wipe off the heating element. You might need to use a little pressure to get it completely clean. Clean the rollers with a cloth or compressed air. Make sure to remove debris so they can properly grip the paper. Replacing the paper is as easy as sliding off the old roll and replacing it with a new one. Remember to feed the paper through the heating element, because otherwise you won’t print anything. Replacing the ribbon is similar to replacing the roll of paper; make sure to feed it past the heating element, or the printer won’t work properly. Your printer’s manufacturer should include any special instructions for installing a new ribbon.

Maintaining and Troubleshooting Inkjet Printers
Maintenance on inkjet printers is interesting. One would think that using a printer on a regular basis would make it prone to more issues, right? Not the inkjet printer. They rely on regular use (but not abuse) to minimize printing issues, therefore minimizing the need to troubleshoot.

Inkjet Printer Maintenance
Inkjet printers are reliable devices that require little maintenance as long as they are used within their design parameters (high-use machines will require more intensive maintenance). Because of the low price of these printers, manufacturers know that people don’t want to spend a lot of money maintaining them.

If you perform even the most basic maintenance tasks on inkjet printers, they will soldier on for years without a whimper. Inkjets generally have built-in maintenance programs that you should run from time to time to keep them in good operating order. Inkjet printers don’t get nearly as dirty as laser printers, and most manufacturers do not recommend periodic cleaning. Unless your manufacturer explicitly tells you to do so, don’t vacuum an inkjet. Inkjets generally do not have maintenance kits, but most inkjet printers come with extensive maintenance software (see Figure 26-38). Usually, the hardest part of using this software is finding it in the first place. Look for an option in Printing Preferences, a selection on the Start menu, or an option on the printer’s management Web page. Don’t worry—it’s there!



Figure 26-38  Inkjet printer maintenance screen

When you first set up an inkjet printer, it normally instructs you to perform a routine to align, or to calibrate the printheads properly. Specifics differ, but the printer will usually print at least one test page and either ask you to place it in the scanner (if it has one) or use the menu to indicate which sets of numbered lines align best. If this isn’t done, the print quality will show poor color registration—a fancy way of saying the different color layers that make up your print aren’t aligned properly. The good news is that you can perform this procedure at any time. If a printer is moved or dropped or it’s just been working away untended for a while, it’s often worth running the alignment/registration routine. Some printers will even do this automatically from time to time.

Replacing cartridges in inkjet printers usually is easy, but the exact process can vary widely from printer to printer. Refer to the documentation, but typically you’ll open a compartment on the printer and see one or more cartridges attached to the printhead. If the printhead isn’t accessible, don’t try to force it out; printheads often move to the center of the printer for easy access, in which case you’ll need the printer to be on before you replace cartridges.

Cartridges may simply slide into place, but the printer may also have clips to lock them in. Check the clips or slots on the printhead for an indicator of which cartridge goes where. Follow the manufacturer’s instructions for removing the cartridge you need to change, then remove the new cartridge from its packaging. Look for a piece of tape or other protective covering over its nozzles or contacts; you’ll need to remove that before inserting it. Make sure you follow the insertion process carefully, as an improperly seated cartridge may catch on other components when the printhead moves. Once you insert the new cartridges and close the compartment, the printhead should move back into place.

Did I say that you never should clean an inkjet? Well, that may be true for the printer itself, but there is one part of your printer that will benefit from an occasional cleaning: the inkjet’s printer head nozzles. The nozzles are the tiny pipes that squirt the ink onto the paper.



NOTE   All inkjet inks are water-based, and water works better than denatured alcohol to clean them up. Every inkjet printer has a different procedure for cleaning the printhead nozzles. On older inkjets, you usually have to press buttons on the printer to start a maintenance program. On more modern inkjets, you can access the head-cleaning maintenance program from Windows.



CAUTION   Cleaning the heads on an inkjet printer is sometimes necessary, but I don’t recommend that you do it on a regular basis as preventive maintenance. The head-cleaning process uses up a lot of that very expensive inkjet ink—so do this only when a printing problem seems to indicate clogged or dirty printheads!

Definitely use inkjet printers regularly—that’s good maintenance. Keeping the ink flowing through the printheads prevents them from drying up and clogging. If you don’t have anything “real” to print for a week, run a test page.

Inkjet Printer Problems
A common problem with inkjet printers is the tendency for the ink inside the nozzles to dry out when not used even for a relatively short time, blocking any ink from exiting. If your printer is telling Windows that it’s printing and feeding paper through, but either nothing is coming out (usually the case if you’re just printing black text) or only certain colors are printing, the culprit is almost certainly dried ink clogging the nozzles.

Another problem that sometimes arises is the dreaded multipage misfeed. This is often not actually your printer’s fault—humidity can cause sheets of paper to cling to each other—but sometimes the culprit is an overheated printer, so if you’ve been cranking out a lot of documents without stopping, try giving the printer a bit of a coffee break. Also, fan the sheets of the paper stack before inserting it into the paper tray.

Finally, check to see if excess ink overflow is a problem. In the area where the printheads park, look for a small tank or tray that catches excess ink from the cleaning process. If the printer has one, check to see how full it is. If this tray overflows onto the main board or even the power supply, it will kill your printer. If you discover that the tray is about to overflow, you can remove excess ink by inserting a twisted paper towel into the tank to soak up some of the ink. It is advisable to wear latex or vinyl gloves while doing this. Clean up any spilled ink with a paper towel dampened with distilled water.

Maintaining and Troubleshooting Laser Printers
Quite a few problems can arise with laser printers, but before getting into those details, you need to review some recommended procedures for avoiding those problems.



CAUTION   Before you service a laser printer, always, always turn it off and unplug it! Don’t expose yourself to the very dangerous high voltages found inside these machines.

Laser Printer Maintenance
Unlike computer maintenance, laser printer maintenance follows a fairly well-established procedure. Of course, you’ll need to replace toner every so often, but keeping your laser printer healthy requires following these maintenance steps.

Keep It Clean  Laser printers are quite robust as a rule. A good cleaning every time you replace the toner cartridge will help that printer last for many years. I know of many examples of original HP LaserJet I printers continuing to run perfectly after a dozen or more years of operation. The secret is that they were kept immaculately clean.

Your laser printer gets dirty in two ways: Excess toner, over time, will slowly coat the entire printer. Paper dust, sometimes called paper dander, tends to build up where the paper is bent around rollers or where pickup rollers grab paper. Unlike (black) toner, paper dust is easy to see and is usually a good indicator that a printer needs to be cleaned. Usually, a thorough cleaning using a can of compressed air to blow out the printer is the best cleaning you can do. It’s best to do this outdoors, or you may end up looking like one of those chimney sweeps from Mary Poppins! If you must clean a printer indoors, use a special low-static vacuum—often called a toner vac—designed especially for electronic components, like some of the great products from Metro Vacuum (https://metrovac.com).

Every laser printer has its own unique cleaning method, but the cleaning instructions tend to skip one little area. Every laser printer has a number of rubber guide rollers through which the paper is run during the print process. These little rollers tend to pick up dirt and paper dust over time, making them slip and jam paper. They are easily cleaned with a small amount of 90 percent or better denatured alcohol on a fibrous cleaning towel. The alcohol will remove the debris and any dead rubber. If the paper won’t feed, you can give the rollers and separator pads a textured surface that will restore their feeding properties by rubbing them with a little denatured alcohol on a nonmetallic scouring pad.



CAUTION   The imaging drum, usually (but not always) contained in the toner cartridge, can be wiped clean if it becomes dirty, but be very careful if you do so! If the drum becomes scratched, the scratch will appear on every page printed from that point on. The only repair in the event of a scratch is to replace the toner cartridge or imaging drum.

If you’re ready to get specific, get the printer’s service manual. They are a key source for information on how to keep a printer clean and running. Sadly, not all printer manufacturers provide these, but most do. While you’re at it, see if the manufacturer has a Quick Reference Guide; these can be very handy for most printer problems!

Periodic Maintenance  Although keeping the printer clean is critical to its health and well-being, every laser printer has certain components that you need to replace periodically. Your ultimate source for determining the parts that need to be replaced (and when to replace them) is the printer manufacturer. Following the manufacturer’s maintenance guidelines will help to ensure years of trouble-free, dependable printing from your laser printer.

Many manufacturers provide kits that contain components that you should replace on a regular schedule. These maintenance kits include sets of replacement parts, such as a fuser, as well as one or more rollers or pads. Typically, you need to reset the page counter after installing a maintenance kit so the printer can remind you to perform maintenance again after a certain number of pages have been printed.

Some ozone filters can be cleaned with a vacuum and some can only be replaced—follow the manufacturer’s recommendation. You can clean the fuser assembly with 90 percent or better denatured alcohol. Check the heat roller (the Teflon-coated one with the light bulb inside) for pits and scratches. If you see surface damage on the rollers, replace the fuser unit.

Most printers will give you an error code when the fuser is damaged or overheating and needs to be replaced; others will produce the error code at a preset copy count as a preventive maintenance measure. Again, follow the manufacturer’s recommendations.



NOTE   Failure of the thermal fuse (used to keep the fuser from overheating) can necessitate replacing the fuser assembly. Some machines contain more than one thermal fuse. As always, follow the manufacturer’s recommendations. Many manufacturers have kits that alert you with an alarm code to replace the fuser unit and key rollers and guides at predetermined page counts.

The transfer corona can be cleaned with a 90 percent denatured alcohol solution on a cotton swab. If the wire is broken, you can replace it; many just snap in or are held in by a couple of screws. Paper guides can also be cleaned with alcohol on a fibrous towel.

As with inkjet printers, some laser printers also have calibration routines to ensure the quality of color prints. Registration routines ensure that each color prints in the correct location, and color calibration ensures that the printer lays down the right amount of each color. Some devices will perform these automatically from time to time. If not, the printer’s manual or menu panel should recommend when to run these routines and should walk you through the process.



CAUTION   The fuser assembly operates at 200 to 300 degrees Fahrenheit, so always allow time for this component to cool down before you attempt to clean it.

Laser Printer Problems
Laser printer problems usually result in poor output. One of the most important tests you can do on any printer, not just a laser printer, is called a diagnostic print page or an engine test page. You do this by either holding down the On Line button as the printer is started or using the printer’s maintenance software. If the print quality is poor, check for a calibration routine on your device, and see if this resolves the issue.

Faded Prints or Blank Pages  If a laser printer is spitting out faded prints or even printing blank pages, that usually means the printer is running out of toner. If the printer does have toner and nothing prints, print a diagnostic/test page. If that is also blank, remove the toner cartridge and look at the imaging drum inside. If the image is still there, you know the transfer corona or the high-voltage power supply has failed. Check the printer’s maintenance guide to see how to focus on the bad part and replace it.

Dirty or Smudged Printouts  If the fusing mechanism in a laser printer gets dirty, it will leave a light dusting of toner all over the paper, particularly on the back of the page. When you see toner speckling on printed pages, you should get the printer cleaned.

If the printout looks smudged or readily rubs off on your fingers, the fuser isn’t properly fusing the toner to the paper (CompTIA calls it toner not fusing to paper). Depending on the paper used, the fuser needs to reach a certain temperature to fuse the toner. If the toner won’t fuse to the paper, try using a lighter-weight paper. You might also need to replace the fuser.

Double/Echo Images  Echo images sometimes appear at regular intervals on the printed page. This happens when the imaging drum has not fully discharged and is picking up toner from a previous image or when a previous image has used up so much toner that either the supply of charged toner is insufficient or the toner has not been adequately charged. Sometimes it can also be caused by a worn-out cleaning blade that isn’t removing the toner from the drum.

Light Echo Images Versus Dark Echo Images  A variety of problems can cause both light and dark echo images, but the most common source of light echo images is “developer starvation.” If you ask a laser printer to print an extremely dark or complex image, it can use up so much toner that the toner cartridge will not be able to charge enough toner to print the next image. The proper solution is to use less toner. You can fix echo image problems in the following ways:

•   Lower the resolution of the page (print at 300 dpi instead of 600 dpi).

•   Use a different pattern.

•   Avoid 50 percent grayscale and “dot-on/dot-off patterns.”

•   Change the layout so that grayscale patterns do not follow black areas.

•   Make dark patterns lighter and light patterns darker.

•   Print in landscape orientation.

•   Adjust print density and RET settings.

•   Print a completely blank page immediately prior to the page with the echo image, as part of the same print job.

In addition to these possibilities, low temperature and low humidity can aggravate echo image problems. Check your user’s manual for environmental recommendations. Dark echo images can sometimes be caused by a damaged drum. It may be fixed by replacing the toner cartridge. Light echo images would not be solved in this way. Switching other components will not usually affect echo image problems because they are a side effect of the entire printing process.

Lines Down the Printed Page  Lines down the printed page usually occur when the toner is clogged, preventing the proper dispersion of toner on the drum. Try shaking the toner cartridge to dislodge the clog. If that doesn’t work, replace the toner cartridge.

Blotchy Print  Blotches are commonly a result of uneven dispersion of toner, especially if the toner is low. Shake the toner from side to side and then try to print. Also be sure that the printer is sitting level. Finally, make sure the paper is not wet in spots. If the blotches are in a regular order, check the fusing rollers and the imaging drum for any foreign objects.

Spotty Print  If spots appear at regular intervals, the drum may be damaged or some toner may be stuck to the fuser rollers. Try wiping off the fuser rollers. Check the imaging drum for damage. If the drum is damaged, get a new toner cartridge.

Embossed Effect  If your prints are getting an embossed effect (like putting a penny under a piece of paper and rubbing it with a lead pencil), there is almost certainly a foreign object on a roller. Use 90 percent denatured alcohol or regular water with a soft cloth to try to remove it. If the foreign object is on the imaging drum, you’re going to have to use a new toner cartridge. An embossed effect can also be caused by the contrast control being set too high. The contrast control is actually a knob on the inside of the unit (sometimes accessible from the outside, on older models). Check your manual for the specific location.

Incomplete Characters  You can sometimes correct incompletely printed characters on laser-printed transparencies by adjusting the print density. Be extremely careful to use only materials approved for use in laser printers.

Creased Paper  Laser printers have up to four rollers. In addition to the heat and pressure rollers of the fuser assembly, other rollers move the paper from the source tray to the output tray. These rollers crease the paper to avoid curling that would cause paper jams in the printer. If the creases are noticeable, try using a different paper type. Cotton bond paper is usually more susceptible to noticeable creasing than other bonds. You might also try sending the output to the faceup tray, which avoids one roller. There is no hardware solution to this problem; it is simply a side effect of the process.

Paper Jams  Every printer jams now and then. To clear jams, always refer first to the manufacturer’s jam removal procedure. It is simply too easy to damage a printer by pulling on the jammed paper! If the printer reports a jam but there’s no paper inside, you almost certainly have a problem with one of the many jam sensors or paper feed sensors inside the printer, and you’ll need to take it to a repair center.

Multipage Misfeed  If the printer grabs multiple sheets at a time, this is called a multipage misfeed. To fix this issue first try opening a new ream of paper and loading that in the printer. If that works, you have a humidity problem. If the new paper angle doesn’t work, check the separation pad on the printer. The separation pad is a small piece of cork or rubber that separates the sheets as they are pulled from the paper feed tray. A worn separation pad looks shiny and, well, worn! Most separation pads are easy to replace.

Paper Not Feeding  If your printer has paper in the tray but you try to print and notice paper not feeding, you might need to clean (or even replace) your printer’s pick-up rollers. First, rule out some simple alternatives. Make sure the printer is configured to use the same tray you’re expecting it to use. Check the paper: make sure the tray isn’t overfilled and confirm the paper there is well aligned, positioned correctly in the tray, and not ripped or bent. See if the weight or coating are different than what you normally use and whether the print settings specify the correct kind of paper. If the paper is different than what you normally use, test whether it’ll pick up the normal paper just fine. If the tray has adjustable guides, make sure they aren’t holding the paper too tightly.

Warped, Overprinted, or Poorly Formed Characters  Poorly formed characters can indicate either a problem with the paper (or other media) or a problem with the hardware.

Incorrect media cause a number of these types of problems. Avoid paper that is too rough or too smooth. Paper that is too rough interferes with the fusing of characters and their initial definition. If the paper is too smooth (like some coated papers, for example), it may feed improperly, causing distorted or overwritten characters. Even though you can purchase laser printer–specific paper, all laser printers print acceptably on standard photocopy paper. Try to keep the paper from becoming too wet. Don’t open a ream of paper until it is time to load it into the printer. Always fan the paper before loading it into the printer, especially if the paper has been left out of the package for more than just a few days.

The durability of a well-maintained laser printer makes hardware a much rarer source of character printing problems, but you should be aware of the possibility. Fortunately, it is fairly easy to check the hardware. Most laser printers have a self-test function—often combined with a diagnostic printout, but sometimes as a separate process. This self-test shows whether the laser printer can properly develop an image without actually having to send print commands from the computer. The self-test is quite handy to verify the question “Is it the printer or is it the computer?” Run the self-test to check for connectivity and configuration problems.

Possible solutions include replacing the toner cartridge, especially if you hear popping noises; checking the cabling; and replacing the data cable, especially if it has bends or crimps or if objects are resting on the cable. If you have a front menu panel, turn off advanced functions and high-speed settings to determine whether the advanced functions are either not working properly or not supported by your current software configuration (check your manuals for configuration information). If these solutions do not work, the problem may not be user serviceable. Contact an authorized service center.

Troubleshooting 3-D Printers
Creating objects by melting and reforming plastic has a lot of potential for a big mess. Common issues include unwanted strings connecting open spaces (called stringing or oozing), overheating to melt part of the final product, and layers shifting so that they don’t align properly. All filaments differ in quality, just to make an already complex process more problematic. Using poor-quality filament might save money up front but lead to clogged extruders in short order.



NOTE   CompTIA doesn’t specify any maintenance steps for 3-D printers.

Although 3-D printers have been around for a decade or so, the technology still has growing pains. Troubleshooting 3-D printers is way outside the scope of the CompTIA A+ exams, primarily because the processes and such vary tremendously among the many models of printers. For the most part, check the manufacturer’s Web site for help. Try one of the many excellent enthusiast sites out there for help guides, such as https://www.fabbaloo.com. Good luck!

Chapter Review
Questions
1.   What mechanism is used by most inkjet printers to push ink onto the paper?

A.   Electrostatic discharge

B.   Gravity

C.   Air pressure

D.   Electroconductive plates

2.   With a laser printer, what creates the image on the imaging drum?

A.   Primary corona

B.   Laser imaging unit

C.   Transfer corona

D.   Toner

3.   What is the proper order of the laser printing process?

A.   Process, clean, charge, expose, develop, transfer, and fuse

B.   Process, charge, expose, develop, transfer, fuse, and clean

C.   Clean, expose, develop, transfer, process, fuse, and charge

D.   Clean, charge, expose, process, develop, fuse, and transfer

4.   On a dot-matrix printer, what physically strikes the ribbon to form an image?

A.   Electromagnets

B.   Printwires

C.   Character wheel

D.   Print hammers

5.   Which of these items are considered to be dot-matrix printer consumables? (Select all that apply.)

A.   Drive motor

B.   Paper

C.   Flywheel

D.   Ribbon

6.   What part of a laser printer must be vacuumed or replaced periodically to prevent damage caused by the action of the corona?

A.   The rubber rollers

B.   The ozone filter

C.   The transfer filter

D.   The cleaning blade

7.   Which one of the following port types do most printers support?

A.   PS/2

B.   USB

C.   Infrared

D.   RS-232

8.   A standalone printer prints a test page just fine, but it makes gobbledygook out of your term paper. What’s probably wrong?

A.   Out of toner

B.   Fuser error

C.   Printer interface

D.   Faulty software configuration

9.   Which printing process ends with the physical and electrical cleaning of the imaging drum?

A.   Thermal

B.   Inkjet

C.   Impact

D.   Laser

10.   Which tool would help you determine why a print job didn’t print?

A.   Printer driver

B.   Printer setup

C.   Print spooler

D.   System setup

Answers
1.   D. Most inkjet printers use electroconductive plates to push the ink onto the paper.

2.   B. The laser imaging unit creates an image on the imaging drum.

3.   B. Process, charge, expose, develop, transfer, fuse, and clean is the proper process.

4.   B. Printwires physically strike the ribbon in dot-matrix printers.

5.   B, D. Both paper and ribbons are considered dot-matrix printer consumables.

6.   B. The ozone filter of a laser printer should be periodically vacuumed or changed.

7.   B. You’ll find almost all non-networked printers hooked up to USB ports.

8.   D. The application (software) that is trying to print is probably configured incorrectly.

9.   D. The laser printing process ends with the physical and electrical cleaning of the imaging drum.

10.   C. The print spooler can help you determine why a print job didn’t print.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 26 Printers and Multifunction Devices
Chapter 27 Securing Computers
Chapter 28 Operational Procedures
42h 21m remaining
CHAPTER 27
Securing Computers
In this chapter, you will learn how to

•   Explain the threats to your computers and data

•   Describe key security concepts and technologies

•   Explain how to protect computers from network threats

Your PC is under siege. Through your PC, malicious people can gain valuable information about you and your habits. They can steal your files. They can run programs that log your keystrokes and thus gain account names and passwords, credit card information, and more. They can run software that takes over much of your computer processing time and use it to send spam or steal from others. The threat is real and immediate. Worse, they’re doing these things to your clients as I write these words. You need to secure your computer and your users’ computers from these attacks.

But what does computer security mean? Is it an anti-malware program? Is it big, complex passwords? Sure, it’s both of these things, but what about the fact that your laptop can be stolen easily or that improper ventilation can cause hard drives and other components to die?

To secure computers, you need both a sound strategy and proper tactics. For strategic reasons, you need to understand the threat from unauthorized access to local machines as well as the big threats posed to networked computers. Part of the big picture is knowing what policies, software, and hardware to put in place to stop those threats. From a tactical in-the-trenches perspective, you need to master the details to know how to implement and maintain the proper tools. Not only do you need to install anti-malware programs in your users’ computers, for example, but you also need to update those programs regularly to keep up with the constant barrage of new malware.

1102
Analyzing Threats and Vulnerabilities
Threats to your data and PC come from two directions: accidents and malicious people. All sorts of things can go wrong with your computer, from users getting access to folders they shouldn’t see to a virus striking and deleting folders. Files can be deleted, renamed, or simply lost (what Nancy Drew might call “The Case of the Disappearing Files”). Hard drives can die, and optical discs get scratched and rendered unreadable. Accidents happen, and even well-meaning people can make mistakes.

Threats need some way to access a network or facility, whether they are accidental or malicious, internal or external, and that’s where vulnerabilities come in. A vulnerability is a weak spot in your defenses that enables a threat to cause harm. Vulnerabilities can exist in an organization’s physical security or in its networks. Understanding different types of vulnerabilities and the threats that will try to exploit them is vital to protecting your organization’s data, reputation, and safety. We’ll look at threats first, followed by vulnerabilities that threats exploit to do their harm.

Threats
Unfortunately, a lot of people out there intend to do you harm. Combine that intent with a talent for computers, and you have a dangerous combination. Let’s look at the following issues:

•   Malicious actors

•   Unauthorized access

•   Social engineering

•   Insider threats

•   Data destruction, whether accidental or deliberate

•   Administrative access

•   System crash/hardware failure

•   Physical theft

•   Malware

•   Spam

Malicious Actors
In some cases, the threat in question is an individual, also known as a threat actor. Whether they’re an external malicious actor like a hacker or an internal malicious actor like a disgruntled employee, threat actors need some way to use vulnerabilities to their advantage. This is known as an attack, or an exploit. The general order of operations goes something like this: a threat actor identifies one or more vulnerabilities in a network or physical security system, uses some combination of attacks to exploit the vulnerability or vulnerabilities, and proceeds to carry out their nefarious plans. You’ll notice that I didn’t say that a threat actor will use only one attack or exploit only one vulnerability. There’s good reason for this. Very rarely will a malicious actor make use of only one method. For example, a malicious actor attacking from outside the organization may employ a phishing scam to gain user login credentials, use those credentials to gain initial access to a network, then deploy a zero-day attack to take over the network administrator’s account.

If some of these terms sound unfamiliar now, don’t worry. You’re about to get a crash course in some of the many threats and attacks you’ll encounter in the world of IT.



EXAM TIP   Be aware that while many of these terms are considered types of attacks, CompTIA’s A+ 1102 exam objectives classify them all as social engineering or threats. For the purpose of the 1102 exam, threats and attacks are one and the same, but in most other contexts, threats and attacks are separate concepts.

Zero-Day Attack  A zero-day attack is an attack on a vulnerability that wasn’t already known to the software developers. It gets the name because the developer of the flawed software has had zero days to fix the vulnerability. Microsoft, Apple, and other software developers regularly post patches to fix flaws as they’re discovered.

Spoofing  Spoofing is the process of pretending to be someone or something you are not by placing false information into your packets. Any data sent on a network can be spoofed. Here are a few quick examples of commonly spoofed data:

•   Source MAC address and IP address, to make you think a packet came from somewhere else

•   E-mail address, to make you think an e-mail came from somewhere else

•   Web address, to make you think you are on a Web page you are not on

•   Username, to make you think a certain user is contacting you when in reality it’s someone completely different

Generally, spoofing isn’t so much a threat as it is a tool to make threats. If you spoof my e-mail address, for example, that by itself isn’t a threat. If you use my e-mail address to pretend to be me, however, and to ask my employees to send in their usernames and passwords for network login? That’s clearly a threat. (And also a waste of time; my employees would never trust me with their usernames and passwords.)

On-Path Attack  In an on-path attack, an attacker taps into communications between two systems, covertly intercepting traffic thought to be only between those systems, reading or in some cases even changing the data and then sending the data on. A classic on-path attack would be a person using special software on a wireless network to make all the clients think his laptop is a wireless access point. He could then listen in on that wireless network, gathering up all the conversations and gaining access to passwords, shared keys, or other sensitive information.



EXAM TIP   While CompTIA prefers and uses the term on-path attack, you’ll more commonly hear it referred to by its original name, man-in-the-middle, out in the world. Just be aware that the two terms are interchangeable, and that on-path attack is how it will be referred to on the exam.

Session Hijacking  Somewhat similarly to on-path attacks, session hijacking tries to intercept a valid computer session to get authentication information. Unlike on-path attacks, session hijacking only tries to grab authentication information, not necessarily listening in like an on-path attack.

Brute-Force Attack  CompTIA describes brute force as a threat, but it’s more of a method that threat agents use. Brute force is a method where a threat agent guesses many or all possible values for some data. Most of the time the term brute force refers to an attempt to crack a password, but the concept also applies to other attacks. You can brute force a search for open ports, network IDs, usernames, and so on. Pretty much any attempt to guess the contents of some kind of data field that isn’t obvious (or is hidden) is considered a brute-force attack.

There are two other tools attackers use to brute force passwords: dictionaries and rainbow tables. A dictionary attack is a form of brute-force attack that essentially guesses every word in a dictionary. Don’t just think of Webster’s dictionary—a dictionary used to attack passwords might contain every password ever leaked online.

Before we can talk about rainbow tables, we need to look closer at password leaks. One (terrible!) way to authenticate users is to save a copy of their password in a database and check it every time they log in. Hackers love to steal these databases because they can go try the username and password on popular services, and use the passwords to improve the dictionaries they use to guess passwords.

In response to this threat, authentication systems only save a special value (called a hash) computed from the password; each time the user logs in, the system re-computes this special value and compares it with the saved copy. If an attacker steals one of these databases, they only get a bunch of usernames and hashes. Hashes are special because the computation that creates them is irreversible; the only way to figure out what password produced a given hash is to guess a password, perform the same computation, and see if the hashes match.

Attackers fought back by pre-computing large lookup tables—known as hash tables—of passwords and the corresponding hash. When they find a large database of hashed passwords, they can just look up the corresponding password in their hash table. Hash tables for passwords more than a few characters long eat tons of storage space, so they’re turned into rainbow tables to save space (at the expense of a little speed and accuracy.) Rainbow tables use complicated math to condense dictionary tables with hashed entries dramatically. They’re binary files, not text files, and can store amazing amounts of information in a relatively small size. Rainbow tables generally fall into the realm of CompTIA Security+ or even higher-level certifications, but the phrase has become common enough that CompTIA A+ techs need to know what it means.

Denial of Service  A denial of service (DoS) attack uses various methods to overwhelm a system, such as a Web server, to make it essentially nonfunctional. DoS attacks were relatively common in the early days of the Web. These days you’ll see distributed denial of service (DDoS) attacks that use many machines simultaneously to assault a system. A DDoS attack is generally executed using a botnet. A botnet consists of any number (usually a large one) of systems infected with malware designed to allow them to be controlled by an attacker and used to send disruptive traffic designed to bring down a resource. You’ll get a closer look at botnets and how they work later on in the chapter when we discuss malware.

Cross-Site Scripting  Most companies have Web sites, and Web sites can sometimes be very vulnerable to attacks by the bad guys. One such attack that can pose a threat to your Web applications is known as cross-site scripting. Cross-site scripting (XSS) is an attack in which the attacker injects malicious code into the Web app in order to trick it into sending things it shouldn’t to other users of the Web site. Generally, this occurs due to errors in the application’s code, which the attacker finds and exploits. XSS can lead to account takeovers, stolen data, or even a full takeover of the Web site or app. The nitty-gritty details of XSS, specific variants of the attack, and how to prevent them are things you’ll learn more about in CompTIA Security+, but for the CompTIA A+ 1102 exam, be aware that cross-site scripting can pose a major threat to an organization’s Web site(s).

SQL Injection  You’ve most likely deduced by now that accessing, stealing, and destroying data are common goals of malicious actors, so let’s take a look at one of the favorite methods hackers use to achieve them. Before I can tell you about the dreaded SQL injection, I’m going to have to tell you what SQL is. SQL is an acronym for Structured Query Language. SQL is a language that enables a program to interact with a database using various commands and queries. If you’ve started thinking that attacking a database sounds like a dangerous threat, you’re right. An SQL injection occurs when an attacker enters SQL commands into an input field like you’d see in a Web app, in order to gain access to data in a database that they shouldn’t be able to see. You won’t need to know the ins and outs of how SQL injection is performed, but know that preventing it is done at the programming level, with something known as input validation.

Unauthorized Access
Unauthorized access occurs when a person accesses resources without permission. “Resources” in this case means data, applications, and hardware. A user can alter or delete data; access sensitive information, such as financial data, personnel files, or e-mail messages; or use a computer for purposes the owner did not intend.

Not all unauthorized access is malicious—often this problem arises when users who are poking around in a computer out of curiosity or boredom discover they can access resources in a fashion the primary user did not have in mind. Unauthorized access becomes malicious when people knowingly and intentionally take advantage of weaknesses in your security to gain information, use resources, or destroy data!

One way to gain unauthorized access is intrusion. You might imagine someone kicking in a door and hacking into a computer, but more often than not it’s someone sitting at a home computer, trying various passwords over the Internet. Not quite as glamorous, but it’ll do. Another insidious method is manipulating people into giving privileged information or access that would be otherwise unavailable to a would-be attacker. This takes us into a discussion of one of the most common and dangerous categories of threats.

Social Engineering
Although you’re more likely to lose data through accidents, the acts of malicious users get the headlines. Most of these attacks come under the heading of social engineering—the process of using or manipulating people inside the organization to gain access to its network or facilities—which covers the many ways humans can use other humans to gain unauthorized information. This information may be a network login, a credit card number, company customer data—almost anything you might imagine that one person or organization may not want outsiders to access.



NOTE   Social engineering attacks are often used together, so if you discover one of them being used against your organization, it’s a good idea to look for others.

Social engineering attacks aren’t hacking—at least in the classic sense of the word—but the goals are the same and the attacks will often be used by hackers in conjunction with other methods. Let’s look at a few of the more classic types of social engineering attacks.

Infiltration  Hackers can use impersonation to enter your building physically disguised as cleaning personnel, repair technicians, messengers, and so on. They then snoop around desks, looking for whatever they can find. They might talk with people inside the organization, gathering names, office numbers, department names—little things in and of themselves but powerful tools when combined later with other social engineering attacks.

Dressing the part of a legitimate user—with fake badge and everything—enables malicious people to gain access to locations and thus potentially your data. Following someone through the door, for example, as if you belong, is called tailgating. Tailgating is a common form of infiltration.

To combat tailgating, facilities often install an access control vestibule at the entrance to sensitive areas, or sometimes at the entrance to the whole building. Traditionally called a mantrap, an access control vestibule is a small room with a set of two doors, one to the outside, unsecured area and one to the inner, secure area. When walking through the access control vestibule, the outer door must be closed before the inner door can be opened. In addition to the double doors, the user must present some form of authentication. For additional security, an access control vestibule is often controlled by a security guard who keeps an entry control roster. This document keeps a record of all comings and goings from the building.

Information Gathering  You’re probably familiar with the old saying that “knowledge is power.” The good news is that when it comes to securing systems and facilities, the saying is true. The bad news is that it’s also true when someone is trying to compromise those systems and facilities. Social engineering is often used by threat actors to gather information that makes it easier for them to successfully gain access. Here are some common ways that they get ahold of information that they aren’t supposed to have.

Dumpster diving is the generic term for searching garbage for information. This is also a form of intrusion. The amount of sensitive information that makes it into any organization’s trash bin boggles the mind! Years ago, I worked with an IT security guru who gave me and a few other IT people a tour of our office’s trash. In one 20-minute tour of the personal wastebaskets of one office area, we had enough information to access the network easily, as well as to seriously embarrass more than a few people. When it comes to getting information, the trash is the place to look!

Shoulder surfing is another technique for gathering information and gaining unauthorized access. Shoulder surfing is simply observing someone’s screen or keyboard to get information, often passwords. As the name implies, it usually requires the bad guy looking over your shoulder to see what you are doing.

Vishing  Vishing is one of the most common social engineering attacks. In this case, the attacker makes a phone call to someone in the organization to scam them into revealing information gain information. The attacker attempts to come across as someone inside the organization and uses this to get the desired information. Probably the most famous of these scams is the “I forgot my username and password” scam. In this gambit, the attacker first learns the account name of a legitimate person in the organization, usually using the infiltration method. The attacker then calls someone in the organization, usually the help desk, in an attempt to gather information, in this case a password.

Hacker: “Hi, this is John Anderson in accounting. I forgot my password. Can you reset it, please?”

Help Desk: “Sure, what’s your username?”

Hacker: “j_w_anderson.”

Help Desk: “OK, I reset it to e34rd3.”

Vishing certainly isn’t limited to attempts to get network access. There are documented vishing attacks against organizations aimed at getting cash, blackmail material, or other valuables.

Phishing  Phishing is the act of trying to get people to give their usernames, passwords, or other security information by pretending to be someone else electronically. A classic example is when a bad guy sends you an e-mail that’s supposed to be from your local credit card company asking you to send them your username and password. Phishing is by far the most common form of social engineering done today.

Phishing refers to a fairly random act of badness. The attacker targets anyone silly enough to take the bait. Spear phishing is the term used for targeted attacks, like when a bad guy goes after a specific celebrity. The dangerous thing about spear phishing is that the bait can be carefully tailored using details from the target’s life. A particularly dangerous form of phishing specifically targets people who are high up in an organization, such as executives or administrators. This is known as whaling.

Evil Twin  One of the reasons infiltrations can be so dangerous is that a malicious actor may be able to plant devices inside an organization’s network. A particularly dangerous example of this is known as an evil twin. An evil twin is a fake wireless access point configured to mimic the traits of a legitimate device and network, in order to lure unsuspecting users to connect to the attacker’s device. By doing this, the attacker can snoop on Internet traffic, steal user credentials, and use this information to do additional damage.

Insider Threats
Threats to your network or facility don’t only come from the outside. Sometimes, the threat exists within the organization itself. This is known as an insider threat. An insider threat is any security risk that originates from a person inside an organization. Sometimes, the insider in question is malicious, out to steal funds or information. They may also be a disgruntled current or former employee looking to get back at the company.

Don’t make the mistake of thinking that all insider threats are malicious though—sometimes accidents happen, and the insider threat is a well-meaning person just trying to make their or someone else’s job easier. The real threat here is the access to systems and facilities that they have and what they can do with it. There are several ways to mitigate the risks of insider threats, most which center on access control. Only giving users access to what they need to do their jobs and deleting relevant user and administrator accounts when someone leaves the company are both examples of insider threat mitigation. Some methods to mitigate the risk of insider threats will be discussed in greater detail later in the chapter in the “Logical Security” section.

Data Destruction
Often an extension of unauthorized access, data destruction means more than just intentionally or accidentally erasing or corrupting data. It’s easy to imagine some evil hacker accessing your network and deleting all your important files, but authorized users may also access certain data and then use that data beyond what they are authorized to do. A good example is the person who legitimately accesses a Microsoft Access product database to modify the product descriptions, only to discover that she can change the prices of the products, too.

This type of threat is particularly dangerous when users are not clearly informed about the extent to which they are authorized to make changes. A fellow tech once told me about a user who managed to mangle an important database when someone gave him incorrect access. When confronted, the user said: “If I wasn’t allowed to change it, the system wouldn’t let me do it!” Many users believe that systems are configured in a paternalistic way that wouldn’t allow them to do anything inappropriate. As a result, users often assume they’re authorized to make any changes they believe are necessary when working on a piece of data they know they’re authorized to access.

Administrative Access
Every operating system enables you to create user accounts and grant those accounts a certain level of access to files and folders in that computer. As an administrator, supervisor, or root user, you have full control over just about every aspect of the computer. This increased control means these accounts can do vastly more damage when compromised, amplifying the danger of several other threats. The idea is to minimize both the number of accounts with full control and the time they spend logged in.

Even if a user absolutely needs this access, uses strong passwords, and practices good physical security, malware installed by a convincing spear phishing attack could leverage that control to access files, install software, and change settings a typical account couldn’t touch.

System Crash/Hardware Failure
As with any technology, computers can and will fail—usually when you can least afford for it to happen. Hard drives crash, the power fails . . . it’s all part of the joy of working in the computing business. You need to create redundancy in areas prone to failure (such as installing backup power in case of electrical failure) and perform those all-important data backups. A security-specific example would be having redundant firewalls to protect the network in the event that one of them fails. Chapter 14 goes into detail about using backups and other issues involved in creating a stable and reliable system.

Physical Theft
A fellow network geek once challenged me to try to bring down his newly installed network. He had just installed a powerful and expensive firewall router and was convinced that I couldn’t get to a test server he added to his network just for me to try to access. After a few attempts to hack in over the Internet, I saw that I wasn’t going to get anywhere that way.

So, I jumped in my car and drove to his office, having first outfitted myself in a techy-looking jumpsuit and an ancient ID badge I just happened to have in my sock drawer. I smiled sweetly at the receptionist and walked right by my friend’s office (I noticed he was smugly monitoring incoming IP traffic by using some neato packet-sniffing program) to his new server.

I quickly pulled the wires out of the back of his precious server, picked it up, and walked out the door. The receptionist was too busy trying to figure out why her e-mail wasn’t working to notice me as I whisked by her carrying the 65-pound server box. I stopped in the hall and called him from my cell phone.

Me (cheerily): “Dude, I got all your data!”

Him (not cheerily): “You rebooted my server! How did you do it?”

Me (smiling): “I didn’t reboot it—go over and look at it!”

Him (really mad now): “YOU <EXPLETIVE> THIEF! YOU STOLE MY SERVER!”

Me (cordially): “Why, yes. Yes, I did. Give me two days to hack your password in the comfort of my home, and I’ll see everything! Bye!”

I immediately walked back in and handed him the test server. It was fun. The moral here is simple: Never forget that the best network software security measures can be rendered useless if you fail to protect your systems physically!

Protecting Laptops  Physical security for your systems extends beyond the confines of the office as well. The very thing that makes laptops portable also makes them tempting targets for thieves. One of the simplest ways to protect your laptop is to use a basic cable lock. The idea is to loop the cable around a solid object, such as a bed frame, and secure the lock to the small security hole on the side of the laptop.

Malware
Networks are without a doubt the fastest and most efficient vehicles for transferring computer viruses among systems. News reports focus attention on the many malicious software attacks from the Internet, but a huge number of such attacks still come from users who bring in programs on optical discs and USB drives. The “Network Security” section of this chapter describes the various methods of virus infection and other malware and what you need to do to prevent such attacks from damaging your networked systems.

Spam
If you have an e-mail address, there’s a 100 percent chance that you’ve seen spam at some point in your life. Spam is the digital equivalent of junk mail; it’s bulk e-mail sent out to as many people as possible in the hopes that at least some of them engage with it. Sometimes spam is just an annoyance, but it can also be a threat to your network. Phishing attempts, malicious links, and attachments that contain malware are just some of the dangers that spam can present. Spam management methods and tools were covered in detail back in Chapter 19.

Vulnerabilities
Threats to your computers and facilities can be scary, but they need some way to gain access before they can cause trouble. Threats compromise a system by exploiting vulnerabilities in a computer, network, company policy, or physical security to gain access. Once a vulnerability is exploited, whether by an outside hacker, a disgruntled employee, or even inadvertently by a well-meaning person just trying to make their job easier, chaos can ensue. Data deletion, data theft, extortion, and all sorts of other nasty things can happen if vulnerabilities aren’t identified and addressed. As a CompTIA A+ technician, you likely won’t be expected to know the nitty-gritty details of how to fix all vulnerabilities, but you should understand the fundamentals of different types of vulnerability, and how they can threaten an organization. Here are a few common vulnerabilities that you may run across while working as a technician.

Have you ever been working on your computer, playing a game, or having a Zoom meeting, and suddenly your operating system nags you to install updates that require a reboot? I know I have, and as disruptive as that can be, the disruptions that could result from ignoring those messages are even worse. That’s because these warnings are telling you to patch your operating system, and oftentimes, those patches are intended to address a security risk. Unpatched systems are vulnerable to an ever-growing list of vulnerabilities that attackers know about and are actively exploiting. Leaving a system unpatched is like leaving a second-story window open while you go on vacation. Sure, you may get home and see that everything is fine, but you may also have been robbed blind. Patching systems is key and will be discussed in more detail later in this chapter when we address malware prevention.

If leaving your systems unpatched is like leaving a second-story window open when you go on vacation, an unprotected system is like leaving your front door open with a sign on the lawn inviting people to break in. An unprotected system lacks key security tools like anti-malware software and firewalls. Without these in place, there is nothing stopping a hacker from doing whatever they want in your network. They can send malware, try to connect directly to your internal network, and try to steal or destroy your sensitive information, and do all of this with a relatively low chance of being detected. An unprotected system is a serious vulnerability, whether it’s at home, in a small business, or in a major corporation. If you must have unprotected systems, make sure to isolate and monitor them!

Operating systems also have lifespans. Over time, as new and sometimes improved operating systems launch, older ones are phased out. Once an old OS is phased out completely, it stops receiving security updates as new vulnerabilities are discovered. These operating systems are known as end-of-life (EOL) operating systems and can present a major vulnerability to a network if even one device is still using an EOL OS. It’s a fairly common problem, because operating system upgrades can be expensive and disruptive to a business’s operations. Regardless, making sure that operating systems are well supported and still receiving regular security updates is an important way to mitigate vulnerabilities.

While the concept of bring your own device (BYOD) was discussed in the context of securing mobile devices back in Chapter 25, the potential security risks extend past mobile devices to personal laptops as well. While BYOD may be popular with employees and more friendly to an organization’s budget, BYOD can also be a security vulnerability. An external threat can use the fact that personal devices may not all be maintained with standard security features to gain access from the outside. Additionally, insider threats, whether malicious or accidental, can use personal devices to introduce malware, or remove privileged data from the security of the company’s internal network.

In the best of all possible worlds, your organization will use a mix of policies, systems, and elbow grease to ensure the devices in your networks never have vulnerabilities like these. But in reality, a system may need to defer updates for weeks while it’s busy rendering special effects. Users may need time to comply or need network access to do it. The accounting department might require software that only works on an EOL OS. A computer that serves as the interface to an old ICS system may not even have a software firewall (we’ll look at these later in the chapter). Unless you check compliance continually, new violations will appear between checks. In short, compliance is an aspiration, and you’ll often have to manage the vulnerabilities and risks that non-compliant systems represent (often by isolating them and monitoring them well).

Security Concepts and Technologies
Once you’ve assessed the threats to your computers and networks, you need to take steps to protect those valuable resources. Depending on the complexity of your organization, this can be a small job encompassing some basic security concepts and procedures, or it can be exceedingly complex. The security needs for a three-person desktop publishing firm, for example, would differ wildly from those of a defense contractor supplying top-secret toys to the Pentagon.

From a CompTIA A+ certified technician’s perspective, you need to understand the big picture (that’s the strategic side), knowing the concepts and available technologies for security. At the implementation level (that’s the tactical side), you’re expected to know where to find such things as security policies in Windows. A CompTIA Network+ or CompTIA Security+ tech will give you the specific options to implement. (The exception to this level of knowledge comes in dealing with malicious software such as viruses, but we’ll tackle that subject in the second half of the chapter.)

Controlling access is the key. If you can control access to the data, programs, and other computing resources, you’ve secured your systems. Access control is composed of interlinked areas of physical and logical security that a good security-minded tech should think about: physical security, authentication, users and groups, and security policies. Much of this you know from previous chapters, but this section should help tie it all together as a security topic. The first step is understanding physical security, which includes methods of preventing physical access to facilities, systems, and information, and the second is understanding logical security to learn how to protect your network, authenticate users, and employ effective security policies.

Physical Security
For most people, when they hear the word security, the first thing they think of are things like guards, fences, security cameras, and the like. That’s because they’re thinking about physical security. Physical security is often the first line of defense for an organization. It includes the fences and gates that keep people off the property, the locks that keep people from entering a building or area they aren’t supposed to, and the guards who use surveillance tools and alerts to keep an eye on things. Physical security is all about defending facilities and systems from—you guessed it—physical threats, both internal and external. There are layers to physical security that can and often do overlap with logical security tools to provide effective security coverage. Let’s start our investigation by looking at some specific goals and methods of physical security.

Securing Facilities
The first order of security is limiting access to your physical hardware. The security market is huge, but the options basically boil down to fences, doors, locks, alarms, and keeping a close eye on things. The first step is understanding that all of these pieces can (and will) fail or be beaten; great security involves arranging and layering many pieces so that they can enhance each other’s strengths and compensate for each other’s weaknesses.

Think back to the access control vestibule introduced earlier in the chapter. A low-tech solution like a traditional door lock is just a speed-bump to someone with a lock-pick and a moment alone with the lock. Access control vestibules are great because they combine simple measures like doors, door locks, security guards, and an entry control roster in a way that is much harder to beat than one or two locked doors. Some facilities may enhance their entrance security further by adding a magnetometer, better known as a metal detector. As pointed out earlier in the chapter when we talked about different types of threats, some threats originate from inside the organization as well as outside. A metal detector is a good way to help prevent people from bringing in dangerous items that they could use to cause harm, and to prevent them from walking out with something that doesn’t belong to them.

Sometimes access control needs to be extended past the door itself, out to the property. Many facilities have more than one entrance, or multiple buildings. As a result, organizations may add an additional line of defense to keep unauthorized people off company property altogether. Fences are often used to stop people from snooping around where they aren’t supposed to. Bollards, those short concrete or metal posts that you’ll sometimes see in areas with heavy foot traffic, can be used to prevent vehicles from getting too close for comfort (see Figure 27-1).



Figure 27-1  Example of a bollard

Security guards are great, but they can’t be everywhere at once. They need some way to keep an eye on things. That’s where the following tools come into play:

•   Video surveillance can be used by security personnel to monitor the facility from a centralized location.

•   Good lighting makes it harder for a would-be bad guy to avoid detection, with the added benefit of decreasing the likelihood of workplace accidents for staff.

•   Motion sensors can be used to let them know if someone or something is detected so they can take a closer look.

•   Alarm systems can serve a variety of functions, from warning the IT department of an attempted network breach, to informing staff of a security issue, to alerting security staff or law enforcement if a break-in happens after hours.

Any combination of these tools makes a great addition to a robust security plan, but it’s also important to make sure that people inside the organization don’t have access to things they aren’t supposed to. This brings us to the next set of access control options.

Traditional door locks aren’t terrible, but keys are easy to copy and the cost of frequently re-keying locks adds up fast. An organization ready to move beyond the basics can step up to a keyless lock system driven by employee ID badges—especially ones with authentication tools such as radio frequency identification (RFID) or smart cards (see “Authentication,” later in this chapter)—to control building and room access. Figure 27-2 shows a typical badge.



Figure 27-2  Typical employee badge/smart card

Lock Down Systems
Once an attacker has physical access to the building, protecting your hardware gets a lot harder. There are some options here, but don’t plan on them doing much more than slow someone down by a few minutes and make it obvious to anyone watching that they’re up to no good:

•   Lock the doors to your workspaces. A fast, reliable keyless lock system can make it painless to lock them even when the user steps out for a moment.

•   Equipment locks can keep someone from quickly walking off with the hardware.

•   USB locks make it harder to plug in a USB drive to load malware for stealing data.

•   RJ45 locks limit an intruder’s ability to gain access to the wired network.

•   Server locks limit access to a server’s ports and drives. There are also locking rack doors to limit access to the front or back of an entire server rack.

These devices are meaningless if an intruder can walk in like they belong, sit down at an unattended, logged-in computer, and get to work. Don’t leave a logged-in PC unattended, even if it’s just a Standard or Guest user. May the gods help you if you walk away from a server still logged in as an administrator. You’re tempting fate.

If you must step away for a moment, manually lock the computer (or screen) with a hotkey or the primary OS menu. On a Windows system, just press WINDOWS-L on the keyboard to lock it. It’s also a good idea to set up a screensaver with a short wait time and configure it to show the logon screen on resume.



EXAM TIP   If you’re in charge of multiple-user security best practices, using screensaver locks—configured to show the logon screen on resume—can help a lot with users who might forget to lock their systems when taking a break or going to lunch. Both Windows and macOS enable you to take this a step further and set automatic timeout and a screen lock, where the screen goes blank after a few minutes and a password is required for logon.

Protect Sensitive Information
Locking unattended systems is a great habit, but it won’t help much if the intruder manages to watch the user enter their password or is able to read it off a sticky note on the monitor. Don’t write down passwords and leave them in plain sight. Teach users to follow the strong password guidelines set forth in Chapter 13. Be aware of the risk of shoulder surfing. Ideally, the office layout should make it impossible for someone to watch the user without their knowledge.

If users need to work with sensitive information anywhere someone unauthorized could see the screen, they may need a privacy filter (also called a privacy screen)—a framed sheet or film that you apply to the front of your monitor. Privacy filters reduce the viewing angle, making it impossible to see the screen unless you’re directly in front of it (see Figure 27-3). Lock up paper copies of critical, personal, or sensitive documents out of sight and shred any you don’t need immediately.



Figure 27-3  Privacy filter

Logical Security
While physical security is focused on preventing unauthorized access to facilities and equipment, logical security is primarily focused on denying access to computers and data. Logical and physical security features are generally combined for maximum effectiveness. In some cases, like with biometrics, the security tool can be used for both logical and physical security applications. Let’s dig deeper into some of the more commonly implemented logical security controls.

MAC Address Filtering
It’s far from bulletproof, but if an attacker does gain physical access to your site, you may be able to throw up another hurdle to limit their ability to access your network with any of their own devices. Both wired and wireless networks can use MAC filtering to enable you to blacklist or whitelist devices based on their MAC address.

Use a blacklist to block specific computers, adding their MAC addresses to the ranks of the undesired. You can use a whitelist to pre-specify the only MAC addresses allowed access. I say this isn’t bulletproof because a savvy attacker can spoof an address (they’ll have a much easier time sniffing a valid Wi-Fi MAC address than a wired one, though) from another device accessing the network.

Keeping devices you don’t control out of your network is a big win! If the attacker can’t gain access to your network with one of their own devices (which they have probably preloaded with tools for attacking your systems or network), they’ll have to resort to breaking into one of your devices to do the heavy lifting.

MAC addresses aren’t the only way to filter traffic to and from your network. IP addresses can also be used to help keep unwanted traffic from entering or leaving your network. Like MAC filtering, IP filtering is a tool often available with routers and firewalls. IP filtering enables an administrator to set rules about whether packets should be sent or received based on the source or destination IP address. IP filtering isn’t a surefire solution to security issues, but it can be an extra hurdle in the same way MAC filtering is.

Authentication
Security requires properly implemented authentication, which means in essence how the computer determines who can or should access it and, once accessed, what that user can do. A computer can authenticate users through software or hardware, or a combination of both.

You can categorize ways to authenticate into three broad areas: knowledge factors, ownership factors, and inherence factors. You read about multifactor authentication in detail in Chapter 25 in the context of mobile device security. It works the same way when securing a desktop computer, a laptop, a server, or a building. There’s no reason to rehash it here. The only thing to add is that many organizations use two-factor authentication. An example is a key fob that generates a numeric key. A user authenticates by entering his or her username and password (something the user knows) and enters the key (something the user has) when prompted. Another popular method of authentication is to use an authenticator application. An authenticator application adds an additional layer of security similar to many multifactor authentication methods, by generating some form of key or password to be entered in conjunction with standard login credentials.



EXAM TIP   The CompTIA A+ 1102 exam will quiz you on multifactor and two-factor authentication. This applies to all computing devices.

Software Authentication: Proper Passwords  It’s still rather shocking to me to power up a friend’s computer and go straight to his or her desktop, or with my married-with-kids friends, to click one of the parents’ user account icons and not be prompted for a password. This is just wrong! I’m always tempted to assign passwords right then and there—and not tell them the passwords, of course—so they’ll see the error of their ways when they try to log on next. I don’t do it but always try to explain gently the importance of good passwords.

You know about passwords from Chapter 13, so I won’t belabor the point here. Suffice it to say that you must require that your users have proper passwords. Don’t let them write passwords down or tape them to the underside of their mouse pads either!

It’s not just access to Windows that you need to think about. There’s always the temptation for people to do other mean things, such as change CMOS settings, open up the case, and even steal hard drives. Any of these actions renders the computer inoperable to the casual user until a tech can undo the damage or replace components. All modern CMOS setup utilities come with a number of tools to protect your computer, such as drive lock, intrusion detection, and of course system access BIOS/UEFI passwords such as the one shown in Figure 27-4. Refer to Chapter 5 to refresh yourself on what you can do at a BIOS level to protect your computer.



Figure 27-4  BIOS/UEFI access password request

Hardware Authentication  Gates, doors, and computers can make use of badge readers, smart card readers, and biometric scanners to authenticate users with more authority than mere passwords. Smart cards are credit card–sized cards with circuitry that can identify the bearer of the card. Smart cards are relatively common for tasks such as authenticating users for mass transit systems but are fairly uncommon in computers. Figure 27-5 shows a smart card and keyboard combination.



Figure 27-5  Keyboard-mounted smart card reader being used for a commercial application (photo courtesy of Cherry Corp.)

Security tokens are devices that store some unique information that the user carries on their person. They may be digital certificates, passwords, or biometric data. They may also store an RSA token. RSA tokens are random-number generators that are used with usernames and passwords to ensure extra security. Most security hard tokens come in the form of key fobs, as shown in Figure 27-6.



Figure 27-6  RSA key fob (photo courtesy of EMC Corp.)

Apps and services that use security codes usually prompt you to enter the code after you supply your username and password. Some offer to send you a code via e-mail, text message (via short message service [SMS]), or voice call. Figure 27-7 shows PayPal prompting me for a code from my authenticator app (left) and my bank offering to send me a security code (right).



Figure 27-7  Prompt for a security code (left) and offer to send a security code (right)

An authenticator application is a software security token (a soft token) that turns a mobile device into a security token. As shown in Figure 27-8, these apps can generate a security code like the one on the RSA key fob shown previously in Figure 27-6. Hardware tokens are more secure than soft tokens and send-a-code options.



Figure 27-8  Getting a security code from my authenticator app

People can guess or discover passwords, but it’s a lot harder to forge someone’s fingerprints. The Apple keyboard shown in Figure 27-9 authenticates users on a local machine by using a fingerprint scanner. Other devices that will do the trick are key fobs, retina scanners, and palmprint scanners. Devices that require some sort of physical, flesh-and-blood authentication are called biometric scanners or biometric locks. In some rare cases, an organization may decide that fingerprints just aren’t enough authentication. In these cases, you may find the much newer palmprint reader. Palmprint is a bit of a misnomer, as what the scanner is actually doing is using infrared light to map the unique structure of veins in your palm. Advantages of a palmprint reader include being much more difficult, if not impossible, to fake, and the fact that it requires a person to have blood flow, which is a built-in guarantee that the person being authenticated is alive. The main disadvantage is cost, with palmprint readers often costing significantly more than their fingerprint scanning counterparts.



Figure 27-9  Apple TouchID fingerprint reader on a MacBook Air

Clever manufacturers have developed key fobs and smart cards that use RFID to transmit authentication information so users don’t have to insert something into a computer or card reader. The Privaris plusID combines, for example, a biometric fingerprint fob with an RFID tag that makes security as easy as opening a garage door remotely!

Retina scanners loom large in media as a form of biometric security, where you place your eye up to a scanning device. While retina scanners do exist, I have been in hundreds of high-security facilities and have only seen one retina scanner in operation in almost 30 years as a tech. Figure 27-10 shows about the only image of a retina scanner in operation you’ll ever encounter.



Figure 27-10  Retina scanner in Half-Life 2

Current smartphones and tablets use full facial recognition for identification and authentication, although they also use passcodes for when the recognition fails. Figure 27-11 shows a user logging in to an Apple iPhone via facial recognition. (Note the open lock. Hard to show the process in action because it happens so fast!)



Figure 27-11  Unlocking an iPhone via facial recognition

Users and Groups
Windows uses user accounts and groups as the bedrock of access control. A user account is assigned to a group, such as Users, Power Users, or Administrators, and by association gets certain permissions on the computer. Using NTFS enables the highest level of control over data resources.

Assigning users to groups is a great first step in controlling a local machine, but this feature really shines in a networked environment. Let’s take a look.



NOTE   The file system on a hard drive matters a lot when it comes to security. On modern systems, the file system on the boot drive has support for an access control list (ACL), a rich form of user and groups permissions. But this security only extends to drives/cards formatted with modern file systems such as NTFS, APFS, HFS+, and ext3/4. If you copy a file to a drive/card formatted with exFAT or the older FAT32, such as many cameras and USB flash drives use, the OS will strip all permissions and the file will be available for anyone to read!

Access to user accounts should be restricted to the assigned individuals, and those who configure the permissions to those accounts must follow the principle of least privilege: accounts should have permission to access only the resources they need and no more. Tight control of user accounts is critical to preventing unauthorized access. Disabling unused accounts is an important part of this strategy, but good user account management goes far deeper than that.

Groups are a great way to achieve increased complexity without increasing the administrative burden on network administrators, because all operating systems combine permissions. When a user is a member of more than one group, which permissions does that user have with respect to any particular resource? In all operating systems, the permissions of the groups are combined, and the result is what you call the effective permissions the user has to access a resource. As an example, if Rita is a member of the Sales group, which has List Folder Contents permission to a folder, and she is also a member of the Managers group, which has Read and Execute permissions to the same folder, Rita will have both List Folder Contents and Read and Execute permissions to that folder.

Watch out for default user accounts and groups—they can become secret backdoors to your network! All network operating systems have a default Everyone group that can be used to sneak into shared resources easily. This Everyone group, as its name implies, literally includes anyone who connects to that resource. Windows gives full control to the Everyone group by default, for example, so make sure you know to lock this down! The other scary one is the Guest account. The Guest account is the only way to access a system without a username and password. Unless you have a compelling reason to provide guest access, you should always make sure the Guest account is disabled.

All of the default groups—Everyone, Guest, Users—define broad groups of users. Never use them unless you intend to permit all of those folks access to a resource. If you use one of the default groups, remember to configure it with the proper permissions to prevent users from doing things you don’t want them to do with a shared resource!



NOTE   You can use directory permissions to limit access to sensitive information on a shared file server, protect user-specific files from snooping by other users on a multiuser system, and protect the system’s own software from being compromised by any scripts or programs the user runs. The job doesn’t end here, though! Anyone with physical access to a drive can ignore your controls. Use full-disk data-at-rest encryption to protect data (data in storage, not in use or moving around the network).

Security Policies
We’ve already discussed policies in Chapters 13 and 19, but let’s do a quick review and then see how we put it all together to help secure a network. Although permissions control how users access shared resources, there are other functions you should control that are outside the scope of resources. For example, do you want users to be able to access a command prompt on their Windows system? Do you want users to be able to install software? Would you like to control what systems a user can log on to or at what time of day a user can log on? All network operating systems provide you with some capability to control these and literally hundreds of other security parameters, under what Windows calls policies. I like to think of policies as permissions for activities, as opposed to true permissions, which control access to resources.

A policy is usually applied to a user account, a computer, or a group. Let’s use the example of a network composed of Windows systems with a Windows Server. Every Windows client has its own local policies program, which enables policies to be placed on that system only. Figure 27-12 shows the tool you use to set local policies on an individual system, called Local Security Policy, being used to deny the Guest account the capability to log on locally.



Figure 27-12  Local Security Policy

Local policies work great for individual systems, but they can be a pain to configure if you want to apply the same settings to more than one PC on your network. If you want to apply policy settings en masse, you need to step up to features of domain-based Windows Active Directory. You can use organizational units (OUs) that organize users and devices logically into a folder-like hierarchy; then exercise deity-like (Microsoft prefers the term granular) control to apply a different group policy to the network clients in each unit.

One important thing to keep in mind about Active Directory group policies is that they supersede local policies. For example, if you have a local policy in place that allows a specific user to install third-party software, then set a group policy for the domain that prevents all users from doing so, the user won’t be able to install the software. If you run into a situation like this, you’ll find that the gpupdate and gpresult commands we discussed back in Chapter 15 are helpful. They’re a quick way to double-check which group policies are applied to which users and make changes if there’s a conflict. Now let me explain group policy a little more and show you some examples of what it can do.



EXAM TIP   Group policy changes may not immediately apply to all systems. Windows will fetch the group policy when the system boots or someone logs in. It will also refresh the policy from time to time while running, though some policy changes won’t apply without a reboot anyways. You can run gpupdate/force from the command line to update group policy for a specific computer immediately.

Want to set the default wallpaper for every PC in your domain? Group policy can do that. Want to make certain tools inaccessible to everyone but authorized users? Group policy can do that, too. Want to control access to the Internet, redirect home folders, run scripts, deploy software, or just remind folks that unauthorized access to the network will get them nowhere fast? Group policy is the answer. Figure 27-13 shows group policy; I’m about to change the default title on every instance of Internet Explorer on every computer in my domain!



Figure 27-13  Using group policy to make IE title say “Provided by Mike!”

That’s just one simple example of the settings you can configure by using group policy. You can apply literally hundreds of tweaks through group policy, from the great to the small, but don’t worry too much about familiarizing yourself with each and every one. Group policy settings are a big topic on most of the Microsoft certification tracks, but for the purposes of the CompTIA A+ exams, you simply have to be comfortable with the concept behind group policy.

Although I could never list every possible policy you can enable on a Windows system, here’s a list of some commonly used ones:

•   Prevent Registry Edits If you try to edit the Registry, you get a failure message.

•   Prevent Access to the Command Prompt Keeps users from getting to the command prompt by turning off the Run command and the Command Prompt shortcut.

•   Log On Locally Defines who may log on to the system locally.

•   Shut Down System Defines who may shut down the system.

•   Minimum Password Length Forces a minimum password length.

•   Account Lockout Threshold Sets the maximum number of logon attempts a person can make before being locked out of the account.

•   Disable Windows Installer Prevents users from installing software.

•   Printer Browsing Enables users to browse for printers on the network, as opposed to using only assigned printers.

Although the CompTIA A+ exams don’t expect you to know how to implement policies on any type of network, you are expected to understand that policies exist, especially on Windows networks, and that they can do amazing things to control what users can do on their systems. If you ever try to get to a command prompt on a Windows system only to discover the Run command is dimmed, blame it on a policy, not the computer!



EXAM TIP   Account management security policy best practices dictate that you should implement restrictive user permissions, login time restrictions, account lockout based on failed attempts, disable guest accounts, and disable the operating system’s built-in AutoRun or AutoPlay features. Finally, you should always change default system usernames and passwords where possible.

Network Security
Networks are under threat from the outside as well, so this section looks at issues involving Internet-borne attacks, firewalls, and wireless networking. This content is the security bread and butter for a CompTIA A+ technician, so you need to understand the concepts and procedures and be able to implement them properly.

Malicious Software
The beauty of the Internet is the ease of accessing resources just about anywhere on the globe, all from the comfort of your favorite chair. This connection, however, runs both ways, and people from all over the world can potentially access your computer from the comfort of their evil lairs. The Internet is awash with malicious software that is, even at this moment, trying to infect your systems.

The term malware defines any program or code that’s designed to do something on a system or network that you don’t want done. Malware comes in quite a variety of guises, such as viruses, worms, ransomware, spyware, Trojan horses, keyloggers, cryptojacking, and rootkits. Let’s examine all these forms of malware, look at what they do to infected systems, and then examine how these nasties get onto your machines in the first place.

Forms of Malware
Malware has been pestering PC users since the 1980s and has evolved into many forms over the years. From the classic boot sector viruses of the ’90s to the more recent threats of ransomware and attacks on critical infrastructure, malware is an ever-changing threat to your users and data. To better understand these threats, you need to understand the different forms that malware can take.

Virus  A virus is a program that has two jobs: to replicate and to activate. Replication means it makes copies of itself, by injecting itself as extra code added to the end of executable programs, or by hiding out in a drive’s boot sector. Boot sector viruses can be particularly nasty because they live inside your system’s boot partition and activate their malicious code before the security software is able to start up and prevent it. Activation is when a virus does something like corrupting data or stealing private information. A virus only replicates to other drives, such as thumb drives or optical media. It does not self-replicate across networks. A virus needs human action to spread.

Worm  A worm functions similarly to a virus, except it does not need to attach itself to other programs to replicate. It can replicate on its own through networks, or even hardware like Thunderbolt accessories. If the infected computer is on a network, a worm will start scanning the network for other vulnerable systems to infect.

Trojan  A Trojan (named for the Trojan Horse) is a piece of malware that appears or pretends to do one thing while, at the same time, it does something evil. A Trojan horse may be a game, like poker, or ironically, a fake security program. The sky is the limit. Once installed, a Trojan horse can have a hold on the system as tenacious as any virus or worm; a key difference is that installed Trojan horses do not replicate.

Keylogger  Keylogger malware does pretty much what you might imagine, recording the user’s keystrokes and making that information available to the programmer. You’ll find keylogging functions as part of other malware as well. Keyloggers are not solely evil; a lot of parental control tools use keyloggers.

Rootkit  For malware to succeed, it often needs to come up with some method to hide itself. As awareness of malware has grown, anti-malware programs make it harder to find new locations on a computer to hide malware. A rootkit is a program that takes advantage of very low-level operating system functions to hide itself from all but the most aggressive of anti-malware tools. Worse, a rootkit, by definition, gains privileged access to the computer. Rootkits can strike operating systems, hypervisors, and even firmware (including hard drives and accessories . . . yikes!).

The most infamous rootkit appeared a while back as an antipiracy attempt by Sony on its music CDs. Unfortunately for the media giant, the rootkit software installed when you played a music CD and opened a backdoor that could be used maliciously.

Cryptominers  Malicious actors are often motivated by financial gain, so sometimes, they try to kill two birds with one stone by installing malware that can mine cryptocurrency. These cryptominers take control of a computer’s hardware resources and use them to mine cryptocurrency, which is then deposited into a crypto wallet belonging to the attacker. A telltale sign a system is infected with this kind of malware may be inexplicably high GPU or CPU utilization. There are other problems that can lead to excessive hardware utilization, but if you see it, it might be a good idea to check for cryptominer malware.

Behavior
Knowing what form the malware takes is all well and good, but what really matters is how “mal” the malware will be when it’s running rampant on a system. To get things started, let’s dive into an old favorite: spyware.

Spyware  Spyware—malicious software, generally installed without your knowledge—can use your computer’s resources to run distributed computing applications, capture keystrokes to steal passwords, or worse. Classic spyware often sneaks onto systems by being bundled with legitimate software—software that functions correctly and provides some form of benefit to the user. What kind of benefit? Way back in 2005, Movieland (otherwise known as Movieland.com and Popcorn.net) released a “handy” movie download service. They didn’t tell users, of course, that everyone who installed the software was “automatically enrolled” in a three-day trial. If you didn’t cancel the “trial,” a pop-up window filled your screen demanding you pay them for the service that you never signed up for. The worst part, however, was that you couldn’t uninstall the application completely. The uninstaller redirected users to a Web page demanding money again. (Movieland was shut down in 2007.)

For another classic example, look at Figure 27-14: the dialog box asks the user if she trusts the Gator Corporation (a well-known spyware producer from ages ago). Because everyone eventually knew not to trust Gator, they would click No, and the company faded away.



Figure 27-14  Classic Gator Corporation’s acknowledgment warning

If Movieland was a problem back in 2005, what are the big spyware applications today? Unfortunately, I can’t tell you—not because it’s a secret, but because we don’t know about them yet. You’ll probably only run into spyware these days on the CompTIA A+ 1102 exam.

Ransomware  As bad as spyware can be, at least you still have access to your data. Ransomware, on the other hand, encrypts all the data it can gain access to on a system. To top it off, many versions of ransomware can even encrypt data on mapped network drives!



EXAM TIP   Know the various types of malware, including viruses, worms, Trojan horses, keyloggers, rootkits, cryptominers, spyware, and ransomware.

Once it has locked up all your data, the ransomware application pops up a message asking for money (often bitcoins) to decrypt your data (see Figure 27-15). Also, to encourage a faster payment, this ransom is presented with a timer that, when it reaches 0, triggers deletion of the encryption keys, leaving you with a drive full of scrambled data. In some particularly dastardly cases, the ransomware doesn’t actually have the ability to decrypt built in, and will just leave your drives encrypted or wipe the data altogether when that clock hits 0.



Figure 27-15  Clean computer (top) and same computer (bottom) encrypted by Black Basta group malware (Courtesy of National Cyber Labs)

A Bot on the Net Full of Zombies  Another type of malware I want to talk about is the botnet (“bot” as in robot, get it!). As we touched on when we discussed Denial of Service attacks, a botnet, as “net” in its name implies, isn’t a single type of malware, but rather, a network of infected computers (zombies) under the control of a single person or group. Botnets can be massive, easily growing into the millions of zombies for the largest networks.

With that many machines under their control, botnet operators have command of massive computing and network resources. Some of the most common uses of botnets are sending spam or launching distributed denial of service attacks. If you’ve ever wondered how spammers and hackers pay for all that bandwidth, they don’t! They use the bandwidth of millions of zombie machines spread all around the world, from grandma’s e-mail machine to hacked Web servers.

Spam is but one use of a botnet. The criminals who run these networks also use all that collective power to launch a DDoS attack against companies and governments and demand a ransom to call off the attack.

Malware Signs and Symptoms
If your PC has been infected by malware, you’ll bump into some strange things before you can even run an anti-malware scan. Like a medical condition, malware causes unusual symptoms that should stand out from your everyday computer use. You need to become a PC physician and understand what each of these symptoms means.

Malware’s biggest strength is its flexibility: it can look like anything. In fact, a lot of malware attacks can feel like normal PC “wonkiness”—momentary slowdowns, random one-time crashes, and so on. Knowing when a weird application crash is actually a malware attack is half the battle.

Slow performance in a PC can mean you’re running too many applications at once, or that you’ve been hit with malware. Applications can crash at random, even if you don’t have too many loaded. How do you tell the difference? In this case, it’s the frequency. If it’s happening a lot, even when all of your applications are closed, you’ve got a problem. This goes for frequent lockups, too—whether it seems to be PC- or OS-based lockups. If Windows starts misbehaving (more than usual), run your anti-malware application right away.

Malware, however, doesn’t always jump out at you with big system crashes. Some malware tries to rename system files, change file permissions, or hide files completely. You might start getting e-mail messages from colleagues or friends questioning a message “you” sent to them that seemed spammy. You might get automated replies from unknown sent e-mail that you know you didn’t send. An increase in desktop alerts that don’t seem to have a legitimate cause, or unwanted notifications within the OS may also be signs that it’s time to check for malware. You may even get false alerts regarding your computer’s antivirus protection. Most of these issues are easily caught by a regular anti-malware scan, so as long as you remain vigilant, you’ll be okay.



NOTE   While it’s not necessarily a malware attack, watch out for hijacked e-mail accounts belonging either to you or to someone you know. Hackers can hit both e-mail clients and Webmail users. If you start receiving some fishy (or phishy) e-mail messages, change your Webmail username and password and scan your PC for malware.

Some malware even fights back, defending itself from your many attempts to remove it. If your Windows Update feature stops working, preventing you from patching your PC, you’ve got malware. (CompTIA speak: OS update failures.) If other tools and utilities throw up an “Access Denied” road block, you’ve got malware. If you lose all Internet connectivity, either the malware is stopping you or the process of removing the malware broke your connection. (CompTIA refers to this as being unable to access the network, which seems very polite.) In this case, you might need to reconfigure your Internet connection: reinstall your NIC and its drivers, reboot your router, and so on.

Even your browser and anti-malware applications can turn against you. If you type in one Web address and end up at a different site than you anticipated, this is known as a browser redirection and it means that a malware infection might have overwritten your hosts file. The hosts file overrules any DNS settings and can redirect your browser to whatever site the malware adds to the file. Most browser redirections point you to phishing scams or Web sites full of free downloads (that are, of course, covered in even more malware). In fact, some free anti-malware applications are actually malware—what techs call rogue anti-malware programs. You can avoid these rogue applications by sticking to the recommended lists of anti-malware software found online at reputable tech sites, like Ars Technica, Tom’s Hardware, Anandtech, and others. Random/frequent pop-ups can be another annoying sign that your system is infected with some form of malware. Pop-up blocking has become fairly effective over the years, so if you’ve already ruled out the possibility that the browser isn’t up to date or that the pop-up blocker is off, it may be time to start looking for malware.

Watch for security alerts in Windows, either from Windows’ built-in security tools or from your third-party anti-malware program. Windows built-in tools alert you via the Action Center or the Windows Defender Security Center (Windows 10/11). The notification in Figure 27-16 is prompting us to activate Defender Antivirus. You don’t configure much here; it just tells you whether or not you are protected. The Action Center or Security Center will pop up a notification in the notification area whenever Windows detects a problem.



Figure 27-16  Notification to activate Defender Antivirus in Windows 11

Malware Prevention and Recovery
The only way to permanently protect your PC from malware is to disconnect it from the Internet and never permit any potentially infected software to touch your precious computer. Because neither scenario is likely these days, you need to use specialized anti-malware programs to help stave off the inevitable assaults. Even with the best anti-malware tools, there are times when malware still manages to strike your computer. When you discover infected systems, you need to know how to stop the spread of the malware to other computers, how to fix infected computers, and how to remediate (restore) the system as close to its original state as possible.

Dealing with Malware
You can deal with malware in several ways: anti-malware programs, training and awareness, patch/update management, and remediation.

At the very least, every computer should run an anti-malware program. If possible, add an appliance that runs anti-malware programs against incoming data from your network. Also remember that an anti-malware program is only as good as its updates—keep everyone’s definition file (explained a bit later) up to date with, literally, nightly updates! Users must be trained to look for suspicious ads, programs, and pop-ups, and understand that they must not click these things. The more you teach users about malware, the more aware they’ll be of potential threats. Your organization should have policies and procedures in place so everyone knows what to do if they encounter malware. Finally, a good tech maintains proper incident response records to see if any pattern to attacks emerges. He or she can then adjust policies and procedures to mitigate these attacks.



NOTE   One of the most important malware mitigation procedures is to keep systems under your control patched and up to date through proper patch management. Microsoft, Apple, and the Linux maintainers do a very good job of putting out bug fixes and patches as soon as problems occur. If your systems aren’t set up to update automatically, then perform manual updates regularly.

Anti-Malware Programs
An anti-malware program such as a classic antivirus program protects your PC in two ways. It can be both sword and shield, working in an active seek-and-destroy mode and in a passive sentry mode. When ordered to seek and destroy, the program scans the computer’s boot sector and files for viruses and, if it finds any, presents you with the available options for removing or disabling them. Antivirus programs can also operate as virus shields that passively monitor a computer’s activity, checking for viruses only when certain events occur, such as a program execution or file download.



NOTE   The term antivirus (and antispyware, or anti-anything) is becoming obsolete. Viruses are only a small component of the many types of malware. Many people continue to use the term as a synonym for anti-malware.

Antivirus programs use different techniques to combat different types of viruses. They detect boot sector viruses simply by comparing the drive’s boot sector to a standard boot sector. This works because most boot sectors are basically the same. Some antivirus programs make a backup copy of the boot sector. If they detect a virus, the programs use that backup copy to replace the infected boot sector. Executable viruses are a little more difficult to find because they can be on any file in the drive. To detect executable viruses, the antivirus program uses a library of signatures. A signature is the code pattern of a known virus. The antivirus program compares an executable file to its library of signatures. There have been instances where a perfectly clean program coincidentally held a virus signature. Usually, the antivirus program’s creator provides a patch to prevent further alarms.

Windows comes with Windows Defender (simply called Virus & threat protection in Windows 10/11, as shown in Figure 27-17), a fine tool for catching most malware, but it’s not perfect. You can also supplement Windows Defender with a second malware removal program. My personal favorite is Malwarebytes.



Figure 27-17  Windows 11 Virus & threat protection

These applications work exactly as advertised. They detect and delete malware of all sorts—hidden files and folders, cookies, Registry keys and values, you name it. Malwarebytes is free for personal use. Figure 27-18 shows Malwarebytes in action.



Figure 27-18  Malwarebytes

Try This!

Malwarebytes

If you haven’t done this already, do it now. Go to https://www.malwarebytes.com and download the latest copy of Malwarebytes. Install it on your computer and run it. Did it find any malware that slipped in past your defenses?

Now that you understand the types of viruses and how antivirus programs try to protect against them, let’s review a few terms that are often used to describe virus traits.



SIM   Check out the excellent Challenge! sim, “Fixing Viruses,” in the Chapter 27 sims over at https://www.totalsem.com/110X.

Polymorphic/Polymorphs  A polymorphic virus, often shortened to a polymorph, attempts to change its signature to prevent detection by antivirus programs, usually by continually scrambling a bit of useless code. Fortunately, the scrambling code itself can be identified and used as the signature—once the antivirus makers become aware of the virus. One technique used to combat unknown polymorphs is to have the antivirus program create a checksum on every file in the drive. A checksum in this context is a number generated by the software based on the contents of the file rather than the name, date, or size of that file. The algorithms for creating these checksums vary among different antivirus programs (they are also usually kept secret to help prevent virus makers from coming up with ways to beat them). Every time a program is run, the antivirus program calculates a new checksum and compares it with the earlier calculation. If the checksums are different, it is a sure sign of a virus.

Stealth  The term “stealth” is more of a concept than an actual virus function. Most stealth virus programs are boot sector viruses that use various methods to hide from antivirus software. The AntiEXE stealth virus hooks on to a little-known but often-used software interrupt, for example, running only when that interrupt runs. Others make copies of innocent-looking files.

User Education Regarding Common Threats
A powerful tool to prevent malware attacks and to reduce the impact of malware attacks when they happen is to educate your end users. Teach users to be cautious of incoming e-mail they don’t clearly recognize and to never click on an attachment or URL in an e-mail unless they are 100 percent certain of the source. With the rise in ransomware attacks over time, good anti-phishing training has become an absolutely essential tool in the IT security toolbox. Anti-phishing training involves teaching users how to recognize and critically examine incoming e-mails to better avoid falling prey to phishing attempts. Anti-phishing training has benefits that extend beyond the confines of the organization, as phishing attacks happen in SOHO environments as well. Regardless of where or why a person is using their device, this is some very useful education.

Explain the dangers of going to questionable Web sites to your users and teach them how to react when they see questionable actions take place. All Web browsers have built-in attack site warnings like the one shown in Figure 27-19.



Figure 27-19  Attack site warning

Nobody wants their systems infected with malware. Users are motivated and happy when you give them the skills necessary to protect themselves. The bottom line is that educated and aware users will make your life a lot easier.

Malware Prevention Tips
The secret to preventing damage from a malicious software attack is to keep from getting malware on your system in the first place. One way to do this is with a variation on traditional DNS—secure DNS. Secure DNS can describe software or a remote DNS provider that implements some additional filtering to block your devices from visiting all kinds of malicious Web sites.

If you can’t keep the malware from reaching your system, a good next step is catching it on the way in the door. All good antivirus/anti-malware programs (like the built-in Windows Defender Antivirus) include a virus shield that scans e-mail, downloads, running programs, and so on automatically (see Figure 27-20).



Figure 27-20  A Windows 10 virus shield (Defender Antivirus) in action

Use your antivirus shield. It is also a good idea to scan PCs daily for possible virus attacks. Last but not least, know the source of any software before you load it. Only install apps from trusted sources, such as the manufacturer’s Web site, or well-known app stores like Valve’s Steam service. Avoid untrusted software sources, like free registry cleaners from some support domain, at all costs.

Keep your antivirus and anti-malware programs (including Defender Antivirus) updated. New viruses and other malware appear daily, and your programs need to know about them. The list of virus signatures your antivirus program can recognize, for example, is called the definition file, and updated definitions play a critical role in keeping the latest malware out of your system. Fortunately, most antivirus programs update themselves automatically. Further, you should periodically update the core anti-malware software programming—called the engine—to employ the latest refinements the developers have included.

Boot Media Anti-Malware Tools
If you run anti-malware software and your computer still gets infected, especially after a reboot, you need a more serious anti-malware tool. Many anti-malware companies provide a bootable optical disc or USB flash drive (or show you how to make one) that enables you to boot from a known-clean OS and run the same anti-malware software, but this time not corrupted by the malware on your system.

Malware Recovery Tips
When the inevitable happens and either your computer or one of your user’s computers gets infected by malware such as a computer virus, you need to follow certain steps to stop the problem from spreading and get the computer back up safely into service. The CompTIA A+ 1102 exam outlines the following multistep process as the best practice procedures for malware removal:

1.   Investigate and verify malware symptoms.

2.   Quarantine infected systems.

3.   Disable System Restore in Windows.

4.   Remediate infected systems.

A.   Update anti-malware software.

B.   Scanning and removal techniques (e.g., Safe Mode, Preinstallation Environment).

5.   Schedule scans and run updates.

6.   Enable System Restore and create a restore point in Windows.

7.   Educate the end user.



EXAM TIP   In addition to this malware removal process, the CompTIA A+ 1102 objectives also mention OS reinstallation as another way to make sure your system is malware-free—just restore a full system backup (in Windows, you can take or restore one with the Backup and Restore utility). There are hurdles to using this approach.

You must have space to store one or more full backups, plan far enough ahead to have one or more recent backup available, know at least one is malware-free, and be prepared to either back up user files/data separately or lose any created/modified since the last backup. You won’t always have this option, but a good way to get started is to back up user files and data separately and take a full backup of the system itself once you have all of the software you need installed and configured. If you attempt to reinstall your OS from a backup and you find that your system is still infected, it may be time to try what is known as a clean install, which means just starting from a fresh copy of Windows and treating it like a new device. This has disadvantages as well, since it means starting from scratch with your system’s apps and data. In some cases, this may be your only choice, but it isn’t always ideal.

Recognize and Quarantine  The first step is to identify and recognize that a potential malware outbreak has occurred. If you’re monitoring network traffic and one computer starts spewing e-mail, that’s a good indicator of malware. Or users might complain that a computer that was running snappily the day before seems very sluggish.

Many networks employ software such as the open source PacketFence that automatically monitors network traffic and can cut a machine off the network if that machine starts sending suspicious packets. You can also quarantine a computer manually by disconnecting the network cable. Once you’re sure the machine isn’t capable of infecting others, you’re ready to find the virus or other malware and get rid of it.

At this point, you should disable System Restore. If you make any changes going forward, you don’t want the virus to be included in any saved restore points. To turn off System Restore in Windows, open the Control Panel and then the System applet. Click the System protection link to open the System Properties window with the System Protection tab displayed. In the Protection Settings section, select a drive and click Configure. In the System Protection dialog box that opens, select Turn off system protection. Repeat the procedure for each hard drive on the system.

Search and Destroy  Once you’ve isolated the infected computer (or computers), you need to get to a safe boot environment and run anti-malware software. You can try the Windows Recovery Environment in Windows 10/11, because it doesn’t require anything but a reboot. If that doesn’t work, or you suspect a boot sector virus, you need to turn to an external bootable source, such as a bootable optical disc or USB flash drive.

Get into the habit of keeping around a bootable anti-malware flash drive or optical media. If you suspect a virus or other malware, use the boot media, even if your anti-malware program claims to have eliminated the problem. Turn off the PC and reboot it from the anti-malware disc or flash drive (you might have to change CMOS settings to boot to optical or USB media). This will put you in a clean boot environment that you know is free from any boot sector viruses. If you only support fairly recent computers, you will likely be booting to a USB flash drive, so you can put a boot environment on a thumb drive for even faster start-up speeds.

You have several options for creating the bootable optical disc or flash drive. First, some antivirus software comes in a bootable version. Second, you can download a copy of Linux that offers a live USB or DVD option such as Ubuntu. With a live bootable device, you boot to the device and install a complete working copy of the operating system into RAM, never touching or accessing the hard drive, to give you full Internet-ready access so you can reach the many online anti-malware sites you’ll need for access to anti-malware tools.

Finally, you can download and burn a copy of the Ultimate Boot CD. Don’t worry, you can use it with a USB drive. It comes stocked with several antivirus and anti-malware programs, so you won’t need any other tool. Find it at https://www.ultimatebootcd.com. The only downside is that the anti-malware engines will quickly be out of date, as will their malware libraries.

Once you get to a boot environment, update your anti-malware software and then run its most comprehensive scan. Then check all removable media that were exposed to the system, and any other machine that might have received data from the system or that is networked to the cleaned machine. A virus or other malicious program can often lie dormant for months before anyone knows of its presence.

E-mail is still a common source of viruses, and opening infected e-mails is a common way to get infected. Viewing an e-mail in a preview window opens the e-mail message and exposes your computer to some viruses. Download files only from sites you know to be safe and avoid the less reputable corners of the Internet, the most likely places to pick up computer infections.



EXAM TIP   CompTIA considers the process of removing a virus part of the remediation step. Since you can’t remediate a PC until after a virus is gone, I’ve laid out the steps as you see here.

Remediate  Malware infections can do a lot of damage to a system, especially to sensitive files needed to load Windows, so you might need to remediate formerly infected systems after cleaning off the drive or drives. Remediation simply means that you fix things the virus or other malware harmed. This can mean replacing corrupted Windows Registry files or even startup files.

If you can’t start Windows after the malware scan is finished, you need to boot to the Windows Preinstallation Environment and use the Windows Recovery Environment/System Recovery Options.

With the Windows Recovery Environment (covered in detail in Chapter 16), you have access to more repair tools, such as Startup Repair, System Restore, System Image Recovery, Refresh, and Command Prompt (see Figure 27-21). Run the appropriate option for the situation and you should have the machine properly remediated in a jiffy.



Figure 27-21  System Recovery Options



EXAM TIP   Remember to re-enable System Restore and create a new restore point once the system has been repaired. Be aware that you may see recovery environment referred to as recovery mode on the exam, so don’t let that throw you off.

Educate End Users  The best way to keep from having to deal with malware is education. It’s your job as the IT person to talk to your users, especially the ones whose systems you’ve just spent an hour ridding of nasties, about how to avoid these programs. Show them samples of dangerous e-mails they should not open, Web sites to avoid, and the types of programs they should not install and use on the network. Any user who understands the risks of questionable actions on their computers will usually do the right thing and stay away from malware.

Finally, have your users run antivirus and antispyware programs regularly. Schedule them while interfacing with the user so you know it will happen.

1101
Firewalls
Much as anti-malware programs are essential tools in the fight against malicious programs on the Internet, firewalls are devices or software that protect an internal network from unauthorized access to and from the Internet at large. Firewalls use a number of methods to protect networks, such as hiding IP addresses and blocking TCP/IP ports.

A typical network uses one of two types of firewalls: hardware firewalls, often built into routers, and software firewalls that run on your computers. Both types of firewall protect your computer and your network. You also run them at the same time. Let’s look at both a typical SOHO router’s firewall features and your computer’s software firewall to see how they protect your network and your computers.

Hardware Firewall Settings
Most SOHO networks use a hardware firewall, often as a feature built into a router like the ASUS model shown in Figure 27-22. A hardware firewall protects a LAN from outside threats by filtering the packets before they reach your internal machines, which you learned about back in Chapter 21. Routers, however, have a few other tricks up their sleeves. From the router’s browser-based settings screen (see Figure 27-23), you can configure a hardware firewall. Let’s walk through a few of the available settings.



Figure 27-22  ASUS router as a firewall



Figure 27-23  Default Web interface

A hardware firewall watches for and stops many common threats—all you have to do is turn it on (see Figure 27-24). Hardware firewalls use Stateful Packet Inspection (SPI) to inspect each incoming packet individually. SPI also blocks any incoming traffic that isn’t in response to your outgoing traffic. You can even disable unused ports entirely, blocking all traffic in or out. But what if you want to allow outside users access to a Web server on the LAN? Because Network Address Translation (NAT) hides the true IP address of that system (as described in Chapter 21), you’ll need a way to allow incoming traffic past the router/firewall and a way to redirect that traffic to the right PC.



Figure 27-24  SPI firewall settings with firewalls enabled

Port forwarding/mapping enables you to open a port in the firewall and direct incoming traffic on that port to a specific IP address on your LAN. In the case of the Web server referenced in the previous paragraph, you would open port 80 (for HTTP packets) and instruct the router to send all incoming traffic to the server machine. Figure 27-25 shows port forwarding configured to send all HTTP packets to an internal Web server.



Figure 27-25  Port forwarding

Port forwarding isn’t the only way to open ports on a firewall. Port triggering enables you to open an incoming connection to one computer automatically based on a specific outgoing connection. The trigger port defines the outgoing connection, and the destination port defines the incoming connection. If you set the trigger port to 3434 and the destination port to 1234, for example, any outgoing traffic on port 3434 will trigger the router to open port 1234 and send any received data back to the system that sent the original outgoing traffic. Figure 27-26 shows a router set up with port triggering for an Internet Relay Chat (IRC) server.



Figure 27-26  Port triggering

If you want to go beyond port forwarding and port triggering and open every port on a machine, you need a screened subnet. A screened subnet puts systems with the specified IP addresses outside the protection of the firewall, opening all ports and enabling all incoming traffic (see Figure 27-27). If you think this sounds incredibly dangerous, you are right! Any PC inside the screened subnet will be completely exposed to outside attacks. Don’t use it!



Figure 27-27  Screened subnet (DMZ) set up on a SOHO router



EXAM TIP   CompTIA uses the term screened subnet in the A+ 1102 exam objectives, so be ready in case you see it on the exam, but on the job, you’ll more likely encounter the term demilitarized zone or DMZ (as shown in Figure 27-27).

Software Firewalls
While a hardware firewall does a lot to protect you from outside intruders, you should also use a software firewall, such as the firewalls built into each version of Windows, called (appropriately) Windows Defender Firewall or Windows Defender Firewall with Advanced Security. (Earlier versions of Windows just called the tool(s) Windows Firewall.) Windows Defender Firewall (see Figure 27-28) handles the heavy lifting of port blocking, security logging, and more.



Figure 27-28  Windows 10 Firewall settings

You can configure Windows Defender Firewall via the Windows Defender Firewall applet in Control Panel. Here you can fine-tune port security by setting up exceptions to open individual ports, or adjust application security by adding exceptions to let specific programs and services pass through the firewall. If you wanted to run a Minecraft server (a game that requires an Internet connection), for example, it would need to be on the list of exceptions for your firewall. Most programs you install add themselves to this list automatically, otherwise Windows Defender Firewall prompts you the first time you run it and asks if you want to add the program as an exception.



EXAM TIP   You can also manage Windows Defender Firewall through the Windows Security app. To activate or deactivate the firewall, visit the Firewall & network protection section. To activate, click the Turn on button under each network type you use. To deactivate, click the network name and then toggle Defender Firewall off.

When Microsoft first introduced Windows Firewall, way back in Windows XP, its biggest shortcoming was that it failed to consider that a single PC, especially a portable, might connect to multiple networks. You don’t necessarily want the same firewall settings used for both public and private networks. Microsoft developed a way for you to separate trustworthy networks (like the one in your house or at the office) from non-trustworthy networks (like a public Wi-Fi Internet connection at the airport) by including three network types: Domain, Private, and Guest or Public.

•   A Domain network is a Windows network controlled by a Windows domain controller that runs Active Directory Domain Services. In this case, the domain controller itself tells your machine what it can and cannot share. You don’t need to do anything when your computer joins a domain.

•   A Private network enables you to share resources, discover other devices, and allow other devices to discover your computer safely.

•   A Guest or Public network prevents your computer from sharing and disables all discovery protocols.

When your computer connects to a network for the first time, Windows will prompt you to choose the network type. Windows 10/11 asks if you want to allow other devices on the network to discover your PC (see Figure 27-29). It will mark the network Private if you answer yes; Public if you answer no. In either case, Windows uses your answer to decide whether to share files and resources or lock them down tight.



Figure 27-29  Windows 10 network options, public or private?

When your computer joins a domain, Windows automatically sets your network location to Domain (unless your domain controller chooses something different, which is unlikely).

When running on a Private (Home or Work) network, Windows enables Network Discovery and File and Printer Sharing as exceptions. When running on a Guest or Public network, Windows disables these exceptions.



EXAM TIP   The Network Discovery setting dictates whether a computer can find other computers or devices on a network, and vice versa. Even with Network Discovery activated, several firewall settings can overrule certain connections.

That’s the end of the story if your Windows machine never changes networks, but what about machines (mainly laptops) that hop from one network to another (see Figure 27-30)? In that case, you need different firewall settings for each network the system might encounter.



Figure 27-30  Many machines need more than one network setting.



EXAM TIP   Expect a scenario question on home vs. work vs. public network options on the CompTIA A+ 1102 exam. Just remember that you trust home and work networks, but don’t trust public ones.

Once you’ve picked a network type, you might want to customize the firewall settings further. If you click the Advanced settings option in the Windows Defender Firewall applet, you’ll discover a much deeper level of firewall configuration. In fact, it’s an entirely different tool called Windows Defender Firewall with Advanced Security (see Figure 27-31). You can also access it directly through the Administrative Tools in Control Panel.



Figure 27-31  Windows Defender Firewall with Advanced Security

From the Windows Defender Firewall with Advanced Security snap-in, you have much more control over how Windows treats exceptions. In the standard Windows Defender Firewall applet, you can only choose a program and make it an exception, giving it permission to pass through the firewall. But programs both send and receive network data, and the basic applet doesn’t give you much control over the “inbound” and “outbound” aspect of firewalls. The Windows Defender Firewall with Advanced Security snap-in takes the exceptions concept and expands it to include custom rules for both inbound and outbound data. Figure 27-32 shows the outbound rules for a typical Windows system.



Figure 27-32  Outbound Rules list

A rule always includes at least the following:

•   The name of the program

•   Group: an organizational group that helps sort all the rules

•   The associated profile (All, Domain, Public, Private)

•   Enabled/disabled status

•   Remote and local address

•   Remote and local port number

You can add, remove, and customize any rule to your liking. It quickly gets complicated, so unless you need to set a lot of custom rules, stick to the standard Windows Defender Firewall applet.

Internet Appliances
The discussion of firewalls barely scratches the surface of tools used to secure a large network. While enterprise networking is generally beyond the scope of a CompTIA A+ tech’s duties, the CompTIA A+ 1101 objectives cover a few devices critical to modern network security—IDS, IPS, and network taps—plus the concept of unified threat management. Let’s take a look.

An intrusion detection system (IDS) is an Internet application that inspects packets, looking for active intrusions. An IDS functions inside the network, watching for threats that a firewall might miss, such as viruses, illegal logon attempts, and other well-known attacks. Plus, because it inspects traffic inside the network, the IDS can discover internal threats, like the activity of a vulnerability scanner smuggled in on a flash drive by a disgruntled worker planning an attack on an internal database server.

An IDS always has some way to let the network administrators know if an attack is taking place: at the very least the attack is logged, but some IDSs offer a pop-up message, an e-mail, or even a text message to an administrator’s phone. An IDS can also respond to detected intrusions with action. The IDS can’t stop the attack directly, but can request assistance from other devices—like a firewall—that can.

An intrusion prevention system (IPS) is very similar to an IDS, but an IPS sits directly in the flow of network traffic. This active monitoring has a trio of consequences. First, an IPS can stop an attack while it is happening. There’s no need to request help from any other devices. Second, the network bandwidth and latency take a hit. Third, if the IPS goes down, the network link might go down too. Depending on the IPS, it can block incoming packets on-the-fly based on IP address, port number, or application type. An IPS might go even further, literally fixing certain packets on-the-fly.

A network tap is a piece of network monitoring hardware (although there are also smaller-scale software options) that sits between devices on the network and copies the traffic between them for later analysis. This comes in handy because, rather than directly interacting with the traffic and potentially interfering with it, a network tap allows the traffic to flow normally. The copied network traffic can then be inspected without the risk of network disruptions. Network taps can also be part of a virtual network, with a lot of additional flexibility in how they are used. Figure 27-33 shows an example of how a network tap might be used.



Figure 27-33  One potential configuration of a network tap

All these network Internet appliances, no matter how advanced and aware they become, are still singular tools in the box used to protect networks. That is why modern dedicated firewall/Internet appliances are built around providing unified threat management (UTM). UTM takes the traditional firewall and packages it with many other security services such as IPS, VPN, load balancing, antivirus, and many other features depending on the make and model. The UTM approach to building network gear helps build robust security deep into the network, protecting what really matters: our data.

1102
Authentication and Encryption
You know that the first step in securing data is authentication, through a username and password. But when you throw in networking, you’re suddenly not just a single user sitting in front of a computer and typing. You’re accessing a remote resource and sending login information over the Internet. What’s to stop someone from intercepting your username and password?

Firewalls do a great job of controlling traffic coming into a network from the Internet and going out of a network to the Internet, but they do nothing to stop interceptor hackers who monitor traffic on the public Internet looking for vulnerabilities. Worse, once a packet is on the Internet itself, anyone with the right equipment can intercept and inspect it. Inspected packets are a cornucopia of passwords, account names, and other tidbits that hackers can use to intrude into your network. Because we can’t stop hackers from inspecting these packets, we must turn to encryption to make them unreadable.

Network encryption occurs at many levels and is in no way limited to Internet-based activities. Not only are there many levels of network encryption, but each encryption level also provides multiple standards and options, making encryption one of the most complicated of all networking issues. You need to understand where encryption comes into play, what options are available, and what you can use to protect your network.

Network Authentication
Have you ever considered the process that takes place each time a person types in a username and password to access a network, rather than just a local machine? What happens when this network authentication is requested? If you’re thinking that information is sent to a server of some sort to be authenticated, you’re right—but do you know how the username and password get to the serving system? That’s where encryption becomes important in authentication.

In a local network, authentication and encryption are usually handled by the OS. In today’s increasingly interconnected and diverse networking environment, there is a motivation to enable different operating systems to authenticate any client system from any other OS. Modern operating systems such as Windows and macOS use standard authentication encryptions such as MIT’s Kerberos, enabling multiple brands of servers to authenticate multiple brands of clients. These LAN authentication methods are usually transparent and work quite nicely, even in mixed networks.

Data Encryption
Encryption methods don’t stop at the authentication level. There are a number of ways to encrypt network data as well. The encryption method is dictated to a large degree by what method the communicating systems will connect with. Many networks consist of multiple networks linked together by some sort of private connection, usually some kind of WAN connection such as old T1s or Metro Ethernet. Microsoft’s encryption method of choice for this type of network is called IPsec (derived from IP security). IPsec provides transparent encryption between the server and the client.

A virtual private network (VPN) can also use IPsec, but VPNs typically use other encryption methods. Speaking of VPNs, if you’re on an untrusted network, you can also protect your network traffic by tunneling it all through a VPN connection. Security-conscious organizations may even require all of their portable devices access the Internet through a VPN connection to one of their home offices.

Application Encryption
When it comes to encryption, even TCP/IP applications can get into the swing of things. The most famous of all application encryptions is the Secure Sockets Layer (SSL) security protocol, which was used to secure Web sites. Everyone uses Transport Layer Security (TLS) in HTTPS (HTTP over TLS) protocol these days. (SSL has been replaced by TLS, in other words.) These protocols make it possible to secure the Web sites people use to make purchases over the Internet. You can identify HTTPS Web sites by the https:// (rather than http://) included in the URL (see Figure 27-34).



Figure 27-34  A secure Web site



NOTE   HTTPS originally meant HTTP over SSL, so the “S” in HTTPS made sense. Most Web sites use the more robust TLS to encrypt connections. The Internet people just quietly switched TLS for SSL, but didn’t make a new acronym such as “HTTPT.” CompTIA refers to the “S” as standing for “secure,” which is a great way to remember the main difference between HTTP and HTTPS.

To make a secure connection, your Web browser and the Web server must encrypt their data. That means there must be a way for both the Web server and your browser to encrypt and decrypt each other’s data. To do this, the server sends a public key to your Web browser so the browser knows how to decrypt the incoming data. These public keys are sent in the form of a digital certificate. This certificate is signed by a trusted certificate authority (CA) that guarantees that the public key you are about to get is actually from the Web server and not from some evil person trying to pretend to be the Web server. A number of companies issue digital certificates, such as Verisign, Comodo, and many others.

Your Web browser has a built-in list of trusted certificate authorities, referred to as trusted root CAs. If a certificate comes in from a Web site that uses one of these highly respected companies, you won’t see anything happen in your browser; you’ll just go to the secure Web page, where a small lock icon will appear in the browser status bar or address bar. Figure 27-35 shows the list of trusted certificate authorities built into the Firefox Web browser.



Figure 27-35  Trusted certificate authorities

If you receive a certificate that your browser thinks is fishy, such as one that is expired or one for which the browser does not have a trusted root CA, the browser will warn you and usually give you some way to make an exception for the certificate, as shown in Figure 27-36.



Figure 27-36  Incoming certificate

We all have to make our own decisions here, but you should usually heed the browser’s warning and advice. Most certificate warnings are invalid for boring reasons, like the site owner forgetting to update the certificate on time. But the certificate warnings could just as easily indicate that the site or your connection to it is compromised! Only add an exception if you know it’s safe. You might, for example, need to add an exception to access a site on your organization’s intranet.

Wireless Issues
Wireless networks add a whole level of additional security headaches for techs to face, as you know from Chapter 20. Here are a few points to consider:

•   Set up wireless encryption, at least WPA2 but preferably the more secure WPA3 if your device supports it, and configure clients to use it.

•   Disable DHCP and require your wireless clients to use a static IP address.

•   If you need to use DHCP, only allot enough DHCP addresses to meet the needs of your network, to avoid unused wireless connections.

•   Change the WAP’s SSID from the default.

•   Filter by MAC or IP address to help limit network access to known clients only.

•   Change the default username and password. Even if the defaults are generated and look secure, knowledge of how they were generated might make them easier to guess.

•   Update the firmware as needed.

•   If available, make sure the WAP’s firewall settings are turned on.

•   Configure SOHO router NAT/DNAT settings.

•   Use SOHO router content filtering/parental controls.

•   Consider physical security of SOHO router.

Chapter Review
Questions
1.   What is the process for using or manipulating people to gain access to network resources?

A.   Cracking

B.   Hacking

C.   Network engineering

D.   Social engineering

2.   Which of the following might offer good hardware authentication?

A.   Strong passwords

B.   Encrypted passwords

C.   NTFS

D.   Smart cards

3.   Which of the following is used for biometric authentication?

A.   Motion sensor

B.   RSA token

C.   Palmprint scanner

D.   Kerberos

4.   Which hardware firewall feature enables incoming traffic on a specific port to reach an IP address on the LAN?

A.   Port forwarding

B.   NAT

C.   Screened subnet

D.   Multifactor authentication

5.   Zander downloaded a game off the Internet and installed it, but as soon as he started to play, he got a Blue Screen of Death. Upon rebooting, he discovered that his Documents folder had been erased. What happened?

A.   He installed spyware.

B.   He installed a Trojan.

C.   He broke the Group Policy.

D.   He broke the Local Security Policy.

6.   Which of these choices would provide better security for Mary’s Wi-Fi router?

A.   Secure DNS

B.   WEP

C.   WPA2

D.   WPA3

7.   Malware that encrypts a hard drive and demands payment in exchange for decryption is known as what?

A.   Trojan

B.   Cryptominer

C.   Ransomware

D.   Keylogger

8.   John dressed up in a fake security guard uniform matching the ones used by a company and then walked into the company’s headquarters with some legitimate employees in an attempt to gain access to company resources. What kind of attack is this?

A.   Administrative access

B.   Data destruction

C.   Spoofing

D.   Tailgating

9.   Andre, CEO of a midsized company, received an e-mail that appeared to be from a colleague that wanted to close a major deal. Suspicious because the deal in question didn’t exist, he called in his IT security team who determined that it came from a spoofed IP address. Which of the following best describes this attempted attack?

A.   Phishing

B.   Whaling

C.   Zero-day

D.   Tailgating

10.   Edna wants to put a policy in place at her company to prevent or at least limit viruses. What policies would offer the best solution?

A.   Install antivirus software on every computer. Teach users how to run it.

B.   Install antivirus software on every computer. Set up the software to scan regularly.

C.   Install antivirus software on every computer. Set up the software to update the definitions and engine automatically. Set up the software to scan regularly.

D.   Install antivirus software on every computer. Set up the software to update the definitions and engine automatically. Set up the software to scan regularly. Educate the users about sites and downloads to avoid.

Answers
1.   D. Social engineering is the process of using or manipulating people to gain access to network resources.

2.   D. Smart cards are an example of hardware authentication devices.

3.   C. Palmprint scanners are a method of biometric authentication.

4.   A. To open a port on your hardware firewall and send incoming traffic to a specific PC, use port forwarding.

5.   B. Zander clearly installed a Trojan, a virus masquerading as a game.

6.   D. Mary should set up WPA3 on her Wi-Fi router.

7.   C. Malware that demands money in exchange for hard drive decryption is called ransomware.

8.   D. John just practiced tailgating on the unsuspecting company.

9.   B. Andre was the target of a whaling attempt.

10.   D. The best policy includes updating the software engine and definitions, scanning PCs regularly, and educating users.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Chapter 27 Securing Computers
Chapter 28 Operational Procedures
Appendix A Mapping to the CompTIA A+ Objectives
42h 21m remaining
CHAPTER 28
Operational Procedures
In this chapter, you will learn how to

•   Implement best practices associated with documentation and support systems information management

•   Explain basic change-management best practices

•   Summarize environmental impacts and local environmental controls

•   Explain the importance of prohibited content/activity and privacy, licensing, and policy concepts

The term operational procedures encompasses a lot for any organization, from best practices for safety (Chapter 1) to dealing with security risks (Chapter 27); from organizational polices for limiting access to sensitive data (also Chapter 27) to proper communication techniques and professionalism all techs should employ (again, Chapter 1). The CompTIA A+ 1102 exam even throws in basics of scripting (Chapter 15) and remote access technologies (Chapter 21) as operational procedures (though labeling them as such feels like a reach to me).

This chapter explores another aspect of operational procedures—namely, business practices that enable continuity, a fancy way of saying that an organization should keep working more or less the same in the face of both mundane day-to-day change and sudden disasters. We’ll focus here on four categories of business continuity and operational procedures: documentation and support systems management, basic change management, environmental impacts and controls, and prohibited content/activity, privacy, licensing, and policies.

1102
Implementing Best Practices Associated with Documentation and Support Systems Information Management
Organizations need documentation to provide continuity and structure. Documentation can take many forms, but the four categories of concern to a new tech are asset management, custom installation of software packages, ticketing systems, and knowledge base/articles.

Asset Management
Techs help organizations institute asset management practices to protect organizational assets. These include inventory lists, database systems, and barcodes, among other things.



EXAM TIP   Although the term “barcode” is not likely to appear on the CompTIA A+ 1102 exam, organizations still use this technology to track assets.

Inventory Lists
Have you ever worked for a company that issued you a piece of equipment that had a company-specific tag on it? This could be anything from a number engraved onto the handle of a shovel to an RFID tag attached to a computer. Regardless of the form, every organization has to track the physical and virtual assets that it has in its inventory at any given time. For a tech company, the inventory might include, for example, 32 Dell laptops, 32 USB-C power adapters, 32 copies of Microsoft Office, and so forth. Regardless of the form, inventory lists are found in every organization and document the assets that the organization has deployed and holds in reserve. Keeping track of these assets is an essential function. Inventory lists document the who, what, and where of each asset so that an organization can track all its assets.

Database System
For now, let’s keep this really simple. In the context of asset management, database systems are used to track things like who has the asset (e.g., Melissa Layne), what type of asset this person has (e.g., a laptop), and where this asset is located (e.g., the research and innovation department). Sometimes database systems document why the person is using the asset (e.g., to analyze quantitative and qualitative data for her department). Asset management database systems can also be used for things like

•   Recording an asset’s description: make, model, serial numbers, asset barcode, asset category, etc.

•   Recording an asset’s acquisition and disposal information

•   Linking purchase receipts, manuals, and other digital documents to asset records

•   Tracking an asset’s status and location

•   Obtaining a report listing assets assigned to a department or employee

•   Recording asset maintenance and repair histories (date, details, costs, etc.)

Some of the listed items will be discussed further in the “New User Set-Up Checklist” and “End-User Termination Checklist” sections later in the chapter. As you progress through more advanced topics and courses, there will be much more to learn about database systems.



NOTE   The difference between an inventory list and a database system is that an inventory list keeps track of the assets that the organization has given out to people and that it has as “extras.” A database system tracks more detailed information about the assets.

Barcodes
Many inventory items have simple stickers or printed labels with barcodes—unique symbols/numbers that track specific items. Figure 28-1 shows a typical barcode. A barcode acts as a fingerprint for an item, binary code that can be readily scanned. One drawback to barcodes is that they’re read-only. You can’t add data or information to them at all.



Figure 28-1  Barcode on an SSD encoding its serial number

Asset Tags and IDs
Asset tags can use the radio frequency identification (RFID) wireless networking protocol to also keep track of inventory (see Figure 28-2). The asset tag includes an RFID tag (consisting of a microchip and antenna), which an RFID scanner or reader can electronically read and identify even without line of sight to the item. Most RFID tags are passive, meaning that the tag receives all the power it needs from the scanner’s signal! An active RFID tag, on the other hand, uses a battery or external power source to send out and receive signals. Both types of RFID tags enable asset management. Unlike barcodes, the information stored in an RFID tag can be updated with new details.



Figure 28-2  RFID tag

Procurement Life Cycle
This is one of those topics that is a pain to talk about because every organization has its own process. For small companies, the procurement life cycle can be as simple as picking up the phone, making a few calls, and getting what they need. For highly bureaucratic organizations, the procurement life cycle can be a years-long process involving thousands of pages of rules. At its core, the procurement life cycle is the process involved in buying assets that your project needs. However, we are going to try to keep this simple and break down the procurement life cycle into six simple phases.

Identify Needs  Develop an understanding of what you need and why you need it. This can involve simple statements of work or complex documents detailing very specific objectives. This phase will vary from organization to organization and across use cases.

Evaluate Suppliers  Once you know what you need and why you need it, you need to scope out who provides the product or service you require. Sometimes this can be completed with a simple Web search. Other times it may require you to conduct a lengthy series of interviews. Typically, the cost of an implementation is directly proportional to the amount of time you spend evaluating the best supplier.

Negotiate Terms and Finalize the Purchase Order  When you have decided on the best supplier, you need to contact that supplier and enter into a negotiation of terms. Think of this as buying a car, but at a much larger scale. Everyone is willing to make concessions. In the world of business, it is how many concessions you can get, while maintaining quality, that matters in the end.

So, now you have bargained your way down to the very best terms that you can extract from the supplier. This is known as their best and final offer. You agree that this works for your organization, which then sends to the supplier a purchase order (PO) with relevant payment information. The supplier in turn sends an invoice to your organization to initiate the billing process.

Receive Invoice and Process Payment  Your organization receives an invoice, aligned with the purchase order, and sends the supplier the funds to facilitate payment. Are you finished? Not just yet.

Delivery and Audit  After the supplier has been paid, they deliver the service or product as promised. Upon implementation, you begin to monitor how effective the new service or product is compared to your previous state. This is called the audit.

Maintain Records for Future Audits  Everything is up and running. You are happy. The supplier is happy. Now you must continue to track effectiveness versus the return on investment (ROI), to assess periodically whether this solution is still effective or, if you need a new approach.

Warranty and Licensing
In the role of an asset manager, you will also need to keep track of warranty and licensing documentation. Although this may seem like an overwhelming task, as long as you have established solid security measures and adhere to licensing compliance requirements, you will be able to easily manage and update this important documentation. This in no way means that this job is easy. It’s not. In terms of licensing compliance, the stakes are high. If, for example, a company has 50 unlicensed copies of a software application running on 400 of its computers, the company could face fines as high as $500,000!

Unlicensed assets are also linked to potential data loss. Data loss leads to privacy violations, and the snowball continues to get bigger and bigger. There are, however, software applications that can make the tracking job easier, such as various Software as a Service (SaaS) products that make maintaining compliance a little easier.

Assigned Users
Your organization may receive a set number of licenses for a particular product, such as software. This represents how many people in your organization can use the product. Sometimes suppliers are flexible, and they will say, “As long as you don’t have more than ten people accessing our product, then everything is fine.” Other times, suppliers want to know specifically who is using their product, and if this changes they will want to know who the replacement is. In this case the users are known as assigned users.

Individual organizations may also have their own rules about assigning user roles to individuals, even if the supplier does not require the organization to provide identities for individual users. When this is the case, it is often related to audits that determine if the right people are receiving access to the right products or services to ensure optimal performance of the organization as a whole.

Documentation for Policies, Procedures, Industry Standards, and Compliance
Organizations of every size should have a library of documents that cover the organization’s policies and procedures and any industry standards and compliance regulations that apply to the organization. New employees should be given a package of these documents the first week on the job and instructed to review them. The onus, however, is on the employer to have these documents ready for new employees and to instill the need to apply the core principles contained within them to the organizational culture. Doing so will prevent issues, avoid inefficiencies, and create a sense of ownership.

Standard Operating Procedures
From a technician’s point of view, the most common operating issue revolves around software, such as what sort of software users are allowed to install on their computers or, conversely, why you have to tell a user that he can’t install the latest application that may help him do his job more effectively because that software isn’t on the approved list. This can lead to some uncomfortable confrontations, but it’s part of a tech’s job.



EXAM TIP   The CompTIA A+ 1102 exam objectives call out procedures for custom installations of software packages. If your organization has rules about what software you can and can’t install, it probably also has processes that lay out what to do when users request job-related software that isn’t on the approved list. For example, folks who work out at NASA’s Johnson Space Center here in Houston have to open a support ticket with the IT department if they need a program that isn’t on the approved list. From there, the process governs how to decide if the software’s license is acceptable, whether it will cause security or compatibility problems, and so on.

The concepts behind standard operating procedures (SOPs) are not meant to make a tech’s life difficult and mundane. They are meant, for example, to stop users with insufficient technical skill or knowledge from installing malicious programs or applications that will destabilize their systems, thus keeping technical support calls down, which in turn enables techs to focus on more serious problems.

Organizations largely develop standard operating procedures for employees for two reasons: to enhance the success of the organization, and to meet government-related compliance requirements. Organizational policies include regulatory compliance policies, acceptable use polices, and password policies, among others. Because security is growing to include SOPs associated with regulatory compliance, risk management, end-user training, and so forth, those who have service desk responsibilities will likely have to eventually incorporate these SOPs to keep the organization secure.

Acceptable Use (AUP)
An acceptable use policy (AUP) describes what employees can and cannot do with the organization’s property. An example of a common AUP provision is that a company laptop can be used only for company business. Another common AUP provision bars employees from accessing illegal Web sites from the organization’s computers. AUPs are often very detailed and specific documents that employees must read, agree to, and sign as a step in the employment process.

Network Topology Diagrams
Network documentation provides a road map for current and future techs who need to make changes or repairs over time. For the most part, CompTIA Network+ techs and system administrators handle the oversight of the network, but CompTIA A+ techs do a lot of the implementation of fixes. A network topology diagram provides a map for how everything connects in an organization’s network. These diagrams include switches, routers, WAPs, servers, and workstations (see Figure 28-3). More complex diagrams identify connection types and speeds, and the technologies in use (listing a WAP as an 802.11ax or Wi-Fi 6, for example). Many organizations rely on the Cisco icon set as a universal visual aid for creating these diagrams (see Figure 28-4).



Figure 28-3  Typical network topology diagram



Figure 28-4  A sampling of Cisco network diagram icons

Regulatory Compliance Requirements
Part of a government’s job is to ensure safe work environments and minimize exploitation of workers. To this end, governments develop rules and regulations that specify how organizations are supposed to manage their workplaces, workers, and materials. Properly run organizations enforce regulatory compliance requirements—following the laws and regulations—to maintain a healthy workforce. Compliance means, in a nutshell, that members of an organization must abide by or comply with all of the rules that apply to the organization. Statutes with funny names such as Sarbanes-Oxley impose certain behaviors or prohibitions on what people can and cannot do in the workplace.

It has become commonplace for Web sites and applications to collect useful and informative data about their visitors and users. In this age of information overload, it’s equally important that visitors and users understand that their usage data is being collected. To ensure there is understanding and agreement from both parties, many organizations have integrated a splash screen prior to using the application or Web site requiring users to agree to things such as data privacy, terms and conditions, or other compliance measures.

New-User Setup Checklist
To make the first day of work easier for new employees, most employers have developed documentation to make sure that they are not overwhelmed and, more importantly, that they have everything they need to start working.

One of these documents is a new-user setup checklist, which is a best practice associated with the documentation and support systems information management that techs use to ensure that a new user is set up with the proper equipment, network credentials, company policies and procedures, and so forth. New-user setup checklists are flexible, meaning that predefined items can be listed in a set order (1, 2, 3, etc.). Although the items may vary based on the employee’s position and role in the company, here are some common items you might need to provide to a new employee:

•   Technology: PC, laptop, mouse/mouse pad, keyboard, phone, webcam, external storage

•   Software: product/project development, analytical, statistical, etc.

•   E-mail/messaging setup (e.g., Microsoft Outlook, Teams, Zoom, Teams, etc.)

•   Password security

•   Documentation for hardware or software for further reference on functionality provided

•   Documentation on data privacy policies for new employee to read and sign

•   Contact information provided if new employees have questions, issues, concerns, etc.

Good onboarding gets users to the point where they have everything they need to perform their job functions, they understand how to use it, and they understand and agree to any related security policies that could have a significant negative impact on them and the organization should they not practice them.

End-User Termination Checklist
For any number of reasons, voluntary or involuntary, an employee may leave an organization. Regardless of the reason, the IT department should complete an end-user termination checklist to ensure that the departing employee returns all equipment issued by the organization, that their network access has been removed, and, where applicable, that knowledge transfer is facilitated, such as requesting documents the user has created that could help their successor. If you are given this responsibility in your organization, you need to follow your organization’s checklist carefully to make sure that the former employee cannot engage in malicious behavior.

Ticketing Systems
Ticketing systems help handle requests for technical assistance. Many companies use ticketing software internally to provide employees with technical support. Some companies also offer consumer ticketing services. For example, if a user encounters a problem with software, the system might allow them to submit a ticket to the software vendor to resolve the problem.

A ticketing system for internal use usually involves requests to an IT department. It streamlines the process for submitting problems and getting them resolved. Ticketing software for consumers might be assigned to a support person who is familiar with typical technical issues. According to CompTIA, some of the information needed to resolve an issue using a ticketing system might include:

•   User information (name, location, job position, etc.)

•   Date

•   Device information (type of device, model, serial, etc.)

•   Categories

•   Severity

•   Escalation levels

•   Problem description (clarity here is very important)

•   Progress notes

•   Problem resolution (never forget this, always document your findings)

Clear, concise writing is critical when it comes to the problem description, notes, and resolution. You probably won’t be the only tech responding to every ticket, so it’s important that your coworkers can understand what the problem is and how it is being addressed. Figure 28-5 shows how this information might be presented on a trouble ticket.



Figure 28-5  A typical interface for a ticketing system

Here is an example of how a ticketing system process might play out. Jamie’s company computer is not starting. She contacts the IT department by submitting a helpdesk “ticket” in which she provides necessary information (name, date, device information, description of problem, etc.) that helps the responding tech, Jamal, get an initial idea of what the issue is and how to help resolve the issue.

Next, depending on the type of ticketing system, Jamal the tech contacts user Jamie and asks her to explain in further detail what is wrong with the computer. Jamal starts troubleshooting by asking questions such as “Is the computer plugged in?” and “Is the power source completely plugged into the PC?” He also takes notes, documenting his questions and her responses, and any information about their interaction regarding the issue. Jamie responds to Jamal’s questions until they have pinpointed the issue with the computer. Depending on the severity of the issue, the issue either will be resolved and the ticket will be closed or, if the issue cannot be resolved, the ticket will be escalated to another tech who might have more in-depth experience and guidance to help solve Jamie’s PC issue.

Knowledge Base/Articles
Organizations use documentation to enable cooperation among employees and coordination among departments. From a tech’s perspective, documentation helps in troubleshooting various issues. Creating and maintaining a company knowledge base—a set of documents that tell the tale of equipment used, problems encountered, and solutions to those problems—provides an essential tool for current and future techs. The articles could be, for example, articles from third-party tech sources that apply to the organization’s equipment, such as Cisco articles about the routers the organization uses.

Change-Management Best Practices
CompTIA A+ techs are well positioned to offer valuable change management insights. You see what works, what doesn’t, and what needs to change. The old laser printers in the accounting department, for example, can’t keep up with user needs and you’re spending way too much time each week keeping them running. And you’re tired of users complaining to you. Change is needed.

Change isn’t only grass-roots driven, but often comes from the top. Every organization has formal and informal change-management processes and a designated individual to oversee these processes. You can’t just buy a new laser printer, for example, without considering the cost and impact. You can’t upgrade the operating systems for 100 users without thorough testing and analysis of the OS. Let’s take a closer look at change-management best practices, which include documented business processes and the change-management process.

Documented Business Processes
Every step of a change needs documented business processes. Documented business processes include a plan to return an infrastructure to its pre-change environment, the steps to create an operational environment for development and/or testing, as well as appointing an individual who is responsible for these types of processes. Let’s take a look at these three documented business processes, which the CompTIA A+ 1102 objectives identify, respectively, as rollback plan, sandbox testing, and responsible staff member.

Rollback Plan
What if an executed change is a failure? This happens more than you think. Therefore, before a change occurs, a rollback plan must be in place that defines the steps needed to return the infrastructure to its pre-change environment. OS rollbacks, uninstallation, or return to old equipment are all possible parts of a good rollback plan.

For example, Jamie at Bayland Widgets Corp. (BWC) wants to upgrade 16 systems in the design lab from Windows 7 to Windows 11. She obtains approval from management and subsequently implements the upgrade. After a few days, several users have complained that an important CAD application BWC uses is having issues, such as software freezes.

Jamie looks at the rollback plan documentation that lays out the steps for undoing the upgrades. She follows through with the undo process, making notes about the steps, then awaits further instructions for how to get the design lab computers upgraded without failures.

Sandbox Testing
Simply put, a sandbox is a place where you can experiment without messing up the primary system. A sandbox usually is a virtualized environment (refer to Chapter 22) that isolates the test machine from the host machine to avoid causing additional problems. The ability to restore a VM or container from a snapshot makes each of them an ideal choice for sandbox testing, which entails checking out new and updated applications without putting the systems and data you depend on at risk.

Responsible Staff Member
Activities like rollback plans and sandbox testing (and change management, discussed in the next section) are typically led by a responsible staff member (RSM). This individual leads projects like these by following policies, processes, and procedures that have been developed (and likely refined over time) toward facilitating, coordinating, and implementing projects.

For example, Janice, the director of the accounting department, needs 20 of her employees’ computers upgraded to Windows 11. Who does she contact to initiate this change? The responsible staff member, of course! This person is appointed by IT department leadership and will assist Janice from the beginning of the upgrade all the way to the end. Depending on the size of your organization, the RSM may be the person who addresses the problem themselves or a manager who coordinates with others to get it fixed.

Change-Management Process
A change-management process enables organizations to implement changes to IT infrastructure in a safe and cost-effective manner. Any organization with a change-management process should have documents that lay out the steps, who performs them, and how they go about it.

One of your first jobs as a tech is to consult these documents so that—when change comes your way (either from you or from on high)—you’ll already understand the process. When it’s time for a change, start by reviewing this process to avoid being embarrassed about (and possibly disciplined for) missing some important step.

There’s no single guide to change management, though most organizations follow common-sense guidelines. This section provides an outline of the change-management best practices CompTIA recommends. A package created by a CompTIA A+ tech should include all the documentation just discussed, plus receipts, overtime records, an inventory of changed systems, lists of new users created, signed end-user acceptance forms, and so on.

Request Forms
A request form kicks off the change-management process. At some point, someone (maybe you or maybe the CIO of the company you work for) identifies a problem that needs to be fixed and submits a basic request form to IT. Depending on your organization, this form may range from a simple one-pager to an extremely complex set of documents. However, regardless of the level of complexity, all request forms have three things in common. They state the problem, what needs to be fixed, and what the desired outcome is.

Beyond these essentials, other information may be needed, such as why this change is important, who it will benefit, how soon it needs to be implemented, and a host of other factors. Again, these requirements all vary depending on the organization you work for and the procedures and requirements it has put in place. The key thing to remember here is that if you submit a change request form, you should be ready to explain why the change is needed. If you can do that, the rest is all a matter of following processes, which you will pick up quickly.

Determine the Purpose of the Change
No organization is ever going to give you new equipment or allow you to make upgrades without knowing why they are needed. To propose a change, you’ll almost certainly need to document the purpose of the change. Returning to the scenario from the earlier “Rollback Plan” section in which Jamie at BWC wanted to upgrade 16 systems in the design lab from Windows 7 to Windows 11, users have demanded the latest OS from Microsoft to better serve customers who have (all) jumped to Windows 11. The purpose of the change, therefore, is improved performance and support for clients.

Determine the Scope of the Change
Usually included as part of the purpose of the change, the scope of the change defines who and what this change will affect. This includes an inventory of all systems involved, the number of people involved in making the change, how long the change will take, and often the estimated cost of the change.

In our design lab scenario, Jamie estimates that in order to upgrade 16 computing devices to Windows 11, she will need approximately three people to help with the upgrade, and it should be completed in three days. With this information, in addition to a determination of which edition of Windows 11 will be installed, Jamie now has a pretty good idea of what her overall budget will be.

Document the Date and Time of the Change
Knowing when changes will be deployed is essential. Depending on the application and your organization, anywhere from a few people to literally thousands of people may be impacted. Thus, a clearcut date and time needs to be established for when any system changes will occur. You don’t want to be “that guy” who pushes the big red button and sends their company into complete chaos. Imagine that your alarm clock has been set to play heavy metal music at maximum volume and you have no idea what time it will go off. If the music starts to blare before you want to get up, you would very likely wake up extremely grumpy and the day that followed would be far from optimal. This is exactly what your colleagues will be like if you don’t adequately document the date and time associated with system changes.

Determine Impact
This phase of change management can be a little tricky, depending on the existing level of documentation related to your systems. Your goal here is to identify which systems the change will impact (both the system the change is made to and its interconnected systems) and to what extent they will be impacted (e.g., unavailable to users for two hours). In a perfect world, every organization should have a complete architectural mapping of all systems and the interrelationships that exist between components. When this is the case, you can reference the documentation and trace where connections exist and deduce where the change will likely impact other systems. This enables you to give everyone a heads-up as to what to expect, when it will happen, and what steps they might need to take. However, you aren’t always going to be in a situation where you have access to a complete overview of how systems are connected.

There is an old joke in the IT world that goes like this, “There is only one guy who knows how this all works and he died three years ago.” Yea, it’s rather gallows humor, but unfortunately it is frequently applicable in a general sense. As organizations grow, they have the tendency to stack systems upon systems, with little or no documentation explaining what happened, when it happened, or why it happened. If this describes your organization, you are in the unenviable spot of basically flying with one eye covered. However, by acquainting yourself with the systems that you will be working with, you will quickly learn how things are connected, and when asked to perform this type of assessment, you can make assumptions as to where interrelationships exist. The key here is to remember the old adage “Better safe than sorry.” So, if anything, be overly cautious and prepare others for the worst-case scenario.

Analyze the Level of Risk
All changes to infrastructure come with risk. A proper change-management request will certainly require a risk analysis, a detailed assessment of possible problems that could result from the change to determine the risk level of the change. Determining the risk level will include the development of a non-exhaustive list of questions covering as many possible things that could go wrong during the change. What if the upgrade fails? Has the new application been tested on a sample system? Will the new computers have adequate firewalls? Don’t panic (well, not too much), as any risk analysis will almost certainly be passed off to a security person in your organization—but that person might have great interest in your opinions and concerns!

Change Board Approvals
So, Jamie has all this documentation to back up her request to upgrade 16 design lab computers to Windows 11. She has documented the purpose and scope of the change, the proposed date and time of the change, the affected systems and corresponding impact, and the level of risk the changes poses. Now she needs to submit this documentation to the change board to obtain their approval. The change board consists of techs and representatives from management, IT security, and administration who meet on a regular basis (quarterly is common). They review the change documentation and either approve or deny the change, but more often than not they first ask for more information or details, making a “proposal–rejection–fix–back to change board” cycle that repeats itself until everyone is satisfied.

Plan for the Change
If you receive approval from the change board, you’ll need to plan for the change. What needs to be done before the change starts? What needs to be purchased? Where will new, uninstalled equipment be stored? On which days will you implement this change? During what time period? Who will cover your other duties while you’re otherwise engaged? Anything that needs to be ready before you start is covered in the plan for the change.

End-User Acceptance
Part of successful change management is educating the end users in both the need for the change and how to adapt to changed systems. End-user acceptance is vital for successful change. More than anything else this means training. Do the users know how to use the new features on your super printer? What new features in this OS upgrade do end users need to learn? Are the end users versed in the new application (and know not to use the old one)?

Now let’s shift gears and discuss how you and end users need to be aware of environmental impacts and how to control them so that your organization’s existing technology is protected, as well as technology you may have proposed to implement in a potential change-management plan.

Environmental Impacts and Local Environmental Controls
Computers are surrounded by a host of dangers all just waiting to wreak havoc. In addition to power surges, brownouts, and blackouts, discussed in Chapter 7, there are other factors that could negatively affect your computer. Environmental factors such as chemicals stored near your computer, dust, heat, cold, wet…it’s a jungle out there!

Managing environmental controls requires a person who can multitask. They must make sure the equipment is working properly and is maintained and monitored, and they must also be ready for any unexpected variables to pop up in the interim. A person in this type of position undoubtedly needs clear processes and procedures in place to make sure that a certain level of protection has been met.



EXAM TIP   Expect questions on environmental threats, impacts, and how to control them on the CompTIA A+ 220-1102 exam.

Temperature, Humidity, and Ventilation
Proper local environmental controls help secure servers and workstations from the environmental impact of excessive heat, dust, and humidity. Such environmental controls include air conditioning, proper ventilation, air filtration, and monitors for temperature and humidity. A CompTIA A+ technician maintains an awareness of temperature, humidity level, and ventilation, so that he or she can tell very quickly when levels or settings are out of whack.

A computer works best in an environment where the air is clean, dry, and room temperature. CompTIA doesn’t expect you to become an environmental engineer, but it does expect you to explain and deal with how dirty or humid or hot air can affect a computer. We’ve covered all of these topics to some extent throughout the book, so let’s just do a quick overview with security in mind.

Ventilation Patrol
Most computers are designed to operate at room temperature, which is somewhere in the area of 22°C (72°F) with the relative humidity in the 30–40 percent range. Colder and dryer is better for computers (but not for people), so the real challenge is when the temperature and the humidity go higher.

A modern office will usually have a good heating, ventilation, and air conditioning (HVAC) system, so your job as a tech is to make sure that nothing interferes with the proper functioning of your HVAC system. That means you’re pretty much always on ventilation patrol. Watch for the following to make sure air is flowing:

•   Make sure ducts are always clear of obstructions.

•   Make sure duct dampers are adjusted for proper airflow (not too hot or too cold).

•   Make sure equipment is located in an area with proper ventilation.

Dirty Air
Dust and debris aren’t good for any electronic components. Your typical office air conditioning does a pretty good job of eliminating the worst offenders, but not all computers are in nice offices. No matter where the computers reside, you need to monitor your systems for dirt. The best way to do this is observation as part of your regular work. Dust and debris will show up all over the systems, but the best place to look are the fans. Fans will collect dust and dirt quickly (see Figure 28-6).



Figure 28-6  Dirty fan

Dust Cleanup  All electronic components get dirty over time. To clean them, you need to use either compressed air or a nonstatic vacuum. So which one do you use? The rule is simple: If you don’t mind dust blowing all over the place, use compressed air. If you don’t want dust blowing all over the place, use a vacuum.

Airborne Particle Protection  Computers and the individuals operating them are typically in enclosed, indoor environments. Just as you would in your own home, changing the air filters on a regular basis reduces the amount of airborne particles coming through the filters. Dedicate a certain date to change all of the filters and make sure to always keep an inventory of the correct size filters ready for the next filter change. Another option to protect against airborne particles is to wear a mask such as the N95 masks sold in many home improvement and hardware stores.

Location/Equipment Placement  Equipment closets filled with racks of servers need proper airflow to keep things cool and to control dusty air. Make sure that the room is ventilated and air-conditioned (see Figure 28-7) and that the air filters are changed regularly.



Figure 28-7  Air-conditioning vent in a small server closet

If things are really bad, you can enclose a system in a dust shield. Dust shields come complete with their own filters to keep a computer clean and happy even in the worst of environments.



EXAM TIP   Always use proper ventilation, air filters, and enclosures. To protect against airborne particles, consider wearing a protective mask.

Hazardous Materials
Offices are filled with chemicals and substances that pose health risks. Some of these risks are immediate—hazardous materials can burst into flames or damage your skin, lungs, and eyes. Others may cause cancer or other health conditions through regular exposure over many years. The CompTIA A+ 1102 objectives want you to know about compliance to government regulations that apply to working with these substances.

Regulations may sound intimidating, but the goal here is simple: people who work with or around dangerous substances deserve to know what the risks are, what precautions they should take, and what to do if there’s an accident. You’ll need to consult and comply with local regulations, but you should at least be familiar with the material safety data sheet (MSDS)—a document that details the risks, precautions, and clean-up/disposal procedures—for any substances you work with regularly and know how to find the MSDS if something you aren’t familiar with spills. For specific information on proper battery and toner disposal, and other device and asset disposal, take a look at Chapters 11 and 26.

Recycling E-Waste
Most U.S. cities have one or more environmental services centers that you can use to recycle electronic components. For your city, try a Google (or other search engine) search on the term “environmental services” and you’ll almost certainly find a convenient place for e-waste disposal.

Prohibited Content/Activity and Privacy, Licensing, and Policies
Organizations need policies and procedures in place to deal with negative events that affect their networks and systems—an incidence response. The larger the organization, the more detailed the incidence response, ranging from the team involved to the planning and steps in every contingency. This is a gigantic topic that is covered in more advanced certifications, such as CompTIA Security+. From a CompTIA A+ tech’s standpoint, you need to understand your role and what you should (and definitely should not) do when responding to an incident involving prohibited content or activity. This section explains how prohibited content, computer-related activity, and licensing can trigger negative events and also outlines the important steps to take in the unfortunate instance that such a negative event happens.

Try to stay away from any personal information on a PC. If you find something private (that isn’t illegal), ignore it and forget about it. If you find something illegal, you must follow the proper procedures. If a device you work on becomes evidence in legal proceedings, isolate the system and document everything that happens going forward. Pay special attention to the chain of custody or whoever is currently in control of the machine.

Data Classification
Larger organizations, such as government entities, benefit greatly from organizing their data according to its sensitivity—what’s called data classification—and making certain that computer hardware and software stay as uniform as possible. In addition, many government and internal regulations apply fairly rigorously to these organizations.

Data classification systems vary by the organization, but a common scheme classifies documents as public, internal use only, highly confidential, top secret, and so on. Using a classification scheme enables employees such as techs to know very quickly what to do with documents, the drives containing documents, and more. Your strategy for recycling a computer system left from a migrated user, for example, will differ a lot if the data on the drive was classified as internal use only or top secret.

Data classification goes hand in hand with data retention requirements, which dictate how long data needs to be kept by an organization, and is often related to how it has been classified. Customer data, security logs, and employee data, all can be covered under a company’s data retention requirements. After the pre-determined period of retention, data can be disposed of, but until then, it needs to be kept just as safely as data that is currently still in use.

Regulated Data
Regulated data is data that requires specific privacy and security safeguards as mandated by federal, state, or local laws or regulations or by industry standards or regulations. An organization’s technology policies must clearly address these privacy and security safeguards. There are four types of regulated data that IT departments must protect. Let’s look at each.

Credit Card Transactions
The Payment Card Industry Data Security Standard (PCI DSS) is a rigorous set of rules for securing systems that accept, transmit, process, or store credit/debit card payments.

Personally Identifiable Information
Personally identifiable information (PII) is a big umbrella term for any data that can lead back to a specific individual. Regulating and protecting PII will continue to be an issue for industries and government organizations for a long, long time. The General Data Protection Regulation (GDPR) is a fairly new law that defines a broad set of rights and protections for the personal information of citizens living in countries in the European Union. Consult your superiors about your organization’s policies for working with regulated data.

Laws protecting data have been developed so that organizations can create their own PII documentation for their employees to follow. The main premise behind these laws is that some information collected from individuals contains sensitive information that could easily identify who they are. Also, these regulatory laws specify that any PII data should be permanently deleted if there is no use for it. Never, in any circumstance, should PII be shared with anyone.

A sub-category of PII is personal government-issued information. Personal government-issued information consists of things like social security numbers, driver’s license or passport numbers, a birth certificate, all of which, unsurprisingly, are issued by the government. These documents and the information they contain are sensitive and can leave someone vulnerable to serious identity theft if they fall into the wrong hands, and special care must be taken to protect them.

Protected Healthcare Data
Protected health information (PHI), or simply healthcare data, is basically any data that involves a person’s health status, medical records, and healthcare services they have received. Like PII, PHI should never be shared unless given permission by the owner of that information.

Compliance
Compliance means that members of an organization must abide by or comply with all of the rules that apply to the organization. As we discussed earlier when we talked about standard operating procedures, the most common compliance issue revolves around software, such as what sort of software users are allowed to install on their computers. Compliance keeps technical support calls down and enables techs to focus on more serious problems—like an incident response.

Licensing, End-User License Agreement, and Digital Rights Management
Software licensing has many twists that can easily lead a user or a tech out of compliance. Like other creative acts, programmers are granted copyright to the software they create. The copyright owner then decides how he or she or it (the corporation) will license that software for others to use. Licenses can be for personal use or corporate use. They can also be valid licenses or non-expired licenses. Licenses can be closed source or open source. Each of these options has variations as well, so this gets complex. Let’s start at the top and work through the variations.

Personal Use License Versus Corporate Use License
For moral or philosophical reasons, some developers want their software to be free for some or all purposes. When Linus Torvalds created the Linux operating system, for example, he made it freely available for everyone. GIMP image-editing software likewise is available to download and use for free.

Personal use licenses have variations. Many personal use programs are “free” only for personal use. If you want to use the excellent TeamViewer remote access program at your office, for example, you need to buy a corporate license. But if you want to log in to your home machine from your personal laptop, you can use TeamViewer for free. When software is released under a corporate use license, you have a legal obligation to pay money for access to it—but a lot of variations apply. Traditionally, you bought a copy of a program and could use it forever, sell it to someone else, or give it away. You bought copies for each user with a personal use license, or multiple users with an enterprise license.

Today, the picture is muddier. You can buy the use of Microsoft Office, for example, as long as you pay a monthly or yearly fee. The personal use license enables you to share the software with several other people or accounts and use it on several of your personal machines.

License Validity and Expiration
Many software licenses come with strings attached, and as techs we must pay careful attention to them. For example, a license might say how many systems you can install it on, how many human users it can have, how many CPUs you can run it on, whether you’re allowed to use it for commercial purposes, whether someone who owns a valid license can transfer it to anyone else, which version(s) of the software the license is valid for, or even how long the license will remain valid.

A license is valid when your organization complies completely with these stipulations. Some programs that demand a license key may straight-up tell you if the license key itself is no longer valid—but confirmation that the license key is valid doesn’t mean you’re off the hook when it comes to complying with every last clause in the license. Some licenses stipulate that you can only use the software with a non-expired license. Other licenses permit you to keep using the installed version after the license has expired but cut off your access to updates and security patches until you renew the license.



EXAM TIP   At first glance, valid licenses and non-expired licenses seem to mean the same thing; however, it’s important to know the distinctions between the two for the 1102 exam, objective 4.6.

Open Source Licenses
Another huge variation in software use and licensing is what you can do with the source code of an application. Open source licenses generally allow you to take the original code and modify it. Some open source licenses require you to make the modified code available for free download; others don’t require that at all. Closed source licenses stipulate that you can’t modify the source code or make it part of some other software suite.

End-User License Agreements
The end-user license agreement (EULA) that you must accept to be able to proceed when opening or installing new software obligates you to abide by the use and sharing guidelines stipulated by the software copyright holder. When you agree to the EULA, in other words, you’re agreeing not to do things like make illegal copies of the software or attempt to reverse-engineer how it works. The EULA may also give the copyright holder permission to collect data on you and how you use the software and limit whether (or for how much) you can sue the copyright holder if it mangles your files or causes other problems.

Digital Rights Management
Software and media companies use various forms of digital rights management (DRM) technology to try to enforce their policies regarding when, where, and how we can use the software or access media such as video, music, and books. In short, DRM is one way the industry has tried to fight software and media piracy over the years. Many programs require activation over the Internet, for example, or a special account with the copyright holder. Some media files can only be opened by the provider’s official app.



NOTE   The key for a tech is to know the specific licenses paid for by the tech’s organization and ensure that the organization abides by those licenses. Using pirated software, exceeding the use limits set by a EULA, and using programs that aren’t licensed for commercial use in a corporate setting all expose your organization to lawsuits.

Incident Response
Organizations have incident response policies and procedures to deal with negative events. CompTIA A+ techs might be members of the incident response team. As such they need to understand first response actions, identification and reporting of incidents, and chain of custody. Let’s start by looking at first response actions.

First Response
First response means securing the area, determining the scope of the incident, and analyzing the impact the incident might have on the organization. If you’re part of the incident response team, your first response duties will be spelled out in detail in the incident response plan. Most likely, your team’s first action when something bad happens is to secure the area. Securing the area can mean physical lockdown—no one in or out—or other lockdown—no network traffic in or out of the affected section.

Incident Reporting
An incident report means telling your supervisor about the data you’ve gathered regarding a computer or network incident. This provides a record of what you’ve done and accomplished. It also provides information that, when combined with other information you may or may not know, could reveal a pattern or bigger problem to someone higher up the chain.

This can be accomplished with a documentation of incident. Many companies have pre-made forms that you simply fill out and submit. Other places are less formal. Regardless, you need to do this!

Tracking specific problems through incident reports documentation helps current and future techs deal with problematic hardware and individuals. If you have five identical color laser printers in five departments, for example, and one starts jamming regularly after 10,000 pages, documenting the problem—the incident—and the solution will point very clearly to the potential problems with the other four printers when they reach that same usage level.

Once you’ve gathered data about a particular system or dealt with a computer or network problem, what’s next?

Inform Management/Law Enforcement as Necessary
So, you have documented all of the necessary information needed about the incident. Now it’s time for you to make a decision. Is the incident at a low risk level and can be resolved at your level? Or, is it something that has escalated to a higher risk level where you need to inform your supervisor? Determine the scope of the incident (single system, whole group of users, and so on) and explore its seriousness and potential impact on the organization. Determining the scope of the incident can be accomplished by questioning users, reviewing log files, and so on. Your network and security people will handle possible impact scenarios and determine if the impact is serious enough to include law enforcement in the investigation.

Chain of Custody
When responding to an incident involving prohibited content or activity, there must be an end-to-end process for identifying who owns what, where it is, and who is liable for it. It asks and answers, “Whose responsibility is this?” when assets, digital or physical, transfer hands in an organization. For example, who is in charge and liable for data integrity (ensuring that the data is in its original and uncorrupted form) and data preservation (ensuring that the data is backed up and kept available)? Where is the data stored (i.e., drive, server)? This process, called the chain of custody, begins when the evidence is initially seized or collected and establishes a continuous accounting of where the evidence is at all times, who has possessed it, what activities were performed on it, and the details of its storage, use, and transfer. This process helps to ensure the integrity of evidence and minimizes the possibility that it has been altered or tampered with. Chain of custody contributes to the admissibility and value of evidence in court.

Beyond A+
Whew! You’ve just finished a book that covers everything you need to know to take and pass the CompTIA A+ 1101/1102 exams. Congratulations! What’s next?

First, go back to the Introduction and review the study chart and guidelines. Review, review, review! Take the practice exams and look for exam sources online to get even more scoop on the types of questions you’ll see.

Second, schedule your exams if you haven’t already done so (pressure and diamonds and all that). Having that endpoint in sight helps focus.

Go back to my original question once you’ve taken and passed both CompTIA A+ exams: What’s next? The two logical steps are to start studying for CompTIA Network+ and CompTIA Security+. These complete CompTIA’s Core curriculum and round out tech skills needed for today’s interconnected and security-heightened world. There are a lot of great writers and videographers out there who have excellent materials on CompTIA Network+ and Security+ (including me), so you won’t find it hard to get study materials.

Good luck, my friend, and keep in touch!



Chapter Review
Questions
1.   Henry gets a help desk call from Arthur in accounting who reports that his keyboard is not working. This seems like a familiar problem, one that another tech mentioned a short time back. Where should Henry look to find information on the problem?

A.   Change documentation

B.   Incident reports

C.   Asset management documentation

D.   Risk management documentation

2.   Annie wants to mark several Mac laptops issued to salespeople so that she can set up a scanner at the office door to track each time the laptops enter and leave the building. What will help her accomplish this goal?

A.   Add a barcode sticker to each laptop.

B.   Add an RFID tag to each laptop.

C.   Submit a change document to the change board.

D.   It can’t be done, because the laptops run macOS.

3.   Joan has proposed upgrading the inkjet printers in the marketing department with color laser printers. The purpose of the change is to reduce the cost per page printed, because toner is less expensive than ink and the duty cycle of laser printers is longer than that of inkjet printers. The marketing department currently has three inkjet printers. What’s her logical next step?

A.   She should complete the scope of change part of the change document to factor in the price of the printers.

B.   She should perform a risk analysis to determine any potentially negative consequences.

C.   She should download the documentation on the new printers and begin the education process for the marketing department on how to use them.

D.   She should contact the change board with her initial proposal.

4.   Once the change board has reviewed and approved Joan’s plan for the new printers, what’s her next step?

A.   Create a rollback plan in case the quality of print with the laser printers isn’t sufficient for the marketing materials.

B.   Test the rollback plan.

C.   Finalize the change documentation.

D.   Implement the change plan.

5.   What broad term describes the process of creating a road map for current and future techs to make changes or repairs over time for an organization?

A.   Change documentation

B.   Change management

C.   Management documentation

D.   Network documentation

6.   What broad term describes the process of enabling organizations to implement changes to IT infrastructure in a safe and cost-effective manner?

A.   Change documentation

B.   Change management

C.   Management documentation

D.   Network documentation

7.   As part of the change-management process, educating users on new systems is an important component in which of the following?

A.   Rollback plan

B.   Accessibility training

C.   End-user acceptance

D.   Risk analysis

8.   Which of the following is an example of an environmental control?

A.   HVAC system

B.   Temperature and humidity

C.   Surge protector

D.   Fire extinguisher

9.   Which of the following is a detailed assessment of possible problems that could result from change?

A.   Acceptable use policy

B.   New-user setup checklist

C.   Regulatory requirements

D.   Risk analysis

10.   What does an IT department use for a departing employee to ensure that all equipment has been returned, access has been removed, and, where possible, knowledge transfer has been facilitated?

A.   End-user termination checklist

B.   New-user setup checklist

C.   Network topology diagram

D.   Acceptable use policy

Answers
1.   B. Henry should check the incident reports to see if there’s a history of problems with the computer at that workstation.

2.   B. Annie should add a radio frequency identification (RFID) tag to each laptop and install a scanner at the door to track when the laptops are taken out of the office and returned.

3.   A. Joan hasn’t finished the scope of change yet, so she should include the price of the printers.

4.   A. Once the change board has approved the change plan, Joan should make sure to have a good rollback plan in place in case something unforeseen and negative happens.

5.   D. The term network documentation describes the road map for current and future techs to make changes or repairs over time for the organization.

6.   B. The term change management describes the process organizations use to implement changes to IT infrastructure in a safe and cost-effective manner.

7.   C. Training users in new or updated systems leads to end-user acceptance of the changes.

8.   A. An HVAC system is an example of an environmental control.

9.   D. A risk analysis is a detailed assessment of possible problems that could result from change.

10.   A. When an employee parts ways with an organization, the IT department uses an end-user termination checklist to ensure that the employee has returned all equipment, that their access has been removed, and, where possible, knowledge transfer has been facilitated.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Appendix B About the Online Content
Glossary
Index
42h 21m remaining
GLOSSARY  
100BASE-T  Ethernet cabling system designed to run at 100 Mbps on twisted pair cabling. Also called Fast Ethernet.

1000BASE-T  Ethernet cabling system designed to run at 1000 Mbps on twisted pair cabling. Also called Gigabit Ethernet.

1000BASE-TX  Similar to 1000BASE-T but uses two pairs of wires rather than four. Not as commonly used as 1000BASE-T.

10GBASE-T  Ethernet standard that supports speeds of up to 10 Gbps and is common on server-to-server connections. Requires Cat 6 or better twisted pair or fiber optic cabling.

2-in-1  Portable devices that serve as both a laptop and a tablet.

3G  Third-generation cellular data technologies (such as EV-DO, UTMS, HSPA+, and HSDPA) with real-world speeds under 10 Mbps.

4G  Fourth-generation cellular data technologies. Most popularly implemented as Long Term Evolution (LTE), a wireless data standard with theoretical download speeds of 1 Gbps and upload speeds of 100 Mbps.

5G  Fifth-generation cellular data technologies, launched in 2019. Their specifications call for up to 20 Gbps, but real-world speeds are often less and can vary depending on the carrier and location.

64-bit processing  A type of processing that can run a compatible 64-bit operating system, such as Windows 10 and 11, and 64-bit applications. 64-bit PCs have a 64-bit-wide address bus, enabling them to use more than 4 GB of RAM.

802.11a  Wireless networking standard that operates in the 5-GHz band with a theoretical maximum throughput of 54 Mbps.

802.11ac  Wireless networking standard that operates in the 5-GHz band and uses multiple in/multiple out (MIMO) and multi-user MIMO (MU-MIMO) to achieve a theoretical maximum throughput of 1+ Gbps.

802.11ax  Wireless networking standard that operates in the 2.4-, 5-, and 6-GHz bands. Also known as high-efficiency wireless, it introduces improvements that optimize congested networks and reduce power use on client devices. The main improvement is the introduction of the 6-GHz band, which supports more channels, is less saturated, and suffers less interference. Also known as Wi-Fi 6 or Wi-Fi 6E (if it supports the 6-GHz band).

802.11b  Wireless networking standard that operates in the 2.4-GHz band with a theoretical maximum throughput of 11 Mbps.

802.11g  Wireless networking standard that operates in the 2.4-GHz band with a theoretical maximum throughput of 54 Mbps and is backward compatible with 802.11b.

802.11n  Wireless networking standard that can operate in both the 2.4-GHz and (optionally) 5-GHz bands and uses multiple in/multiple out (MIMO) to achieve a theoretical maximum throughput of 100+ Mbps.

AC (alternating current)  Type of electricity in which the flow of electrons alternates direction, back and forth, in a circuit.

acceptable use policy (AUP)  Defines what actions employees may or may not perform on company equipment, including computers, phones, printers, and even the network itself. This policy defines the handling of passwords, e-mail, and many other issues.

access control list (ACL)  A clearly defined list of permissions that specifies what actions an authenticated user may perform on a shared resource.

access control vestibule  Small room with a set of doors—one to the unsecured area and one to a secured area. Only one door can open at a time, and individuals must authenticate to continue through the door to the secured area. Combats tailgating. Also commonly known as a mantrap.

access point  See WAP.

Accounts (Windows Settings)  Windows Settings category that includes e-mail and account options.

activation (software)  Process of confirming that an installed copy of a Microsoft product (most commonly Windows or a Microsoft Office application) is legitimate. Usually done at the end of software installation.

active partition  On a hard drive, the primary partition that contains an operating system.

actively listen  Part of respectful communication involving listening and taking notes without interrupting.

activity light  An LED on a NIC, hub, or switch that blinks rapidly to show data transfers over the network.

Address Resolution Protocol (ARP)  Protocol in the TCP/IP suite used with the command-line utility of the same name (arp) to determine the MAC address that corresponds to a particular IP address

administrative shares  Administrator tool to give local admins access to hard drives and system root folders.

Administrative Tools  Group of Control Panel applets, including Computer Management, Event Viewer, Performance Monitor, and Task Scheduler.

administrator account  User account, created when the OS is first installed, that is allowed complete, unfettered access to the system without restriction.

administrator password  Credentials for the system administrator account.

Administrators group  List of members with complete administrator privileges.

ADSL (asymmetric digital subscriber line)  Fully digital, dedicated connection to the telephone system that provides average download speeds of 3–15 Mbps and upload speeds of 384 Kbps to 1.5 Mbps. Asymmetric identifies that upload and download speeds are different, with download usually being significantly faster than upload.

Advanced Encryption Standard (AES)  A block cipher created in the late 1990s that uses a 128-bit block size and a 128-, 192-, or 256-bit key size. Practically uncrackable.

Advanced Micro Devices (AMD)  See AMD.

AirDrop  Apple feature for its various operating systems that enables easy wireless sharing of files between Apple devices.

algorithm  Set of rules for solving a problem in a given number of steps.

AMD (Advanced Micro Devices)  CPU and chipset manufacturer that competes with Intel. Produces FX, A-Series, Ryzen, and Opteron CPUs and APUs. Also produces video card processors (GPUs) under its Radeon brand.

amperage  See current.

amperes (amps or A)  Unit of measure for amperage, or electrical current.

analog  Device that uses a physical quantity, such as length or voltage, to represent the value of a number. By contrast, digital storage relies on a coding system of numeric units.

Android application package (APK)  Installation software for Android apps.

ANSI/TIA  A major telecommunication standards agency. The Telecommunication Industry Association (TIA) establishes the UTP categories under the ANSI/TIA 568 specification. The American National Standards Institute (ANSI) accredits TIA standards to ensure compatibility of industry and international standards. See also UTP.

anti-malware program  Software designed to identify and block or remove malware. Typically powered by frequently updated definition files containing the signatures of known malware.

antistatic bag  Bag made of antistatic plastic into which electronics are placed for temporary or long-term storage. Used to protect components from electrostatic discharge.

antistatic mat  Special surface on which to lay electronics to prevent electrostatic discharge. Includes a grounding connection designed to equalize electrical potential between a workbench and one or more electronic devices.

antistatic wrist strap  Special device worn around the wrist to prevent electrostatic discharge. Includes a grounding connection designed to equalize electrical potential between a technician and an electronic device.

antivirus program  Software designed to combat viruses by either seeking out and destroying them or passively guarding against them. Typically, it is frequently updated with new definition files to enable up-to-date protection from newly discovered viruses.

API (application programming interface)  Enables computer programs to “talk” to each other. Unlike a user interface, an API is not visible to the user. Documented APIs enable one vendor to create software that can communicate with another vendor’s software.

APIPA (Automatic Private IP Addressing)  Feature of Windows that automatically assigns an IP address to the system when the client cannot obtain an IP address automatically. See also zeroconf.

App Store  Apple’s mobile software storefront, where you can purchase apps for your smartphone, tablet, and other Apple products.

Apple File System (APFS)  Apple’s proprietary file system, introduced to replace the older HFS+.

applet  Generic term for a program in the Windows Control Panel.

application manager  Mobile device interface for removing and managing apps running on the device.

application programming interface  See API.

application spoofing  The act of disguising a malicious mobile app as a legitimate one for the purpose of infecting a target device with malware or stealing credentials like passwords.

application virtualization  Process that virtualizes OS capabilities that an application would normally use to install and do its work. Enables the use of an application without actually installing it, running an application that only works on an older OS version, or even running an application that only works on a different OS.

Applications  Tab in Task Manager that lists running applications.

Apps (Windows Settings)  Windows settings category that enables you to list, view, manage autostart, and uninstall apps.

Apps & features  Area of the Windows 10 Settings Apps category that enables users to add and remove programs and Windows features.

apt-get  Linux command for installing or updating a program using the advanced packaging tool.

ARM (Advanced RISC Machine)  Energy-efficient processor design frequently used in mobile devices and also used by the latest macOS computers using the M1 and M2 processors.

ARP  See Address Resolution Protocol.

aspect ratio  Ratio of width to height of a display. Wide-screen displays such as modern TVs, desktop computer monitors, portable computer displays, and even smartphones commonly use 16:9 or 16:10, although you can find devices with many other aspect ratios.

assertive communication  Means of communication that is not pushy or bossy but is also not soft. Useful in dealing with upset customers as it both defuses their anger and gives them confidence that you know what you’re doing.

asset tag  Inventory tracking tags (which may be simple barcodes or use wireless networking protocols such as RFID) that help an organization track items such as equipment.

attack vector  The route or methods used by a given attack (including malware).

attributes  Values in a file that determine the hidden, read-only, system, and archive status of the file.

ATX (Advanced Technology Extended)  Popular motherboard form factor that generally replaced the AT form factor.

audio jack  Very popular connector used to transmit two audio signals; perfect for stereo sound. Confusingly, you can find the diameter described as both 1/8 inch and 3.5 mm.

AUP  See acceptable use policy.

authentication  The process of identifying and granting access to some user trying to access a system.

authorization  The process that defines which resources an authenticated user may access and what the user may do with those resources.

AutoPlay  A Windows feature that opens a dialog box when removable media is inserted into the computer, providing options based on what Windows finds on the drive, including starting the Autorun application.

Autorun  A feature that enables Windows to look for and read a file called autorun.inf immediately after a removable media device (optical disc or thumb drive) is inserted and automatically run whatever program the file lists.

Backup and Restore  Windows 7’s backup utility. It offers two options: create a backup or restore from a backup. Windows 10 still supports making and restoring these backups, which it calls Backup and Restore (Windows 7). See also File History.

backup testing  The process of ensuring that file or system backups have produced backups from which you can restore usable systems and files.

badge reader  See smart card reader.

bandwidth  The capacity of a network to transmit a given amount of data during a given period.

bash  Default command shell on macOS and most Linux distributions. See shell.

basic disk  Hard drive partitioned in the “classic” way with a master boot record (MBR) and partition table. See also dynamic disks.

battery health  The amount of charge a battery can hold. Decreases over time as the battery is charged and discharged.

battery life  The length of time a battery can be used before needing to be recharged.

binary numbers  Number system with a base of 2, unlike the number systems most of us use that have bases of 10 (decimal numbers), 12 (measurement in feet and inches), and 60 (time). Binary numbers are preferred for computers for precision and economy. An electronic circuit that can detect the difference between two states (on–off, 0–1) is easier and more inexpensive to build than one that could detect the differences among ten states (0–9).

biometric authentication  Authentication process using biometric data such as voice, fingerprints, or retinal scans.

biometric scanner  Hardware device used to support authentication; works by scanning and remembering a unique aspect of a user’s body part (e.g., retina, iris, face, or fingerprint) by using some form of sensing device such as a retinal scanner.

BIOS (basic input/output services) (basic input/output system)  Classically, software routines burned onto the system ROM of a PC. More commonly seen as firmware that directly controls a particular piece of hardware. This firmware handles startup operations and low-level control of hardware such as disk drives, the keyboard, and monitor.

bit  Single binary digit. Also, any device that can be in an on or off state.

BitLocker Drive Encryption  Drive encryption software offered in high-end versions of Windows. BitLocker requires a special chip to validate hardware status and to ensure that the computer hasn’t been hacked.

Bluetooth  Wireless technology designed to create small wireless networks preconfigured to do specific jobs, but not meant to replace full-function networks or Wi-Fi.

Blue Screen of Death (BSoD)  Infamous error screen that appears when Windows encounters an unrecoverable error. This is an example of a proprietary crash screen.

bollard  Short post made of metal, concrete, or another solid material used to prevent vehicles from entering or driving onto an area. Often used to protect pedestrian areas or deny vehicles from getting too close to a secure area.

boot  To initiate an automatic routine that clears the memory, loads the operating system, and prepares the computer for use. Term is derived from “pull yourself up by your bootstraps.” Necessary because RAM doesn’t retain program instructions when power is turned off.

boot method  Media a computer uses to initiate the booting process. Includes optical media, removable drives, or a networked location. For the related CMOS setting, see boot sequence.

boot options  Settings in the system setup program that define which devices the system will attempt to boot from (and in what order).

boot sector  First sector on a storage drive. The boot-up software in ROM tells the computer to load whatever program is found there. If a system disk is read, the program in the boot record directs the computer to the root directory to load the operating system.

bootable disk  Any storage device with a self-starting operating system.

bootleg application  Fake application designed to trick users into installing it. See also application spoofing.

bootmgr  Windows Boot Manager. Manages the boot process using information from the Boot Configuration Data (BCD) file.

bootrec  A Windows Recovery Environment troubleshooting and repair tool that repairs the master boot record, boot sector, or BCD store.

botnet  Network of computers infected with malware that can be controlled to do the bidding of the malware developers, or anyone who pays them. A common use is carrying out distributed denial of service (DDoS) attacks.

broadband  Commonly understood as a reference to high-speed, always-on communication links that can move large files much more quickly than a regular phone line.

broadcast  A network transmission addressed for every node on the network.

broadcast domain  Group of computers connected by one or more switches––that is, a group of computers that receive broadcast frames from each other.

browser  Program specifically designed to retrieve, interpret, and display Web pages.

brute-force attack  Simple attack that attempts to guess credentials or identify vulnerabilities by trying many possibilities.

BSoD  See Blue Screen of Death.

bug  Programming error that causes a program or a computer system to perform erratically, produce incorrect results, or crash. The term was coined when a real bug was found in one of the circuits of one of the first ENIAC computers.

bus  Series of wires connecting two or more separate electronic devices, enabling those devices to communicate. Also, a network topology where computers all connect to a main line called a bus cable.

BYOD (bring your own device)  An organizational policy that permits employees to use their own phones or other mobile devices instead of company-issued ones.

byte  Unit of 8 bits; fundamental data unit of personal computers. Storing the equivalent of one character, the byte is also the basic unit of measurement for computer storage.

cable Internet  Fast Internet connection from a cable TV provider via RG-6 or RG-59 cable and a cable modem.

cable lock  Simple anti-theft device for securing a laptop to a nearby object.

cable modem  Device that enables Internet connection over existing coaxial cable television infrastructure by translating signals into a form that networked devices can understand.

cable tester  Device for verifying that the connectors and wires in a cable (such as UTP) are in good order.

cache (disk)  Special area of RAM that stores the data most frequently accessed from the hard drive. Cache memory can optimize the use of your systems.

cache (L1, L2, L3, etc.)  Special section of fast memory, usually built into the CPU, used by the onboard logic to store information most frequently accessed by the CPU.

calibration  Process of matching the print output of a printer to the visual output of a monitor.

card reader  Device with which you can read data from one of several types of flash memory.

Cat 5  Category 5 wire; an ANSI/TIA standard for UTP wiring that can operate at up to 100 Mbps.

Cat 5e  Category 5e wire; ANSI/TIA standard for UTP wiring that can operate at up to 1 Gbps.

Cat 6  Category 6 wire; ANSI/TIA standard for UTP wiring that can operate at up to 10 Gbps.

Cat 6a  Category 6a wire; augmented Cat 6 UTP wiring that supports 10-Gbps networks at the full 100-meter distance between a node and a switch.

Cat 7  Supports 10-Gbps networks at 100-meter segments; shielding for individual wire pairs reduces crosstalk and noise problems. Cat 7 is not an ANSI/TIA standard.

catastrophic failure  A failure in which a component or whole system will not boot; usually related to a manufacturing defect of a component. Could also be caused by overheating and physical damage to computer components.

cd  Command-line utility for changing the focus of the command prompt from one directory to another. Shorthand for “change directory.”

cellular location services  Mobile device feature that can detect the device’s location, enabling apps to request and use this information to provide location-aware services, such as finding nearby restaurants.

certificate authority (CA)  Trusted entity that signs digital certificates to guarantee that the certificate was signed by the Web site in question (and not forged).

chain of custody  A documented history of who has been in possession of a system or component.

change board  A group of representatives from around the organization who review and approve change proposals.

change documentation  Collected documentation for all aspects of a change process, including plans leading up to the change as well as receipts, overtime documents, an inventory of changed systems, a list of created users, and signed end-user acceptance forms.

change management  A well-defined process composed of many planning and execution steps that enables organizations to change their IT infrastructure in a safe, cost-effective manner.

checksum  Value generated from some data, like a file, and saved for comparing to other checksums later. Can be used to identify identical data, such as files on a user’s system that match known viruses. Checksums can also be used to monitor whether a program is changing itself over time, which is a strong warning sign that it may be malware that evolves to avoid detection.

chipset  Electronic chips, specially designed to work together, that handle all of the low-level functions of a PC. In the original PC, the chipset consisted of close to 30 different chips. For most of the 1990s and 2000s, chipsets usually consisted of one, two, or three separate chips embedded into a motherboard. Today’s CPUs have controllers built in, such as the memory and display controllers. Almost all chipsets are now a single chip.

chkdsk (checkdisk)  Hard drive error detection and, to a certain extent, correction utility in Windows, launched from the command-line interface. Originally a DOS command (chkdsk.exe); also the executable for the graphical Error checking tool.

chmod  Linux command used to change user and group permissions for a file.

chown  Linux command used to change ownership over a directory or file.

Chrome OS  Google’s Linux-based operating system designed to connect users via the Internet into Google applications, such as Gmail, Google Docs, and more. Chrome OS comes preinstalled on purpose-built hardware such as the Chromebook portable computers.

Chromebook  Strictly, any portable computer running Google’s Chrome OS. Chromebooks offer an experience focused on Web applications by making use of virtually unlimited data storage in the cloud and Software as a Service (SaaS) applications available over the Web. Because they offload so much work, Chromebooks have a reputation for being cheap and light, but premium Chromebooks are increasingly common.

Classless Inter-Domain Routing (CIDR)  Current system for creating and notating IPv4 subnets; replaced the older, less flexible three-class system.

clean installation  Installing an operating system on a fresh drive, following a reformat of that drive. Often it’s the only way to correct a problem with a system when many of the crucial operating system files have become corrupted.

clearing cache  The process of clearing stored app or browser settings in order to resolve performance issues. Commonly used to resolve issues with Web browsers or to free up resources on mobile devices.

client  Computer program that uses the services of another computer program. Also, software that extracts information from a server; a Web browser is a client, and the Web site that it accesses is the server. Also, a machine that accesses shared resources on a server.

client/server  Relationship in which client software obtains services from a server on behalf of a person.

client-side virtualization  Using a hypervisor installed on a client machine to run a virtual machine. The VM may be created and stored on the client machine or accessed over the network.

clock cycle  Single charge to the clock wire (CLK) of a CPU, informing the CPU that another piece of information is waiting to be processed.

clock speed  The maximum number of clock cycles that a CPU can handle in a given period of time, measured in MHz or GHz. In modern CPUs, the internal speed is a multiple of the external speed. See also clock-multiplying CPU.

clock-multiplying CPU  CPU that takes the incoming clock signal and multiples it inside the CPU to let the internal circuitry of the CPU run faster.

cloud computing  A model for enabling and accessing computing storage and other shared (or not shared) resources on demand. The “cloud” is based on servicing models that include, among others, Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS), as well as hybrid mixtures of these services.

CMOS (complementary metal-oxide semiconductor)  Defunct technology used in earlier computer systems that hooked up a small amount of RAM to a small battery to hold system settings for the BIOS firmware even with the computer off. This has long since been incorporated into the chipset. CMOS is often informally used to refer to the CMOS setup program or system setup utility.

CMOS battery  A coin cell lithium-ion battery that maintains power to the CMOS memory chip when the computer is otherwise unpowered. The usual battery size is CR2032.

CMOS clear  A jumper setting or button on the motherboard that, when set, will revert CMOS settings to the factory defaults. Sometimes labeled CLRTC on the motherboard.

CMOS setup program  Program enabling you to access and update CMOS data. Also referred to as the system setup utility, BIOS setup utility, UEFI/BIOS setup, and similar names.

coaxial cable  Cabling in which an internal conductor is surrounded by another, outer conductor, thus sharing the same axis.

code  Set of symbols representing characters (e.g., ASCII code) or instructions in a computer program (a programmer writes source code, which must be translated into executable or machine code for the computer to use).

code-division multiple access (CDMA)  Wireless data standard for mobile devices.

color depth (display)  The number of bits (the bit depth) necessary to represent the number of colors in a graphics mode. Common color bit depths are 16-bit and 32-bit, representing 65,536 colors and 16.7 million colors (plus an 8-bit alpha channel for transparency levels), respectively.

command  A request, typed from a terminal or embedded in a file, to perform an operation or to execute a particular program.

command prompt  Text prompt for entering commands.

command-line interface (CLI)  Text user interface. Users input text commands and receive text output. CLI commands, which are more flexible and often faster (or use fewer resources) than a graphical equivalent, are also easy to compose into scripts for performing frequent tasks.

community cloud  Cloud network that serves a community or group with shared needs and interests, such as hospitals or defense contractors.

compatibility modes  Feature of Windows to enable software written for previous versions of Windows to operate in newer versions.

compliance  Concept that members of an organization must abide by the rules created by and applying to that organization (including government regulations). For a technician, compliance often defines what software can or cannot be installed on an organization’s computers.

component failure  Occurs when a system device fails due to a manufacturing defect or some other type of defect.

compression  Process of squeezing data to eliminate redundancies, allowing files to use less space when stored or transmitted.

Computer Management  Applet in Windows’ Administrative Tools that contains several useful snap-ins, such as Device Manager and Disk Management.

connector  Small receptacle used to attach a cable to a device or system. Common types of connectors include USB, PS/2, RJ-45, VGA, HDMI, DVI, HD15, DisplayPort, and Thunderbolt.

consumables  Materials used up by printers, including paper, ink, ribbons, 3-D printer filament, and toner cartridges.

container file  A file that contains multiple data streams, such as a ZIP archive file or an MP4 movie file. Also called a wrapper.

context menu  Small menu brought up by right-clicking on objects in Windows.

contrast ratio  Difference in intensity between the lightest and the darkest spot that a device can display (in the case of a monitor) or capture (in the case of a camera or scanner).

Control Panel  Collection of Windows applets, or small programs, that can be used to configure various pieces of hardware and software in a system.

controller card  Card adapter that connects devices, such as a drive, to the main computer bus/motherboard.

copy command  Command-line tool used to make a copy of a file and paste it in another location.

counter  Used to track data about a particular object when using Performance Monitor.

cp  Copy command in Linux.

CPU (central processing unit)  “Brain” of the computer. Microprocessor that handles primary calculations for the computer. CPUs are known by names such as Core i7 and Ryzen.

CRC  See cyclic redundancy check.

credit card reader  Device that can be attached to mobile phones and tablets to take credit card payments.

crimper  A specialized tool for connecting network cables to a connector, such as twisted pair wires to an RJ-45 connector or coaxial cable to an RG-6 connector. Also called a crimping tool.

cross-site scripting (XSS)  An attack in which the attacker injects malicious code into a Web app in order to trick it into sending things that it shouldn’t to other users of the Web app.

cryptominer  A form of malware that enlists the hardware of the target system to mine cryptocurrency without the knowledge of the system’s owner.

CSMA/CA (carrier sense multiple access/collision avoidance)  Networking scheme used by wireless devices to transmit data while avoiding data collisions, which wireless nodes have difficulty detecting.

CSMA/CD (carrier sense multiple access/collision detection)  Networking scheme used by Ethernet devices to transmit data and resend data after detection of data collisions.

current  Amount of electrons moving past a certain point on a wire, measured in units called amperes. Also called amperage.

cyclic redundancy check (CRC)  Very accurate mathematical method used to check for errors in long streams of transmitted data. Before data is sent, the main computer uses the data to calculate a CRC value from the data’s contents. If the receiver calculates from the received data a different CRC value, the data was corrupted during transmission and is re-sent. Ethernet packets use the CRC algorithm in the FCS portion of the frame.

DAC  See discretionary access control.

data classification  System of organizing data according to its sensitivity. Common classifications include public, highly confidential, and top secret.

Data Collector Sets  Windows log repository that accepts log entries from other Windows computers.

data roaming  A feature of cellular data systems that enables the signal to jump from cell tower to cell tower and from your provider to another provider without obvious notice.

data storage  Saving a permanent copy of your work so that you can come back to it later.

data usage cap  Restrictions on how much data a user may consume. Once the user exceeds the limit, data may be blocked entirely or bandwidth may be throttled.

database system  A representation of the relationship between two or more objects. Often used in asset management to keep track of who has possession of various assets and why they have them.

DB-9  A two-row DB connector (male) used to connect the computer’s serial port to a serial-communication device such as a modem or a console port on a managed switch.

DC (direct current)  Type of electricity in which the flow of electrons is in a complete circle in one direction.

DDoS (distributed denial of service)  An attack on a computer or network device in which multiple computers send data and requests to the device in an attempt to overwhelm it so that it cannot perform normal operations.

DDR3 SDRAM  Type of SDRAM that sends 8 bits of data in every clock cycle.

DDR4 SDRAM  Type of SDRAM that offers higher density and lower voltages than DDR3 and can handle faster data transfer rates. Maximum theoretical capacity of DDR4 DIMMs is up to 512 GB.

DDR5 SDRAM  The successor to DDR4, offering doubled bandwidth, decreased power consumption, quadrupled DIMM capacity, and up to 7200 MT/s at the time of writing.

DE (desktop environment)  Name for the various user interfaces found in Linux distributions.

debug  To detect, trace, and eliminate errors in computer programs.

decrypt  To pass decryption keys and encrypted data through the appropriate decryption algorithm in order to retrieve the original unencrypted data. See encryption.

dedicated server  Machine that is not used for any client functions, only server functions.

default gateway  In a TCP/IP network, the nearest router to a particular host. This router’s IP address is part of the necessary TCP/IP configuration for communicating with multiple networks using IP.

default user accounts/groups  Users or groups that are enabled by default. Some, such as the guest account, represent a security risk.

definition file  List of malware signatures that enables anti-malware programs to identify malware on your system and clean them. This file should be updated often. Also called a signature file.

defragmentation (defrag)  Procedure in which all the files on a hard disk drive are rewritten on disk so that all parts of each file reside in contiguous clusters. The result is an improvement in disk speed during retrieval operations.

degaussing  Data destruction procedure used to reduce or remove the electromagnetic fields that store data on magnetic hard drives.

del (erase)  Command-line tool used to delete/erase files.

denial of service  See DoS.

Desktop  User’s primary interface to the Windows operating system.

desktop virtualization  A traditional desktop operating system installed in a VM. See also virtual machine.

device charger  Plugs into a power source and charges a device through one of its ports, such as USB or Lightning. Convenient for charging while the device stays on.

device driver  Program used by the operating system to control communications between the computer and peripherals.

device encryption  Enhances mobile device security by encrypting the device’s internal storage.

Device Manager  Utility that enables techs to examine and configure all the hardware and drivers in a Windows PC. It is both an MMC snap-in and a Windows 10 Control Panel utility.

Devices (Windows Settings)  Windows Settings category that enables users to make changes to attached devices such as printers, scanners, keyboard, and mouse.

DFS (distributed file system)  A storage environment where shared files are accessed from storage devices within multiple servers, clients, and peer hosts.

DHCP  See Dynamic Host Configuration Protocol.

diagnostics menu  Hidden mobile device menu that contains tests and diagnostics for verifying the functionality of various device hardware.

dictionary attack  Type of brute-force attack using a dictionary to guess things like usernames and passwords. Don’t think Webster’s—these dictionaries may be full of usernames and passwords that have leaked or been used as defaults over the years.

dig  Linux command that queries DNS to enable troubleshooting and monitoring.

digital certificate  Form in which a public key is sent from a Web server to a Web browser so that the browser can decrypt the data sent by the server.

digital rights management (DRM)  Code schemes for enforcing what users can and can’t do with commercial software or digital media files.

digitizer  The touchscreen overlay technology that converts finger and stylus contact into input data for the device to use.

dilithium crystal  Controlling agent in a faster-than-light warp drive.

DIMM (dual inline memory module)  32- or 64-bit type of DRAM packaging with the distinction that each side of each tab inserted into the system performs a separate function. DIMMs come in a variety of sizes, with 184-, 240-, and 288-pin being the most common on desktop computers.

dipole antenna  Standard straight-wire antenna that provides the most omnidirectional function.

dir  Command-line tool used to display the entire contents of the current working directory.

direct burial  Rating applied to shielded twisted pair (STP) cabling that indicates a thicker jacket and some form of waterproofing for use outdoors or underground.

direct LED backlighting  Matrix of LEDs that illuminates a display from directly behind the display panel.

directory  Another name for a folder.

discretionary access control (DAC)  Authorization method based on the idea that there is an owner of a resource who may at his or her discretion assign access to that resource. DAC is considered much more flexible than mandatory access control (MAC).

Disk Cleanup (cleanmgre.exe)  Utility built into Windows that can help users clean up their hard drives by removing temporary Internet files, deleting unused program files, and more.

Disk Defragmenter (dfrgui.exe)  A program that maintains performance by rearranging chunks of data on a storage device to ensure chunks that comprise a file are stored contiguously. Filename is dfrgui.exe. Renamed to Optimize Drives in Windows 8 and up.

disk duplexing  Type of disk mirroring using two separate controllers rather than one; marginally faster than traditional mirroring because one controller does not write each piece of data twice.

disk initialization  A process that places special information on every hard drive installed in a Windows system.

Disk Management (dismgmt.msc)  Snap-in available with the Microsoft Management Console that enables techs to configure the various disks installed in a system; available in Computer Management | Administrative Tools.

disk mirroring  Process by which data is written simultaneously to two or more disk drives. Read and write speed is decreased, but redundancy in case of catastrophe is increased.

disk quota  Application allowing network administrators to limit hard drive space usage.

disk striping  Process by which data is spread among multiple (at least two) drives. Increases speed for both reads and writes of data. Considered RAID level 0 because it does not provide fault tolerance.

disk striping with parity  Method for providing fault tolerance by writing data across multiple drives and then including an additional drive, called a parity drive, that stores information to rebuild the data contained on the other drives. Requires at least three physical disks: two for the data and a third for the parity drive. This provides data redundancy at RAID levels 5, 10, and 0+1 with different options.

disk thrashing  Hard drive that is constantly being accessed due to lack of available system memory. When system memory runs low, a Windows system will utilize hard disk space as “virtual” memory, thus causing an unusual amount of hard drive access.

Disk Utility  macOS tool that checks for hard drive errors.

display adapter  Handles all the communication between the CPU and the monitor. Also known as a video card or graphics card.

Display Settings  Windows utility that enables a user to change color schemes, font sizes, and other aspects of what appears on the computer monitor.

DisplayPort  Digital video connector used by some Apple Mac desktop models and some PCs, notably from Dell. Designed by VESA as a royalty-free connector to replace VGA and DVI.

distended capacitors  Failed capacitors on a motherboard, which tend to bulge out at the top. This was especially a problem during the mid-2000s, when capacitor manufacturers released huge batches of bad capacitors.

distributed denial of service  See DDoS.

distribution (distro)  A specific variant of Linux.

DLP (Data Loss Prevention)  System or set of rules designed to stop leakage of sensitive information. Usually applied to Internet appliances to monitor outgoing network traffic.

DMZ  See screened subnet.

DNS (Domain Name Service)  TCP/IP name resolution system that translates a host name into an IP address. Uses UDP port 53.

DNS domain  Specific branch of the DNS name space. Top-level domains (TLDs) include .com, .gov, and .edu.

docking station  Device that provides a portable computer extra features such as an optical drive, in addition to legacy and modern ports. Similar to a port replicator. Also, a charging station for mobile devices.

document the findings, actions, and outcomes  Recording each troubleshooting job: what the problem was, how it was fixed, and other helpful information. (Step 6 of 6 in the CompTIA troubleshooting methodology.)

domain  Groupings of users, computers, or networks. In Microsoft networking, a domain is a group of computers and users that share a common account database and a common security policy. On the Internet, a domain is a group of computers that share a common element in their hierarchical name. Other types of domains exist—e.g., broadcast domain, etc.

domain controller  A computer running Windows Server that stores a set of domain accounts.

domain-based network  Network that eliminates the need for logging on to multiple servers by using domain controllers to hold the security database for all systems.

DoS (denial of service)  An attack on a computer resource that prevents it from performing its normal operations, usually by overwhelming it with large numbers of requests in an effort to monopolize its resources.

DRAM (dynamic random access memory or dynamic RAM)  Memory used to store data in most personal computers. DRAM stores each bit in a “cell” composed of a transistor and a capacitor. Because the capacitor in a DRAM cell can only hold a charge for a few milliseconds, DRAM must be continually refreshed, or rewritten, to retain its data.

drive cloning  Taking a PC and making a duplicate of the hard drive, including all data, software, and configuration files, and transferring it to another PC. See also image deployment.

drive letter  A letter designating a specific drive or partition.

driver signing  Digital signature for drivers used by Windows to protect against potentially bad drivers.

DSL (digital subscriber line)  High-speed Internet connection technology that uses a regular telephone line for connectivity. DSL comes in several varieties, including asymmetric (ADSL) and symmetric (SDSL), and many speeds. Typical home-user DSL connections are ADSL, with faster download speeds than upload speeds.

dual boot  Refers to a computer with two operating systems installed, enabling users to choose which operating system to load on boot. Can also refer to kicking a device a second time just in case the first time didn’t work.

dual-channel architecture  Using two sticks of RAM to increase throughput. See also triple-channel architecture and quad-channel architecture.

dual-channel memory  Form of memory access used by many motherboards that requires paired identical sticks of RAM.

dumpster diving  To go through someone’s trash in search of information.

duplexing  Similar to mirroring in that data is written to and read from two physical drives, for fault tolerance. Separate controllers are used for each drive, both for additional fault tolerance and for additional speed. Considered RAID level 1. Also called disk duplexing or drive duplexing.

duplexing assembly  Mechanical feature of some printers that can automatically flip the paper to print on both sides.

DVI (digital visual interface)  Special video connector designed for digital-to-digital connections; most commonly seen on PC video cards and LCD monitors. Some versions also support analog signals with a special adapter.

dynamic disks  Special feature of Windows that enables users to span a single volume across two or more drives. Dynamic disks do not have partitions; they have volumes. Dynamic disks can be striped, mirrored, and striped or mirrored with parity.

Dynamic Host Configuration Protocol (DHCP)  Protocol that enables client hosts to request and receive TCP/IP settings automatically from an appropriately configured server. Uses UDP ports 67 and 68.

ECC (error correction code)  Special software, embedded on hard drives, that constantly scans the drives for bad blocks.

ECC RAM/DRAM (error correction code RAM/DRAM)  RAM that uses special chips to detect and fix memory errors. Commonly used in high-end servers where data integrity is crucial.

effective permissions  User’s combined permissions granted by multiple groups.

EFS (encrypting file system)  Storage organization and management service, such as NTFS, that has the capability of applying a cipher process to the stored data. The professional editions of Windows offer a feature called the Encrypting File System (EFS), an encryption scheme that any user can use to encrypt individual files or folders on a computer.

electromagnetic interference (EMI)  Electrical interference from one device to another, resulting in poor performance of the device being interfered with. Examples: static on your TV while running a blow dryer, or placing two monitors too close together and getting a “shaky” screen.

electromagnetic pulse (EMP)  Potentially damaging burst of electromagnetic energy caused by events such as electrostatic discharge (ESD), lightning, nuclear detonations, and so on.

electrostatic discharge (ESD)  Uncontrolled rush of electrons from one object to another. A real menace to PCs, as it can cause permanent damage to semiconductors.

eliciting answers  Communication strategy designed to help techs understand a user’s problems better. Works by listening to a user’s description of a problem and then asking cogent questions.

embedded system  A computer that is dedicated to a specific task and often is included as part of a larger and more complex system. Embedded systems are found in everything from medical devices to power plants to toys to railway control systems.

emergency notification  Feature built into smartphones enabling them to receive messages from emergency broadcast systems, such as the Emergency Alert System (EAS) in the United States.

encrypted  Data that has been passed through an encryption algorithm, rendering it unreadable without the decryption keys. See encryption.

encryption  Making data unreadable by those who do not possess a key or password.

end process  Option in Task Manager to halt a program or background process. Other supporting processes continue to run after ending a process they support.

end process tree  Option in Task Manager to halt a program or background process and all of its supporting processes.

end task  Process of forcibly exiting a program or application, initiated using Task Manager in Windows or Activity Monitor in macOS.

end-user acceptance  Change management step that entails educating and training users about what has changed and how to use any new systems, devices, or features.

end-user license agreement  See EULA.

Enhanced 911 (E911)  Improves 911 service for cellular phones by using GPS and cellular network triangulation to locate the device and dispatch emergency responders.

entry control roster  Document for recording who enters and leaves a building.

environment variables  System data such as the date and time, currently logged-in users, running operating system version, and more. Scripts and programs on a system often use these variables to tailor their behavior to the system’s capabilities and configuration.

environmental control  Practice of protecting computing equipment from environmental damage by taking measures such as air conditioning, proper ventilation, air filtration, temperature monitoring, and humidity monitoring.

equipment rack  A metal structure used in equipment rooms to secure network hardware devices and patch panels. Most racks are 19 inches wide. Devices designed to fit in such a rack use a height measurement called units, or simply U.

erase lamp  Component inside laser printers that uses light to make the coating of the photosensitive drum conductive.

Error checking  Windows graphical tool that scans and fixes hard drive problems. Often referred to by the name of the executable, chkdsk, or Check Disk. The macOS equivalent is the Disk Utility, and Linux offers a command-line tool called fsck.

error correction code  See ECC.

eSATA  Serial ATA-based connector for external hard drives and optical drives.

escalate  Process used when person assigned to repair a problem is not able to get the job done, such as sending the problem to someone with more expertise.

ESD mat  See antistatic mat.

ESD strap  See antistatic wrist strap.

establish a plan of action to resolve the problem and implement the solution  After establishing and testing a theory about a particular problem, techs solve the problem. (Step 4 of 6 in the CompTIA troubleshooting methodology.)

establish a theory of probable cause (question the obvious)  After identifying a problem, techs question the obvious to determine what might be the source of the problem. (Step 2 of 6 in the CompTIA troubleshooting methodology.)

Ethernet  Name coined by Xerox for the first standard of network cabling and protocols that define everything necessary to get data from one computer to another. Since its inception, Ethernet as a hardware protocol has gone through hundreds of improvements and even forms the basis of wireless networking signals.

Ethernet over Power (EoP)  Uses a building’s existing electrical network for Ethernet. Requires specialized bridges between the Ethernet network and power outlets.

Ethic of Reciprocity  Golden Rule: Do unto others as you would have them do unto you.

EULA (end-user license agreement)  Agreement that accompanies a piece of software, to which the user must agree before using the software. Outlines the terms of use for the software and also lists any actions on the part of the user that violate the agreement.

Event Viewer (eventvwr.msc)  Utility made available in Windows as an MMC snap-in that enables users to monitor and audit various system events, including network bandwidth usage and CPU utilization.

evil twin  Substitute wireless access point configured to look the same as the real one in order to gather information from users who accidentally connect to it.

exFAT  A Microsoft-proprietary file system that breaks the 4-GB file-size barrier, supporting files up to 16 exabytes (EB) and a theoretical partition limit of 64 zettabytes (ZB). Envisioned for use with flash media devices with a capacity exceeding 2 TB.

expansion slots  Connectors on a motherboard that enable users to add optional components to a system. See also PCIe.

ext4 (Fourth Extended File System)  File system used by most Linux distributions.

extended partition  Type of nonbootable hard disk partition. May only have one extended partition per disk. Purpose is to divide a large disk into smaller partitions, each with a separate drive letter.

external enclosure  Casing that encloses an external hard drive.

external speaker  Portable device that can substantially improve on the audio output of a mobile device or portable computer. Typically connects via Bluetooth or a regular headphone jack.

facial recognition  Technology that enables use of facial features to unlock a mobile device or personal computer.

factory recovery partition  See recovery partition.

factory reset  Returns a device’s software to how it left the factory by removing all user-installed data, programs, and customizations.

FAT (file allocation table)  Hidden table that records how files on a hard disk are stored in distinct clusters. The address of the first cluster of a file is stored in the directory file. The FAT entry for the first cluster is the address of the second cluster used to store that file. In the entry for the second cluster for that file is the address for the third cluster, and so on until the final cluster, which gets a special end-of-file marker. There are two FATs, mirror images of each other, in case one is destroyed or damaged. Also refers to the 16-bit file allocation table when used by Windows 2000 and later NT-based operating systems.

FAT32  File allocation table that uses 32 bits to address and index clusters. Commonly used with USB flash-media drives and versions of Windows prior to XP.

fiber optic cable  High-speed cable for transmitting data, made of high-purity glass sealed within an opaque tube. Much faster than conventional copper wire such as coaxial cable. Most common connectors include ST, SC, and LC.

file  A named collection of any form of data that is stored beyond the time of execution of a single job. A file may contain program instructions or data, which may be numerical, textual, or graphical information.

File Explorer  A tool in Windows that enables users to browse files and folders.

file extension  Two, three, four, five, or more letters that follow a filename and identify the type of file (file format). Common file extensions are .zip, .exe, .doc, .java, and .xhtml.

file format  How information is encoded in a file. Two primary types are binary (pictures) and ASCII (text), but within those are many formats, such as BMP and GIF for pictures. Commonly represented by a suffix (the file extension) at the end of the filename; for example, .txt for a text file or .exe for an executable.

File History  Control Panel applet introduced in Windows 8 for backing up personal files and folders.

file permission  Specifies what degree of access the system should grant a user or group to a particular file.

file server  Computer designated to store software, courseware, administrative tools, and other data on a LAN or WAN. It “serves” this information to other computers via the network when users enter their personal access codes.

file system  Scheme that directs how an OS stores and retrieves data on and off a drive; FAT32 and NTFS are both file systems. Used interchangeably with the term “data structure.”

File Transfer Protocol  See FTP.

file-level backup  Manually or automatically copying individual files or folders to one or more backup locations.

filename  Name assigned to a file when the file is first written on a disk. Every file on a disk within the same folder must have a unique name. Filenames can contain any character (including spaces), except the following: \ / : * ? “< > |

fileshare  A server set up to share documents and other files with other users on a network.

find  Linux command used to locate files in the filesystem.

Finder  macOS’s file and folder browser.

fingerprint lock  Type of biometric device that enables a user to unlock a mobile device using a fingerprint.

fingerprint scanner  Scanner that reads the unique pattern of a person’s fingerprint to authenticate them. Used primarily to unlock devices like smartphones and some laptops.

firewall  Device that restricts traffic between a local network and the Internet.

firmware  Embedded programs or code stored on a ROM chip. Generally OS-independent, thus allowing devices to operate in a wide variety of circumstances without direct OS support. The system BIOS is firmware.

firmware update  Process by which the BIOS of a motherboard can be updated to reflect patched bugs and added features. Performed, usually, through CMOS, though some motherboard manufacturers provide a Windows program for performing a firmware update.

flash ROM  ROM technology that can be electrically reprogrammed while still in the PC. Overwhelmingly the most common storage medium of BIOS in computers today, as it can be upgraded without a need to open the computer on most systems.

flux capacitor  A rectangular-shaped compartment with three flashing Geissler-style tubes arranged in a “Y” configuration that makes time travel possible.

folder permission  Specifies what degree of access the system should grant a user or group to a particular folder.

force stop  Terminate an Android app and all associated background processes. More extreme than simply closing the app, which may leave background processes running.

form factor  Standard for the physical organization of motherboard components and motherboard size. Most common form factors are ATX, microATX, and Mini-ITX.

format  Command-line tool used to format a storage device.

formatting  The process of preparing a partition to store files by creating a file system to organize the blocks and creating a root directory.

fragmentation  Occurs when files and directories get jumbled on a fixed disk and are no longer contiguous. Can significantly slow down hard drive access times and can be repaired in windows by using Optimize Drives. See also defragmentation.

frame  A data unit transferred across a network. Frames consist of several parts, such as the sending and receiving MAC addresses, the data being sent, and the frame check sequence.

freeware  Software that is distributed for free, with no license fee.

FRU (field replaceable unit)  Any part of a PC that is considered to be replaceable “in the field,” i.e., a customer location. There is no official list of FRUs—it is usually a matter of policy by the repair center.

FTP (File Transfer Protocol)  Rules that enable two computers to talk to one another during a file transfer. Protocol used when you transfer a file from one computer to another across the Internet. FTP uses port numbers 20 and 21.

F-type connector  Common coax connector secured with a screw connector.

full device encryption  Enhances mobile device security by encrypting the device’s internal storage.

full format  Format process that tests every sector to mark out the unusable ones in the file allocation table (FAT). See formatting.

full-duplex  Any device that can send and receive data simultaneously.

Full-Speed USB  USB standard that runs at 12 Mbps. Also known as USB 1.1.

fully qualified domain name (FQDN)  A complete, bottom-to-top label of a DNS host going from the specific host to the top-level domain that holds it and all of the intervening domain layers, each layer being separated by a dot. FQDNs are entered into browser bars and other utilities in formats like mail.totalseminars.com.

Function (FN) key  Special key on many laptops that enables some keys to perform a third duty.

Gaming (Windows Settings)  Windows Settings category that contains options to optimize and modify gaming experiences.

GDDR5  Fifth generation of graphical DDR RAM found on high-performance video cards.

General Data Protection Regulation (GDPR)  European Union law that defines a broad set of rights and protections of personal information for citizens of the EU.

general protection fault (GPF)  Error code usually seen when separate active programs conflict on resources or data. Can cause an application to crash.

geofencing  Using mobile device features to detect when the device enters or exits a defined area.

geotracking  Feature in cellular phones that enables cell phone companies and government agencies to use the ID or MAC address to pinpoint where a phone is at any given time.

gestures  Specific motions the user performs on a touchscreen, such as pinching or swiping, that have a special meaning to the app being used.

giga  Prefix for the quantity 1,073,741,824 (230) or for 1 billion. One gigabyte would be 1,073,741,824 bytes, except with hard drive labeling, where it means 1 billion bytes. One gigahertz is 1 billion hertz.

Global Positioning System (GPS)  Technology that enables a mobile device to determine where you are on a map.

global user account  Login information and associated settings maintained at a location accessible by any computer, irrespective of location or local account configuration.

globally unique identifier (GUID) partition table (GPT)  Partitioning scheme that enables you to create more than four primary partitions without needing to use dynamic disks.

Google Play  Google’s app and media store for Android devices.

Google Workspace  Google’s suite of productivity tools and applications. Can be synchronized across multiple devices to enable more efficient workflow.

gpresult  Windows command for listing group policies applied to a user.

GPS  See Global Positioning System.

GPU (graphics processing unit)  Specialized processor that helps the CPU by taking over all of the 3-D rendering duties.

gpupdate  Windows command for making immediate group policy changes in an individual system.

graphical user interface (GUI)  See GUI.

grep  Linux command to search through text files or command outputs to find specific information or to filter out unneeded information.

group  Collection of user accounts that share the same access capabilities.

group policy  Means of easily controlling the settings of multiple network clients with policies such as setting minimum password length or preventing Registry edits.

Group Policy Editor (gpedit.msc)  MMC snap-in used to change or modify group policy in Windows.

GSM (Global System for Mobile Communications)  Wireless data standard for mobile devices.

guest  An operating system running inside a virtual machine.

guest account  Very limited built-in account type for Windows; a member of the Guests group.

Guests group  User group that enables someone without an account to use a system. See group.

GUI (graphical user interface)  Interface that enables user to interact with computer graphically, by using a mouse or other pointing device to manipulate icons that represent programs or documents, instead of using only text as in early interfaces. Pronounced “gooey.”

half-duplex  Transmission mode where a device can either send or receive, but not do both at once.

hang  Occurs when a computer or program stops responding to keyboard commands or other input; a computer or program in such a state is said to be “hung.”

hang time  Number of seconds a too-often-hung computer is airborne after you have thrown it out a second-story window.

hard drive  See HDD.

hard reset  For mobile devices, another term for a factory reset. Don’t confuse this with a hard reboot. See factory reset.

hard token  Dedicated device that contains information used as an authentication factor when logging on to a secure site.

hardware  Physical computer equipment such as electrical, electronic, magnetic, and mechanical devices. Anything in the computer world that you can hold in your hand. A hard drive is hardware; Microsoft Word is not.

hardware firewall  Firewall implemented within networking hardware such as a router. See firewall.

hardware protocol  Defines many aspects of a network, from the packet type to the cabling and connectors used. Ethernet is an example of a hardware protocol.

hardware virtualization  Processor features that speed up and simplify virtualization. Required for some hypervisors to function. See also hypervisor.

hardware-assisted virtualization  Virtualization that makes use of the host machine’s hardware to enable the virtualized software to function.

hash  A special value computed from some other value using an irreversible computation. Has many uses in computing, and plays a key role in modern authentication systems. Instead of saving user passwords directly in a database (which would make them a huge target for attackers), well-designed authentication systems compute and save only a (salted) hash of each password. When the user attempts to log in, the system hashes the provided password to see if it matches the saved hash. See also salted hash.

HDD (hard disk drive)  Data-recording system using solid disks of magnetic material turning at high speeds to store and retrieve programs and data in a computer.

HDMI (High-Definition Multimedia Interface)  Single multimedia connection that includes both high-definition video and audio. Used to connect a computer to LCDs, projectors, and VR headsets.

heat dope  See thermal paste.

heat sink  A specially designed hunk of metal such as aluminum or copper that conducts heat away from a CPU or other heat-producing component and out into fins that transfer the heat to circulating air. When used to cool a CPU, a heat sink is typically paired with a fan assembly to improve its performance.

hex (hexadecimal)  Base-16 numbering system using ten digits (0 through 9) and six letters (A through F). In the computer world, shorthand way to write binary numbers by substituting one hex digit for a four-digit binary number (e.g., hex 9 = binary 1001).

hibernate  Power management setting in which all data from RAM is written to the hard drive before the system goes into sleep mode. Upon waking up, all information is retrieved from the hard drive and returned to RAM. Also called suspend to disk.

hidden attribute  File attribute that, when used, does not allow the dir command to show a file.

hierarchical directory tree  Method by which Windows organizes files into a series of folders, called directories, under the root directory. See also root directory.

high availability  A trait of systems that indicates an emphasis on reliable operations with minimal or no downtime.

High Dynamic Range (HDR)  Video technology that increases the bandwidth of display colors and light intensity above standard dynamic range.

high-level formatting  Format that sets up a file system on a drive.

Hi-Speed USB  USB standard that runs at 480 Mbps. Also referred to as USB 2.0.

horizontal cabling  Cabling that connects the equipment room to the work areas.

host (networking)  On a TCP/IP network, a single device that has an IP address—any device (usually a computer) that can be the source or destination of a data packet. Also, in virtualization, a computer running one or more virtual operating systems.

host (virtualization)  The system running (or hosting) a virtual machine.

host ID  The address of a TCP/IP device such as a computer, printer, camera, or other device.

hostname  Windows command for displaying the name of a computer.

hotspot  A mobile device that broadcasts a small Wi-Fi network to share its mobile data network connection with nearby Wi-Fi devices. Often a standalone device, though many cellular phones and data-connected tablets can be set up to act as hotspots.

hot-swappable  Any hardware that may be attached to or removed from a PC without interrupting the PC’s normal processing.

hot-swapping  Replacing a bad drive in a RAID array without needing to reboot or power down.

HTML (Hypertext Markup Language)  ASCII-based, script-like language for creating hypertext documents such as those on the World Wide Web.

HTTP (Hypertext Transfer Protocol)  Extremely fast protocol used for network file transfers in the WWW environment. Uses port 80.

HTTPS (HTTP over Secure Sockets Layer)  Secure form of HTTP used commonly for Internet business transactions or any time when a secure connection is required. Uses port 443.

hub  Electronic device that sits at the center of a star bus topology network, providing a common point for the connection of network devices. Hubs repeat all information out to all ports and have been replaced by switches, although the term “hub” is still commonly used. A USB hub shares a single USB connection and its bandwidth among connected devices.

hybrid  A network topology that combines features from multiple other topologies, such as the star bus topology.

hybrid cloud  A combination of cloud resources from more than one of the three cloud types (community, private, and public).

Hyper-Threading  Intel CPU feature (generically called simultaneous multithreading) that enables a CPU to run more than one thread at once.

hypervisor  Software that enables a single computer to run multiple operating systems simultaneously.

I/O (input/output)  General term for reading and writing data to a computer. “Input” includes data entered from a keyboard, identified by a pointing device (such as a mouse), or loaded from a disk. “Output” includes writing information to a disk, viewing it on a monitor, or printing it to a printer.

IaaS  See Infrastructure as a Service.

iCloud  Apple cloud-based storage. iCloud enables a user to back up all iPhone or iPad data, and makes that data accessible from anywhere. This includes any media purchased through iTunes as well as calendars, contacts, reminders, and so forth.

ID badge  Small card or document for confirming the identity of its holder and what access they should be granted. May use built-in authentication tools such as RFID or smart card to function as a “something you have” authentication factor.

IDE (Integrated Drive Electronics)  PC specification for small- to medium-sized hard drives in which the controlling electronics for the drive are part of the drive itself, speeding up transfer rates and requiring only a simple adapter (or “paddle”) connection on a motherboard. IDE only supported two drives per system of no more than 504 MB each, and has been completely supplanted by Enhanced IDE. EIDE supports four drives of over 8 GB each and more than doubles the transfer rate. The more common name for PATA drives.

identify the problem  To question the user and find out what has been changed recently or is no longer working properly. (Step 1 of 6 in the CompTIA troubleshooting methodology.)

IEC-320 connector  Connects the cable supplying AC power from a wall outlet into the power supply.

IEEE (Institute of Electronic and Electrical Engineers)  Leading standards-setting group in the United States.

IEEE 802.11  Wireless Ethernet standard more commonly known as Wi-Fi.

image deployment  Operating system installation that uses a complete image of a hard drive as an installation media. Helpful when installing an operating system on a large number of identical PCs.

image file  Bit-by-bit image of data to be burned on optical media or flash drive—from one file to an entire disk—stored as a single file on a hard drive. Particularly handy when copying from CD to CD or DVD to DVD.

image-level backup  Backing up a complete volume, including any OS, boot files, applications, and data it contains.

IMAP4 (Internet Message Access Protocol version 4)  An alternative to POP3 that retrieves e-mail from an e-mail server; IMAP uses TCP port 143.

IMEI (International Mobile Equipment Identity)  A 15-digit number used to uniquely identify a mobile device, typically a smartphone or other device that connects to a cellular network.

impedance  Amount of resistance to an electrical signal on a wire. Relative measure of the amount of data a cable can handle.

impersonation  A social engineering attack in which a person pretends to be someone else in order to gain access to confidential data or to launch attacks against a computer network.

incident report  Record of the details of an accident, including what happened and where it happened.

incident reporting  Process of reporting gathered data about a system or problem to supervisors. Creates a record of work accomplished and may help identify patterns. Often documented on an incident report form.

Infrastructure as a Service (IaaS)  Cloud-hosted provider of virtualized servers and networks.

inheritance  NTFS feature that passes on the same permissions in any subfolders/files resident in the original folder.

in-place upgrade  See upgrade installation.

insider threat  Threat to an organization that originates from within. An insider threat can be malicious or accidental, but either way, it introduces some type of risk to safety, data, and the business.

installation media (drivers)  Optical media or drive (such as a USB flash drive) that holds all the necessary device driver files for a specific device such as a printer, scanner, or motherboard.

installation media (operating systems)  Optical media or drive (such as a USB flash drive) that holds all the necessary files for installing an operating system or an application (program).

integrated GPU  GPU integrated with the motherboard or processor, in contrast to GPUs on separate graphics cards. This typically lowers power consumption, saves space, reduces heat, and may speed up communication with the GPU.

Intel  One of the two major CPU manufacturers and the original creator of the x86 CPU architecture. Competes directly with AMD in desktop, laptop, and server processors.

interface  Means by which a user interacts with a piece of software.

Internet of Things (IoT)  Everyday home objects that incorporate computing and networked features to enable enhanced functionality. Smart home devices, home security systems, and even refrigerators can be part of the Internet of Things.

Internet service provider (ISP)  Company that provides access to the Internet, usually for money.

interrupt/interruption  Suspension of a process, such as the execution of a computer program, caused by an event external to the computer and performed in such a way that the process can be resumed. Events of this kind include sensors monitoring laboratory equipment or a user pressing an interrupt key.

intrusion detection system (IDS)  Application that inspects packets, looking for active intrusions. Functions inside the network, looking for threats a firewall might miss, such as viruses, illegal logon attempts, and other well-known attacks. May also discover threats from inside the network, such as a vulnerability scanner run by a rogue employee.

intrusion prevention system (IPS)  Application similar to an intrusion detection system (IDS), except that it sits directly in the flow of network traffic. This enables it to stop ongoing attacks itself, but may also slow down the network and be a single point of failure.

inventory management  A process for protecting devices and equipment by tagging them with barcodes or asset tags and keeping track of these tagged devices.

inverter  Device used to convert DC current into AC. Commonly used in older laptops and flatbed scanners with CCFLs.

iOS  The operating system of Apple iPhones.

IoT  See Internet of Things.

ip  Command-line utility for Linux servers and workstations that displays the current TCP/IP configuration of the machine. Similar to ipconfig in Windows.

IP address  Numeric address of a computer connected to the Internet. An IPv4 address is made up of four octets of 8-bit binary numbers (32 bits total) translated into their shorthand numeric values. An IPv6 address is 128 bits long. The IP address can be broken down into a network ID and a host ID. Also called Internet address.

iPadOS  The operating system of Apple’s iPad tablets.

ipconfig  Command-line utility for Windows servers and workstations that displays the current TCP/IP configuration of the machine. Similar to ip in Linux.

IPS (in-plane switching)  Display technology that replaces the older twisted nematic (TN) panels for more accurate colors and a wider viewing angle.

IPsec (Internet Protocol security)  Microsoft’s encryption method of choice for networks consisting of multiple networks linked by a private connection, providing transparent encryption between the server and the client.

IPv4 (Internet Protocol version 4)  Internet standard protocol that provides a common layer over dissimilar networks; used to move packets among host computers and through gateways if necessary. Part of the TCP/IP protocol suite. Uses the dotted-decimal format—x.x.x.x. Each x represents an 8-bit binary number, or 0–255. Here’s an example: 192.168.4.1.

IPv6 (Internet Protocol version 6)  Protocol in which addresses consist of eight sets of four hexadecimal numbers, each number being a value between 0000 and ffff, using a colon to separate the numbers. Here’s an example: fedc:ba98:7654:3210:0800:200c:00cf:1234.

ISO file  Complete copy (or image) of a storage media device, typically used for optical discs. ISO image files typically have a file extension of .iso.

ISP  See Internet service provider.

ITX (Information Technology eXtended)  A family of motherboard form factors. Mini-ITX is the largest and the most popular of the ITX form factors but is still quite small.

jack (physical connection)  Part of a connector into which a plug is inserted. Also referred to as a port.

jailbreaking  Process for circumventing the security restrictions present on an iOS device.

jitter  Network issue in which packets are delayed by variable lengths of time, leading to poor performance.

joule  Unit of energy describing (in this book) how much energy a surge suppressor can handle before it fails.

jumper  Pair of small pins that can be shorted with a shunt to configure many aspects of PCs. Often used in configurations that are rarely changed.

Keep my files  Windows Recovery Environment option in Windows 10 that rebuilds the OS but preserves user files, settings, and Microsoft Store applications (while deleting all other applications on the system).

Kerberos  Authentication encryption developed by MIT to enable multiple brands of servers to authenticate multiple brands of clients.

kernel  Core portion of program that resides in memory and performs the most essential operating system tasks.

kernel panic  The Linux/macOS equivalent of the Windows BSoD. An error from which the OS can’t recover without a reboot. See also Blue Screen of Death.

key fob  Generically, just about anything attached to a key ring that isn’t a key. Some security tools, such as hardware security tokens and RFID authentication devices, are commonly designed as key fobs.

Keychain  A macOS password management and storage service that saves passwords for computer and non-computer environments. Also, the iCloud Keychain adds synchronization among any macOS and iOS devices connected to the Internet for a user account.

keylogger  Software, usually malware, that copies, saves, and sometimes uploads all keystrokes and other inputs on a computer. Keyloggers are used to gather information such as passwords, Web sites visited, and other activities performed on a computer.

kill  Command in UNIX shells (such as Bash) and in PowerShell that terminates an indicated process.

KVM (keyboard, video, mouse) switch  Hardware device that enables multiple computers to be viewed and controlled by a single mouse, keyboard, and screen.

LAN (local area network)  Group of computers connected via cabling, radio, or infrared that uses this connectivity to share resources such as printers and mass storage.

laser  Single-wavelength, in-phase light source that is sometimes strapped to the head of sharks by bad guys. Note to henchmen: Lasers should never be used with sea bass, no matter how ill-tempered they might be. They should, however, be used in optical disc technology, laser-based projectors, single-mode fiber optic cables, and/or laser printers.

latency  Amount of delay before a device may respond to a request; most commonly used in reference to RAM.

launcher  An Android app that serves as the device’s desktop, often with more extensive customization features than launchers provided by Google or the device maker.

LBA (logical block addressing)  See logical block addressing.

LC  See Lucent connector.

LCD (liquid crystal display)  Type of display commonly used on portable computers. LCDs have also replaced CRTs as the display of choice for desktop computer users. LCDs use liquid crystals and electricity to produce images on the screen.

lease  A temporary IP address assignment to a device on the network from a pool of available addresses.

LED (light-emitting diode)  Solid-state device that vibrates at luminous frequencies when current is applied.

Level 1 (L1) cache  First RAM cache accessed by the CPU, which stores only the absolute most accessed programming and data used by currently running threads. Always the smallest and fastest cache on the CPU.

Level 2 (L2) cache  Second RAM cache accessed by the CPU. Much larger and often slower than the L1 cache, and accessed only if the requested program/data is not in the L1 cache.

Level 3 (L3) cache  Third RAM cache accessed by the CPU. Much larger and slower than the L1 and L2 caches, and accessed only if the requested program/data is not in the L2 cache.

LGA (land grid array)  Arrangement of a large number of pins extending from the CPU socket to corresponding contact points on the bottom of the CPU.

Libraries  Feature in Windows that aggregates folders from multiple locations and places them in a single, easy-to-find spot in File Explorer. Default libraries in Windows include Documents, Music, Pictures, and Videos.

Lightning  An 8-pin connector, proprietary to Apple, that can be inserted without regard to orientation. Used to connect mobile devices to a power or data source.

Lightweight Directory Access Protocol (LDAP)  Protocol used for obtaining directory information over a network. Uses port 389.

Li-Ion (Lithium-Ion)  Battery commonly used in portable computing devices. Li-Ion batteries don’t suffer from the memory effects of Nickel-Cadmium (Ni-Cd) batteries and provide much more power for a greater length of time.

link light  An LED on NICs, hubs, and switches that lights up to show good connection between the devices.

link-local address  IPv6 address a computer gives itself when it first boots. IPv6’s equivalent to IPv4’s APIPA address.

Linux  Open-source UNIX-clone operating system.

liquid cooling  A method of cooling a PC that works by running some liquid—usually water—through a metal block that sits on top of the CPU, absorbing heat. The liquid gets heated by the block, runs out of the block and into something that cools the liquid, and is then pumped through the block again.

load balancer  A device that spreads network traffic across multiple servers in order to improve availability of resources.

local area network  See LAN.

Local Security Policy  Windows tool used to set local security policies on an individual system.

local share  File sharing server that only shares with local devices on a LAN.

local user account  List of usernames and their associated passwords with access to a system, contained in an encrypted database.

local username  Username that is stored on the device, rather than on an Active Directory domain controller.

Local Users and Groups (lusrmgr.msc)  Tool enabling creation and changing of group memberships and accounts for users.

location data  Information provided by a mobile device’s GPS; used for mapping functions as well as for location-aware services, such as finding nearby restaurants or receiving coupons for nearby shops.

locator application  Application designed to enable the user of a mobile device or laptop to locate the device in the event that it was lost or stolen.

log files  Files created in Windows to track the progress of certain processes.

logical block addressing (LBA)  Addressing scheme that presents storage chunks on a storage device to the OS as a sequence of blocks beginning with LBA0. This saves the OS from having to deal directly with the details of how storage space is arranged on a hard drive or SSD.

logical drives  Sections of an extended partition on a hard drive that are formatted and (usually) assigned a drive letter, each of which is presented to the user as if it were a separate drive.

logical security  Security measures focused on denying access to networks, systems, and data.

logon screen  First screen of the Windows interface, used to log on to the computer system.

Long Term Evolution (LTE)  Fourth-generation cellular network technology supporting theoretical download speeds up to 1 Gbps and upload speeds up to 100 Mbps. Marketed as and now generally accepted as a true 4G technology.

long-range fixed wireless  Method of wirelessly connecting networks when it isn’t feasible to run cables. Uses directional antennas and can connect buildings up to several miles away.

loop  Control construct used in a script or program to repeat a sequence of instructions when certain conditions are met. For example, a script could use a loop to a set of instructions for resizing an image once for every image file in a directory.

loopback plug  Device used during loopback tests to check the female connector on a NIC.

loopback test  Special test to confirm a NIC can send and receive data. A full external loopback test requires a loopback plug inserted into the NIC’s port.

ls  UNIX equivalent of the dir command, which displays the contents of a directory.

LTE  See Long Term Evolution.

Lucent connector (LC)  Type of fiber optic connector. See fiber optic cable.

M.2  Type of space-efficient expansion slot common in recent portable computers. Also found on some desktop motherboards. M.2 is available in different configurations to support Wi-Fi cards and SSDs.

Mac  Also Macintosh. Common name for Apple Computers’ flagship operating system, as well as their desktop and laptop computers; Apple calls the current operating system macOS.

MAC (mandatory access control)  Authorization method in which the system grants access to resources based on security labels and clearance levels. Less flexible than discretionary access control (DAC), which lets users assign access levels to resources they own. MAC may be used in organizations with very high security needs.

MAC (media access control) address  Unique 48-bit address assigned to each network card. IEEE assigns blocks of possible addresses to various NIC manufacturers to help ensure that the address is always unique. The Data Link layer of the OSI model uses MAC addresses to locate machines.

MAC address filtering  Method of limiting wireless network access based on the physical, hard-wired address of the wireless NIC of a computing device.

machine language  Binary instruction code that is understood by the CPU.

macOS  Operating system from Apple that powers its desktop and portable computers. Based on UNIX; most versions of macOS run on Intel/IBM-based hardware, just like Microsoft Windows. The latest versions of macOS also support Apple’s new M1 and M2 ARM-based processors. Before 2016, it was known as OS X. See also Mac.

magnetic hard drives  Storage devices that read and write data encoded magnetically onto spinning aluminum platters.

magnetometer  A fancy way of saying metal detector.

mail server  Networked host or server that provides e-mail service.

maintenance kit  Set of commonly replaced printer components provided by many manufacturers.

malware  Broadly, software designed to use your computer or device against your wishes. Includes adware, spyware, viruses, ransomware, etc. May be part of seemingly legitimate software or installed by exploiting a vulnerability in the device.

MAM  See mobile application management.

man  Linux command short for manual. Brings up user manual for a wide variety of other Linux commands and utilities.

MAN (metropolitan area network)  802.11 network that covers a single city.

mandatory access control  See MAC (mandatory access control).

man-in-the-middle attack  See on-path attack.

mass storage  Hard drives, optical discs, removable media drives, etc.

master boot record (MBR)  Tiny bit of code that takes control of the boot process from the system BIOS.

Material Safety Data Sheet (MSDS)  Standardized form that provides detailed information about potential environmental hazards and proper disposal methods associated with various computing components.

md (mkdir)  Command-line tool used to create directories.

MDM  See mobile device management.

media access control  See MAC (media access control) address.

mega-  Prefix that stands for the binary quantity 1,048,576 (220) or the decimal quantity of 1,000,000. One megabyte is 1,048,576 bytes. Sometimes shortened to Meg, as in “my video card has 8 Megs of video RAM.” One megahertz, however, is a million hertz.

memory  Device or medium for temporary storage of programs and data during program execution. Synonymous with storage, although it most frequently refers to the internal storage of a computer that can be directly addressed by operating instructions. A computer’s temporary storage capacity is measured in kilobytes (KB), megabytes (MB), or gigabytes (GB) of RAM (random-access memory). Long-term data storage on hard drives and solid-state drives is also measured in megabytes, gigabytes, and terabytes.

mesh topology  Network topology where each computer has a dedicated line to every other computer, most often used in wireless networks.

metered utilization  Fee charged by cloud service providers on the basis of how much of a resource was used. Fees may be based on things like access time, bandwidth used, bytes uploaded or downloaded, CPU usage, and other resource usage metrics.

metropolitan area network  See MAN.

MFA  See multifactor authentication.

MFD  See multifunction device.

MFT (master file table)  Enhanced file allocation table used by NTFS. See also FAT.

micro Secure Digital (microSD)  The smallest form factor of the SD flash memory standard. Often used in mobile devices.

microATX (µATX)  Variation of the ATX form factor, which uses the ATX power supply. MicroATX motherboards are generally smaller than their ATX counterparts but retain all the same functionality.

microprocessor  “Brain” of a computer. Primary computer chip that determines relative speed and capabilities of the computer. Also called the central processing unit (CPU).

Microsoft 365  Microsoft’s subscription suite of productivity apps; includes Word, Teams, Outlook, SharePoint, PowerPoint, and numerous other applications used in homes and businesses around the world.

Microsoft Management Console (MMC)  A shell program in Windows that holds individual utilities called snap-ins, designed for administration and troubleshooting. The MMC enables an administrator to customize management tools by picking and choosing from a list of snap-ins. Available snap-ins include Device Manager, Event Viewer, Local Users and Groups, and Computer Management.

Microsoft Remote Assistance (MSRA)  Feature of Windows that enables users to give anyone control of his or her desktop over the Internet.

microUSB  USB connector commonly found on a variety of devices including Android phones. Slowly being replaced by USB Type-C connectors (especially in Android phones).

migration  Moving users from one operating system or hard drive to another. Particularly common when upgrading operating systems or migrating from a mechanical hard drive (HDD) to a solid-state drive (SSD).

MIMO (multiple in/multiple out)  Feature of 802.11n devices that enables the simultaneous connection of up to four antennas, greatly increasing throughput. 802.11ac also uses Multiuser MIMO (MU-MIMO), which gives a WAP the capability to broadcast to multiple users simultaneously.

mini connector  One type of power connector from a PC power supply unit. Supplies 5 and 12 volts to peripherals.

Mini-ITX  The largest and the most popular of the three ITX form factors. At a miniscule 6.7 by 6.7 inches, Mini-ITX competes with microATX and proprietary small form factor (SFF) motherboards.

miniUSB  Smaller USB connector often found on digital cameras.

mirror set  A type of mirrored volume created with RAID 1. See also mirroring.

mirror space  Storage Space that mirrors files across two or more drives, like RAID 1 or RAID 10. See Storage Spaces.

mirrored volume  Volume that is mirrored on another volume. See also mirroring.

mirroring  Reading and writing data at the same time to two drives for fault tolerance purposes. Considered RAID level 1. Also called drive mirroring.

Mission Control  A feature of macOS that enables switching between open applications, windows, and more.

mkdir  See md.

MMC  See Microsoft Management Console.

mobile application management (MAM)  Enables IT to make and enforce policies regarding appropriate and safe application use on business devices and premises as well as allowing them to push updates and make changes to specific applications.

mobile device  Small, highly portable computing device with tightly integrated components designed to be worn or carried by the user. Includes smartphones, tablets, and wearable devices.

mobile device management (MDM)  A formalized structure that enables an organization to account for all the different types of devices used to process, store, transmit, and receive organizational data.

mobile device management (MDM) policies  Technical controls that govern how mobile devices are used as tools in the workplace.

mobile hotspot  See hotspot.

Molex connector  Computer power connector used by optical drives, hard drives, and case fans. Keyed to prevent it from being inserted into a power port improperly.

monitor  Screen that displays data from a PC. Typically a flat-panel display, such as an LCD.

motherboard  Flat piece of circuit board that resides inside your computer case and has a number of connectors on it. Every device in a PC connects directly or indirectly to the motherboard, including CPU, RAM, hard drives, optical drives, keyboard, mouse, and video cards.

motherboard book  Valuable resource when installing a new motherboard. Normally lists all the specifications about a motherboard, including the type of memory and type of CPU usable with the motherboard.

move  Command-line tool used to move a file from one location to another.

mSATA  Standardized smaller SATA form factor for use in portable devices.

MSDS  See Material Safety Data Sheet.

msinfo32 (System Information)  Provides information about hardware resources, components, and the software environment.

multiboot installation  OS installation in which multiple operating systems are installed on a single machine.

multicore processing  Using two or more execution cores on one CPU die to divide up work independently of the OS.

multifactor authentication (MFA)  Authentication schema requiring more than one unique authentication factor. The factors are knowledge, possession, inherence, location, and temporal. For example, a password (knowledge factor) and a fingerprint (inherence factor) is a basic form of multifactor authentication.

multifunction device (MFD)  Single device that consolidates functions from more than one document-handling device, such as a printer, copier, scanner, or fax machine.

multimeter  Device used to measure voltage, amperage, and resistance.

multimode  Type of fiber optic cabling capable of transmitting multiple light signals at the same time using different reflection angles within the cable core. Signals tend to degrade over distance, limiting multimode cable to short distances. See fiber optic cable.

multiple Desktops  A GUI feature that enables a computer to have more than one Desktop, each with its own icons and background. macOS supports multiple Desktops with Spaces. Most Linux distros use multiple Desktops, often called workspaces. Microsoft introduced the feature with Windows 10.

multitasking  Process of running multiple programs or tasks on the same computer at the same time.

multitouch  Input method on many smartphones and tablets that enables you to perform gestures (actions with multiple fingers) to do all sorts of fun things, such as using two fingers to scroll or swipe to another screen or desktop.

Multiuser MIMO (MU-MIMO)  New version of MIMO included in 802.11ac that enables a WAP to broadcast to multiple users simultaneously.

mv  The move command in Linux and macOS.

NAT (Network Address Translation)  A means of translating a system’s IP address into another IP address before sending it out to a larger network. NAT manifests itself by a NAT program that runs on a system or a router. A network using NAT provides the systems on the network with private IP addresses. The system running the NAT software has two interfaces: one connected to the network and the other connected to the larger network. The NAT program takes packets from the client systems bound for the larger network and translates their internal private IP addresses to its own public IP address, enabling many systems to share a single IP address.

native resolution  Resolution on an LCD monitor that matches the physical pixels on the screen.

Near-Field Communication  See NFC.

near-field scanner  Enables mobile devices to use near-field communication to read things like barcodes and bank cards.

net  Command-line utility in Windows that enables users to view and change a whole host of network settings and information.

net use  Subcommand of the Windows net command that enables a user to connect, disconnect, and view information about existing connections to network resources.

net user  Subcommand of the Windows net command that enables a user to create, delete, and change user accounts.

NetBIOS (Network Basic Input/Output System)  Protocol that operates at the Session layer of the OSI seven-layer model. This protocol creates and manages connections based on the names of the computers involved. Uses TCP ports 137 and 139, and UDP ports 137 and 138.

netstat  Command-line tool in Windows and Linux to identify inbound and outbound TCP/IP connections with the host.

network  Collection of two or more computers interconnected by telephone lines, coaxial cables, satellite links, radio, and/or some other communication technique that communicate with one another for a common purpose.

Network  Interface in File Explorer that displays networked computers and other devices, such as network printers.

Network & Internet (Windows Settings)  Windows Settings category that contains options and settings relating to networks and Internet connectivity, including checking connection status, network sharing, and VPN settings.

network attached storage (NAS)  A device that attaches to a network for the sole purpose of storing and sharing files.

network connection  A method for connecting two or more computers together. See also network.

network documentation  A road map to an organization’s network configuration and topology to guide techs who need to change or repair the network.

network ID  Logical number that identifies the network on which a device or machine exists. This number exists in TCP/IP and other network protocol suites.

network interface card (or controller)  See NIC.

network protocol  Software that takes the incoming data received by the network card, keeps it organized, sends it to the application that needs it, and then takes outgoing data from the application and hands it to the NIC to be sent out over the network.

network topology diagram  A map of how everything in an organization’s network (including switches, routers, WAPs, services, and workstations) connects. May indicate connection types, speed, technologies, and so on.

NFC (Near Field Communication)  Mobile technology that enables short-range wireless communication between mobile devices. Now used for mobile payment technology such as Apple Pay and Google Pay.

NIC (network interface card or controller)  Expansion card or motherboard interface that enables a PC to connect to a network via a network cable. A wireless NIC enables connection via radio waves rather than a physical cable. Also commonly called a wireless card or Wi-Fi card.

nit  Value used to measure the brightness of an LCD display. A typical LCD display has a brightness of between 100 and 400 nits.

nonvolatile  Describes storage that retains data even if power is removed; typically refers to a ROM or flash ROM chip, but also could be applied to hard drives, optical media, and other storage devices.

notification area  Windows GUI feature that contains icons representing background processes, the system clock, and volume control. Located by default at the right edge of the Windows taskbar. Many users call this area the system tray.

nslookup  Command-line program in Windows used to determine exactly what information the DNS server is providing about a specific host name.

NTFS (New Technology File System)  Robust and secure file system introduced by Microsoft with Windows NT. NTFS provides an amazing array of configuration options for user access and security. Users can be granted access to data on a file-by-file basis. NTFS enables object-level security, long filename support, compression, and encryption.

NTFS permissions  Restrictions that determine the amount of access given to a particular user on a system using NTFS.

NVIDIA Corporation  One of the foremost manufacturers of graphics cards and chipsets.

NVMe (Non-Volatile Memory Express)  SSD technology that supports a communication connection between the operating system and the SSD directly through a PCIe bus lane, reducing latency and taking full advantage of the speeds of high-end SSDs. NVMe SSDs come in a few formats, such as an add-on expansion card, though most commonly in M.2 format. NVMe drives are a lot more expensive currently than other SSDs, but offer much higher speeds. NVMe drives use SATAe.

object  System component that is given a set of characteristics and can be managed by the operating system as a single entity.

ohm(s)  A unit of measurement of electronic resistance; used to measure cable’s impedance.

OLED (organic light-emitting diode)  Display technology where an organic compound provides the light for the screen, thus eliminating the need for a backlight or inverter. Used in high-end TVs and small devices such as smart watches, smartphones, and VR headsets.

on-path attack  Attacker serves as an intermediary between two systems, enabling the attacker to observe, redirect, or even alter messages passing in either direction. Also commonly known as a man-in-the-middle (MITM) attack.

operating system (OS)  Series of programs and code that creates an interface so users can interact with a system’s hardware; for example, Windows, macOS, and Linux.

optical disc/media  Types of data discs (such as DVDs, CDs, BDs, etc.) that are read by a laser.

optical drive  Drive used to read/write to optical discs, such as CDs or DVDs.

optical network terminal (ONT)  Works like a modem, but for fiber optic networks. Enables your networked devices to communicate with an Internet service provider.

optimization  Changes made to a system to improve its performance.

OS  See operating system.

overclocking  To run a CPU or video processor faster than its rated speed.

overloaded network  A mobile network that, often due to a large public event, emergency, or network equipment failure, is unable to keep up with user demand. Users may have good signal quality but be unable to access data, text, or voice services.

owner  In both NTFS and UNIX permissions, usually the user that created a given file or folder, although both systems support changing ownership to another user.

Ownership permission  Special NTFS permissions granted to the account that owns a file or folder. Owners can do anything they want to the files and folders they own, including changing their permissions.

PaaS  See Platform as a Service.

packet  Basic component of communication over a network. Group of bits of fixed maximum size and well-defined format that is switched and transmitted as a single entity through a network. Contains source and destination addresses, data, and control information. Packets are included within (and are not the same thing as) a frame.

page file  See virtual memory.

PAN (personal area network)  Small wireless network created with Bluetooth technology and intended to link computers and other peripheral devices.

parallel execution  When a multicore CPU processes more than one thread.

parity RAM  Earliest form of error-detecting RAM; stored an extra bit (called the parity bit) to verify the data.

parity space  Storage Space that adds resiliency similar to RAID 5 or RAID 6. See Storage Spaces.

partition  Section of the storage area of a hard disk. Created during initial preparation of the hard disk, before the disk is formatted. Also called a volume.

partition boot sector  Sector of a partition that stores information important to its partition, such as the location of the OS boot files. Responsible for loading the OS on a partition.

partition table  Table located in the boot sector of a hard drive that lists every partition on the disk that contains a valid operating system.

partitioning  Electronically subdividing a physical drive into one or more units called partitions (or volumes).

passcode lock  Mobile device security feature that requires you enter a series of letters, numbers, or motion patterns to unlock the mobile device each time you press the power button.

password  Key used to verify a user’s identity on a secure computer or network.

password manager  Software that uses strong encryption to protect stored passwords, removing the need to remember all the various and complex passwords a person uses for their various online accounts.

patch  Small piece of software released by a software manufacturer to correct a flaw or problem with a particular piece of software. Also called an update.

patch cables  Short (typically two- to five-foot) UTP cables that connect patch panels to a switch or router.

patch management  Process of keeping software updated in a safe, timely fashion.

patch panel  A panel containing a row of female connectors (ports) that terminate the horizontal cabling in the equipment room. Patch panels facilitate cabling organization and provide protection to horizontal cabling.

path  Route the operating system must follow to find an executable program stored in a subfolder.

pattern lock  Mobile device screen lock that requires the user to swipe a certain pattern in order to be authenticated and unlock the device.

PCI (Peripheral Component Interconnect)  Design architecture for the expansion bus on the computer motherboard that enabled system components to be added to the computer. Used parallel communication, and was replaced by PCIe.

PCI DSS (Payment Card Industry Data Security Standard)  A standard that sets common rules for systems that accept, process, transmit, or store credit/debit card payments. Often referred to as just PCI.

PCIe (PCI Express)  Serialized successor to PCI and AGP that uses the concept of individual data paths called lanes. May use any number of lanes, although a single lane (×1) and 16 lanes (×16) are the most common on motherboards.

PCIe 6/8-pin power connector  Connector on some power supplies for powering a dedicated graphics card.

peer-to-peer network  Network in which each machine can act as both a client and a server.

Performance  Tab in Task Manager that tracks PC performance, including CPU usage, available physical memory, size of the disk cache, and other details about memory and processes.

Performance Monitor (perfmon.msc)  Windows tool for tracking system resources over time.

Performance Options  Tool that enables users to configure CPU, RAM, and virtual memory settings.

peripheral  Any device that connects to the system unit.

permission propagation  Describes what happens to permissions on an object, such as a file or folder, when you move or copy it.

personal area network  See PAN.

Personalization (Windows Settings)  Windows Settings category that enables users to configure preferences such as the background picture for both the desktop and lock screen, colors of interface elements, themes, which elements show on the Start screen, and so on.

personally identifiable information (PII)  Any data that can lead back to a specific individual.

PGA (pin grid array)  Arrangement of a large number of pins extending from the bottom of the CPU package into corresponding holes in the CPU socket.

Phillips-head screwdriver  Most important part of a PC tech’s toolkit.

phishing  A social engineering attack intended to get people to give their usernames, passwords, or other security information by pretending to be someone else electronically.

physical security  Security measures intended to protect facilities and systems from physical threats like unauthorized entry, burglary, or other threats.

ping  Command-line utility used to send a “ping” message to another computer, which can be used to verify another system is on the network, spot potential DNS issues, identify latency problems, and so on.

Pinwheel of Death  See Spinning Pinwheel of Death.

pipe  Command-line operator that uses the | symbol to “pipe” output from one command to another, instead of printing it to the screen.

pipeline  Processing methodology where multiple calculations take place simultaneously by being broken into a series of steps. Often used in CPUs and video processors.

pixel (picture element)  In computer graphics, smallest element of a display space that can be independently assigned color or intensity.

pixels per inch (PPI)  Density of pixels on a display or a light sensor; the higher the density, the greater the resolution.

PKI (public key infrastructure)  Authentication schema where public keys are exchanged between all parties using digital certificates, enabling secure communication over public networks.

Platform as a Service (PaaS)  Cloud-based virtual server(s) combined with a platform that gives programmers the tools needed to deploy, administer, and maintain a Web application.

plenum  Space in the ceiling, walls, and floor where special plenum-grade (fire-retardant) network cables can be run out of sight.

plug and play (PnP)  Combination of smart PCs, smart devices, and smart operating systems that automatically configure all necessary system resources and ports when you install a new peripheral device.

policies  Control permission to perform a given action, such as accessing a command prompt, installing software, or logging on at a certain time of day. Contrast with true permissions, which control access to specific resources.

POP3 (Post Office Protocol 3)  One of the two protocols that receive e-mail from SMTP servers. POP3 uses TCP port 110. While historically most e-mail clients used this protocol, the IMAP4 e-mail protocol is now more common.

port (networking)  In networking, the number used to identify the requested service (such as SMTP or FTP) when connecting to a TCP/IP host. Examples include application protocol ports such as 80 (HTTP), 443, (HTTPS), 21 (FTP), 23 (Telnet), 25 (SMTP), 110 (POP3), 143 (IMAP), and 3389 (RDP).

port (physical connection)  Part of a connector into which a plug is inserted. Physical ports are also referred to as jacks.

port forwarding  Router configuration that enables outside traffic to reach a particular node on a secured network, such as a server. Port forwarding translates the IP address and port number used to reach the network by a remote client into the IP address and port number used by a particular node on the network.

port replicator  Device that plugs into a USB port or Thunderbolt port and offers common PC ports, such as VGA, HDMI, USB, network, and so on. Plugging a laptop into a port replicator can instantly connect the computer to nonportable components such as a printer, scanner, monitor, or full-sized keyboard. Port replicators are typically used at home or in the office with the nonportable equipment already connected.

portable battery recharger  Device containing a rechargeable battery that can be used to charge other devices, typically over USB, when no outlets are available.

POST (power-on self-test)  Basic diagnostic routine completed by a system at the beginning of the boot process to make sure a display adapter and the system’s memory are installed. In the event that there is some problem with the hardware, you’ll generally hear some combination of beeps indicating where the problem is; consult the motherboard book. It then searches for an operating system. If it finds one, it hands over control of the machine to the OS.

POST card  Device installed into a motherboard expansion slot that assists in troubleshooting boot problems by providing a two-digit code indicating the stop of the boot process where the problem is occurring.

potential  The amount of electrical energy stored in an object.

power conditioning  Ensuring and adjusting incoming AC wall power to as close to standard as possible. Most UPS devices provide power conditioning.

power management  Cooperation between hardware, BIOS, and OS to reduce power consumption.

Power Options  Windows Control Panel applet that enables better control over power use by customizing a Balanced, Power saver, or High-performance power plan.

Power over Ethernet (PoE)  Technology that provides power and data transmission through a single network cable.

power plan  Preconfigured profiles (such as Balanced, High performance, and Power saver) in the Power Options applet that modify a Windows system’s behavior to adjust power consumption.

power supply unit (PSU)  Provides the electrical power for a PC. Converts standard AC power into various voltages of DC electricity in a PC.

Power Users group  After Administrator/Administrators, the second most powerful account and group type in Windows. Power users have differing capabilities in different versions of Windows.

power-saving modes  Special power modes that limit or modify device functionality in order to prolong battery life. May take steps such as disabling communications, reducing processor speed, limiting programs, and dimming the screen.

PowerShell  See Windows PowerShell.

preboot execution environment (PXE)  Technology that enables a PC to boot without any local storage by retrieving an OS from a server over a network.

primary partition  Partition on a Windows hard drive that can store a bootable operating system.

principle of least privilege  Accounts should have permission to access only the resources they need and no more.

print server  Server, computer, or standalone network device that shares access to a printer over a network.

printed circuit board (PCB)  Copper etched onto a nonconductive material and then coated with some sort of epoxy for strength.

Privacy (Windows Settings)  Windows Settings category that contains options related to privacy.

private cloud  Cloud network built and maintained by or explicitly for a specific company or organization. Often onsite, but may be provided by a third party. While a public cloud network often requires more expertise and costs more, especially up front, it also enables greater customization and security.

PRL (Preferred Roaming List)  A list that is occasionally and automatically updated to a phone’s firmware by the carrier so that the phone will be configured with a particular carrier’s networks and frequencies, in a priority order, that it should search for when it can’t locate its home carrier network.

Processes  Tab in Task Manager that lists all running processes on a system. Frequently a handy tool for ending buggy or unresponsive processes.

product key  Code used during installation to verify legitimacy of the software.

profile (MDM)  A collection of mobile device management (MDM) configuration and security settings that an administrator has created in order to apply those settings to particular categories of users or devices.

profile (network)  Collection of information necessary to automatically connect to a network, stored by the network’s SSID. Enables mobile and portable devices to easily use many networks.

profile (user)  Describes a Windows user account’s customized environment, including Desktop preferences, color schemes, shortcuts, and so on.

program/programming  Series of binary electronic commands sent to a CPU to get work done.

Programs and Features  Windows Control Panel applet; enables uninstalling or changing program options and altering Windows features.

projector  Device for projecting video images from PCs or other video sources, usually for audience presentations.

prompt  A character or message provided by an operating system or program to indicate that it is ready to accept input.

proprietary  Technology unique to a particular vendor.

proprietary crash screen  A screen, differing between operating systems, that indicates an NMI. See also BSoD and Spinning Pinwheel of Death.

protected health information (PHI)  Personally identifiable information that relates to a person’s health status, medical records, and healthcare services they have received.

protocol  Agreement that governs the procedures used to exchange information between cooperating entities. Usually includes how much information is to be sent, how often it is to be sent, how to recover from transmission errors, and who is to receive the information.

proxy server  Software that enables multiple connections to the Internet to go through one protected computer. Common security feature in the corporate world. Applications that want to access Internet resources send requests to the proxy server instead of trying to access the Internet directly, which both protects the client computers and enables the network administrator to monitor and restrict Internet access.

ps  Linux command for listing all processes running on the computer.

public cloud  Cloud network built and maintained by a large company for use by any individual or company who wants to create an account and start paying for services.

Public folder  Folder that all users can access and share with all other users on the system or network.

public key infrastructure  See PKI.

punchdown block  Connector used to connect UTP cable to a patch panel. Wires are attached to the block using a punchdown tool.

punchdown tool  A specialized tool for connecting UTP wires to a punchdown block.

PVC (polyvinyl chloride)  Material used to make the plastic protective sheathing around many basic network cables. Produces noxious fumes when burned.

pwd  Linux command that displays the user’s current path.

QR scanner  An application or device capable of scanning and interpreting QR codes.

quad-channel architecture  Feature similar to dual-channel RAM, but making use of four sticks of RAM instead of two.

Quality of Service (QoS)  Router feature used to prioritize access to network resources. Ensures certain users, applications, or services are prioritized when there isn’t enough bandwidth to go around by limiting the bandwidth for certain types of data based on application protocol, the IP address of a computer, and all sorts of other features.

quick format  High-level formatting that creates just the file allocation table and a blank root directory. See also formatting.

radio frequency (RF)  The part of the electromagnetic spectrum used for radio communication.

radio frequency identification (RFID)  Wireless technology that uses small tags containing small amounts of digital information, and readers capable of accessing it. Passive RFID tags operate by harvesting some of the power a scanner or reader emits, enabling a vast array of applications. Common uses such as tracking inventory, identifying lost pets, contactless payments, authentication, and wireless door locks are just scratching the surface. See also asset tag, ID badge, key fob, and smart card.

RAID (redundant array of independent [or inexpensive] disks)  Method for creating a fault-tolerant storage system. RAID uses multiple hard drives in various configurations to offer differing levels of speed/data redundancy.

RAID 0  Uses byte-level striping and provides no fault tolerance.

RAID 0+1  A RAID 0 configuration created by combining two RAID 1 arrays. Provides both speed and redundancy, but requires at least four disks.

RAID 1  Uses mirroring or duplexing for increased data redundancy.

RAID 5  Uses block-level and parity data striping. Requires three or more drives.

RAID 5 volume (dynamic disks)  A software-based RAID 5 volume made up of three or more dynamic disks with equal-sized unallocated space. Created with Windows Disk Management.

RAID 6  Disk striping with extra parity. Like RAID 5, but with more parity data. Requires four or more drives, but you can lose up to two drives at once and your data is still protected.

RAID 10  The opposite of RAID 0+1, two mirrored RAID 0 configurations. Provides both speed and redundancy, and also requires four disks.

RAM (random access memory)  Memory that can be accessed at random—that is, memory that you can write to or read from without touching the preceding address. This term is often used to mean a computer’s main memory.

ransomware  A nasty form of malware that encrypts data or drives on the infected system and demands payment, often within a limited timeframe, in exchange for the keys to decrypt the data.

rapid elasticity  Characteristic of cloud computing that enables cloud consumers to add or remove capacity quickly. Because cloud servers are powered by virtual machines, customers can start or shut down new instances of VMs or move the VMs to more powerful hardware.

rd (rmdir)  Command-line tool used to remove directories.

read-only attribute  File attribute that does not allow a file to be altered or modified. Helpful when protecting system files that should not be edited.

real-time clock (RTC)  Device within the CMOS memory chip that provides date and time information to the computer and operating system.

recent apps  Interface for viewing a list of recently used apps on a mobile device.

reciprocity  See Ethic of Reciprocity.

recovery partition  Small hidden partition on a system’s primary hard drive with a factory-fresh OS image to recover and reinstall from.

Recycle Bin  Location to which files are moved when they are deleted from a modern Windows system. To permanently remove files from a system, they must be emptied from the Recycle Bin.

refresh rate  Time required for a monitor to redraw the whole screen.

regedit.exe  Program used to edit the Windows Registry.

registration (printing)  Describes how accurately the printer lays down each color layer that makes up a page or image. Poor registration can result in muddled colors or a fringe of pure color around a shape or image. Printers usually have a routine (which may mention calibration, alignment, or registration) for detecting and fixing alignment issues.

registration (product)  Usually optional process that identifies the legal owner/user of the product to the supplier.

Registry  Complex binary file used to store configuration data about a particular Windows system. To edit the Registry, users can use the Registry Editor or use regedit.

Registry Editor (regedit.exe)  Program used to edit the Windows Registry.

remediation  Repairing damage caused by a virus.

remnant  Potentially recoverable data on a hard drive that remains despite formatting or deleting.

Remote Assistance  See Microsoft Remote Assistance.

remote desktop  Generically, the process of using one system to access the desktop or graphical user interface (GUI) of a remote system.

Remote Desktop Connection  Windows tool used to form a remote desktop connection and graphically access the GUI of a remote system.

Remote Desktop Protocol (RDP)  Protocol used for Microsoft’s Remote Desktop tool. Uses port 3389.

remote network installation  A common method of OS installation where the source files are placed in a shared directory on a network server. Then, a tech who needs to install a new OS can boot the computer, connect to the source location on the network, and start the installation from there.

remotely wipe  The ability to remotely delete user data from a mobile device that has been lost or stolen.

removable media  Any storage on a computer that can be easily removed. For example, optical discs, flash drives, or memory cards.

Remove everything  Windows Recovery Environment option in Windows 10 that deletes all apps, programs, user files, and user settings, resulting in a fresh installation of Windows. Use as a last resort when troubleshooting (and back up data first).

replication  When a virus makes copies of itself, often by injecting itself into other executables. See malware and virus.

reset to factory default  Another term for a factory reset.

resistance  Difficulty in making electricity flow through a material, measured in ohms.

resistor  Any material or device that impedes the flow of electrons. Antistatic wrist straps and mats use tiny resistors to prevent a static charge from racing through the device.

resolution  Measurement for monitors and printers expressed in horizontal and vertical dots or pixels. Higher resolutions provide sharper details and thus display better-looking images.

Resource Monitor (resmon.exe)  Windows utility that displays detailed performance information about a computer’s CPU, memory, disk, and network activity.

resources  Data and services such as files, folders, drives, printers, connections, and so on.

response rate  The amount of time it takes for all the sub-pixels on an LCD panel to change from one state to another. This change is measured in one of two ways: black-to-white (BtW) measures how long it takes the pixels to go from pure black to pure white and back again, and gray-to-gray (GtG) measures how long it takes the pixels to go from one gray state to another.

restore point  A snapshot of a computer’s configuration at a specific point in time, created by the System Restore utility and used to restore a malfunctioning system. See also System Restore.

retina scanner  Biometric security device that authenticates an individual by comparing retinal scans. Rarer in the real world than in media such as movies or video games.

RFI (radio frequency interference)  Another form of electrical interference caused by radio wave–emitting devices, such as cell phones, wireless network cards, and microwave ovens.

RG-6  Coaxial cabling used for cable television. It has a 75-ohm impedance and uses an F-type connector.

RG-59  Coaxial cable used for cable television, cable modems, and broadcast TV; thinner than RG-6, which makes it suitable for shorter patch cables.

riser card  Special adapter card, usually inserted into a special slot on a motherboard, that changes the orientation of expansion cards relative to the motherboard. Riser cards are used extensively in slimline computers to keep total depth and height of the system to a minimum. Sometimes called a daughter board.

risk analysis  A detailed assessment of any problems that could result from a change.

RJ (registered jack) connector  UTP cable connector, used for both telephone and network connections. RJ-11 is a connector for four-wire UTP; usually found in telephone connections. RJ-45 is a connector for eight-wire UTP; usually found in network connections.

RJ-11  See RJ (registered jack) connector.

RJ-45  See RJ (registered jack) connector.

rm  Linux command for deleting files.

rmdir  See rd (rmdir).

roaming  When a mobile device connects to a network not owned by its home carrier.

robocopy  Powerful command-line utility for copying files and directories, even over a network.

rogue anti-malware  Free application that claims to be anti-malware but is actually malware.

ROM (read-only memory)  Generic term for nonvolatile memory that can be read from but not written to. This means that code and data stored in ROM cannot be corrupted by accidental erasure. Additionally, ROM retains its data when power is removed, which makes it the perfect medium for storing BIOS data or information such as scientific constants.

root directory  Directory that contains all other directories. Also known as root folder.

root keys  Five main categories in the Windows Registry:

•   HKEY_CLASSES_ROOT

•   HKEY_CURRENT_USER

•   HKEY_LOCAL_MACHINE

•   HKEY_USERS

•   HKEY_CURRENT_CONFIG

rooting  Process for circumventing the security restrictions and gaining access to the root user account on an Android device.

rootkit  Program that takes advantage of very low-level functionality to gain privileged system access and hide itself from all but the most aggressive anti-malware tools. Can strike operating systems, hypervisors, and even device firmware.

router  Device connecting separate networks; forwards a packet from one network to another based on the network address for the protocol being used. For example, an IP router looks only at the IP network number. Routers operate at Layer 3 (Network) of the OSI seven-layer model.

RSA token  Random-number generator used along with a username and password to enhance security.

RU (rack mounted unit)  Height measurement used for rack-mounted equipment. An RU is 1.75 inches. A device that fits in a 1.75-inch space is called a 1RU; a device designed for a 3.5-inch space is a 2RU; and a device that goes into a 7-inch space is called a 4RU.

run (networking)  A single piece of installed horizontal cabling.

Run as administrator  Method of running a Windows program with elevated privileges, disabling protections that normally limit a program’s ability to damage the system.

SaaS  See Software as a Service.

Safe Mode  Important diagnostic boot mode for Windows that runs only very basic drivers and turns off virtual memory.

safety goggles  Protective glasses that keep stuff out of your eyes.

salted hash  See salting.

salting  The process of protecting password hashes from being easily reversed with a rainbow table by adding additional values to each password before hashing and storing it.

SAN  See storage area network.

sandbox  Virtualized computer used as a restricted environment to safely run untrusted applications or test new applications without posing risk to an actual system or network.

SAS (Serial Attached SCSI)  Fast, robust storage interface based on the SCSI command set. Also supports SATA drives. Used mainly in servers and storage arrays.

SATA (serial ATA)  Serialized version of the ATA standard that offers many advantages over PATA (parallel ATA) technology, including thinner cabling, keyed connectors, and lower power requirements.

SATA 3.2  Another term for SATAe. See SATA Express.

SATA Express (SATAe)  Version of SATA that ties capable drives directly into the PCI Express bus on motherboards. Each lane of PCIe 3.0 is capable of handling up to 8 Gbps of data throughput. A SATAe drive grabbing two lanes, therefore, could move a whopping 16 Gbps through the bus.

SATA power connector  15-pin, L-shaped connector used by SATA devices that support the hot-swappable feature.

SC  See subscriber connector.

SCADA  See supervisory control and data acquisition.

scope of the change  Defines who and what the change will affect. May include an inventory of systems to change, people involved, time required, and estimated cost.

screen lock  Mobile device and Windows feature that locks the screen until some form of authentication challenge is passed.

screen orientation  Describes whether a mobile device screen is in portrait or landscape mode, and the device settings that govern when the orientation may change. When the screen orientation setting is in automatic mode, the user interface (UI) will switch between portrait and landscape modes based on the device’s orientation in physical space.

screened subnet  A lightly protected or unprotected subnet network positioned between an outer firewall and an organization’s highly protected internal network. Screened subnets are used mainly to host public address servers (such as Web servers). Also commonly known as a demilitarized zone (DMZ).

script  Set of text instructions that tells a computer a series of commands to execute in a repeatable fashion.

scripting language  Set of commands, syntax, variables, and format for scripts to be used in a specific computer environment. For example, bash is a scripting language often used in the Bash shell, which is common on UNIX environments.

SCSI (small computer system interface)  Long-lived storage drive technology once common in the server market. Has been through many iterations. Today, the SCSI command set lives on in Serial Attached SCSI (SAS) hard drives. See also SAS.

SDRAM (synchronous DRAM)  Dynamic RAM that is synchronous, or tied to the system clock. This type of RAM is used in all modern systems.

Search (box or field)  Location on the Windows 10 taskbar next to the Start button where users can input text and see relevant suggestions (for settings, programs, files, and popular Web searches).

sector  Magnetically preset storage areas on traditional magnetic hard drives. On older hard drives, a sector held 512 bytes of data; modern drives use 4096-byte Advanced Format (AF) sectors.

Secure Boot  UEFI feature that secures the boot process by requiring properly signed software. This includes boot software and software that supports specific, essential components.

Secure Shell (SSH)  Terminal emulation program similar to Telnet, except that the entire connection is encrypted. Uses port 22.

Secure Sockets Layer (SSL)  Security protocol used by a browser to connect to secure Web sites. Replaced by Transport Layer Security (TLS).

security token  Device that stores some unique information that a user carries with them. May contain digital certificates, passwords, biometric data, or RSA tokens.

segment  The connection between a computer and a switch.

self-grounding  A less-than-ideal method for ridding yourself of static electricity by touching a metal object such as a computer case.

Serial Attached SCSI  See SAS.

serial presence detect (SPD)  Information stored on a RAM chip that describes the speed, capacity, and other aspects of the RAM chip.

server  Computer that shares its resources, such as printers and files, with other computers on a network. Example: network file system server that shares its disk space with a workstation that does not have a disk drive of its own.

Server Message Block (SMB)  Windows’ network file and print sharing protocol, though every major OS now supports it. Protocol of choice for LAN file servers. Uses TCP port 445 and UDP ports 137, 138, and 139.

service  A process that runs in the background of a PC but displays no icons anywhere. You can view a list of services in the Windows Task Manager. Also, a program stored in a ROM chip.

service menu  Hidden device menu containing tools for technicians servicing the device. May contain diagnostics, reports, or interfaces for changing otherwise inaccessible settings.

service pack  Collection of software patches released at one time by a software manufacturer.

Services  Tab in Windows Task Manager that lists all running services on a system. See also service.

Settings app  Windows app that combines a huge number of otherwise disparate utilities, apps, and tools traditionally spread out all over your computer into one fairly unified, handy interface.

sfc (System File Checker)  Command-prompt program (sfc.exe) that scans, detects, and restores Windows system files, folders, and paths.

SFTP (Secure FTP)  Secure version of the File Transfer Protocol (FTP) that uses port 22. See also FTP.

shared resources  Consolidating resources from many systems into a smaller number of more powerful systems, reducing power, maintenance, and hardware costs.

shell  Tool that interprets command-line input, also known as the command-line interpreter.

shielded twisted pair  See STP.

shoulder surfing  Social engineering attack where a malicious actor obtains credentials or other sensitive information by watching someone use a computer or device, often over their shoulder.

shunt  Tiny connector of metal enclosed in plastic that creates an electrical connection between two posts of a jumper. Also known as a jumper block.

shutdown  Windows and Linux command-line tool for shutting down the computer.

SID (security identifier)  Unique identifier for every PC that most techs change when cloning.

side-by-side apps  Windows feature for quickly pinning an app to the left or right half of a screen.

signature (malware)  Code pattern of a known virus or malware that antivirus/anti-malware software uses to detect malware.

signature file  See definition file.

signed driver  A driver designed specifically to work with Windows that has been tested and certified by Microsoft to work stably with Windows.

Simple Mail Transport Protocol  See SMTP.

Simple Network Management Protocol  See SNMP.

simple space  Storage Space that just pools storage space, like just a bunch of disks (JBOD). See Storage Spaces.

simple volume  Volume created when setting up dynamic disks. Acts like a primary partition on a dynamic disk.

single sign-on (SSO)  Process that uses an account or credentials for a popular service (such as a Google Account) to sign on or authenticate with other services.

single-factor authentication  A less-secure authentication process using only one of the authentication factors. See also multifactor authentication.

single-mode fiber optic cabling  Type of fiber optic cabling that uses laser light to transmit at very high rates over long distances. Still fairly rare. See also fiber optic cable.

single-sided RAM  Has chips on only one side, as opposed to double-sided RAM.

sleep mode  Power management setting in which all data from RAM is preserved by powering down much of the computer but maintaining power to RAM, or by writing the contents of RAM to the mass storage drive before the system goes into a reduced-power mode. Upon waking up, the information is retrieved from the HDD or SSD and returned to RAM if necessary; the system continues where it left off.

slot covers  Metal plates that cover up unused expansion slots on the back of a PC. Useful in maintaining proper airflow through a computer case.

S.M.A.R.T. (Self-Monitoring, Analysis, and Reporting Technology)  Monitoring system built into hard drives that tracks errors and error conditions within the drive.

smart card  Hardware authentication involving a credit card–sized card with circuitry that can be used to identify the bearer of that card.

smart card reader  Device that scans the smart card chip, such as those in ID badges. Common applications include enhancing the security of doors or laptops.

smartphone  A cell phone enhanced to do things formerly reserved for desktop and laptop computers, such as Web browsing, document viewing, and media consumption.

SMTP (Simple Mail Transport Protocol)  Main protocol used to send electronic mail on the Internet. Uses port 25.

snap-ins  Utilities that can be used with the Microsoft Management Console.

snapshot  Virtualization feature that enables you to save an extra copy of the virtual machine as it is exactly at the moment the snapshot is taken.

SNMP (Simple Network Management Protocol)  A set of standards for communication with devices connected to a TCP/IP network. Examples of these devices include routers, hubs, and switches. Uses ports 161 and 162.

social engineering  Using or manipulating people inside the networking environment to gain access to that network from the outside.

SO-DIMM (small-outline DIMM)  Memory used in portable PCs because of its small size.

soft power  Characteristic of ATX motherboards, which can use software to turn the PC on and off. The physical manifestation of soft power is the power switch. Instead of the thick power cord used in AT systems, an ATX power switch is little more than a pair of small wires leading to the motherboard.

soft reset  The equivalent of a reboot or restart for a mobile device. An important troubleshooting step because it clears running programs from memory and restarts the operating system. Some portable devices that closely resemble mobile devices may also use soft resets.

soft token  Programming (usually running on a general computing device such as a smartphone or portable computer) that enables the device to serve as an authentication factor when logging on to a secure resource.

software  Single group of programs designed to do a particular job; always stored on mass storage devices.

Software as a Service (SaaS)  Cloud-based service to store, distribute, and update programs and applications. The SaaS model provides access to necessary applications wherever you have an Internet connection, often without having to carry data with you or regularly update software. At the enterprise level, the subscription model of many SaaS providers makes it easier to budget and keep hundreds or thousands of computers up to date.

software firewall  Firewall implemented in software running on servers or workstations. See firewall.

software-defined networking (SDN)  Networking method that uses software tools to control network administration and traffic. SDN allows for the programming of the network to improve efficiency.

solid core  A cable that uses a single solid (not hollow or stranded) wire to transmit signals.

solid-state drive  See SSD.

spam  Unsolicited e-mails from both legitimate businesses and scammers that account for a huge percentage of traffic on the Internet.

spam gateway  Software used to filter incoming e-mail to prevent spam.

spanned volume  Volume that uses space on multiple dynamic disks.

SPD  See serial presence detect.

speaker  Device that outputs sound by using a magnetically driven diaphragm.

spear phishing  Dangerous targeted phishing attack on a group or individual that carefully uses details from the target’s life to increase the odds they’ll take the bait.

spindle speed  Fixed speed in revolutions per minute (RPM) at which a given HDD’s platters spin. The two most common speeds are 5400 and 7200 RPM; higher-performance drives (far less common) run at 10,000 and 15,000 RPM. Also called rotational speed.

Spinning Pinwheel of Death (SPoD)  A spinning rainbow wheel (sometimes referred to as a “beach ball”) that serves as the macOS indicator that an application isn’t responding and may be busy or frozen.

spoofing  Pretending to be someone or something else by placing false information into packets. Commonly spoofed data include a source MAC address or IP address, e-mail address, Web address, or username. Generally a useful tool for enhancing or advancing other attacks, such as social engineering or spear phishing.

spyware  Software that runs in the background of a user’s PC, sending information about browsing habits back to the company that installed it onto the system.

SQL attack  See Structured Query Language (SQL) attack.

SRAM (static RAM)  Very high-speed RAM built into CPUs that reduces wait states by preloading as many instructions as possible and keeping copies of already run instructions and data in case the CPU needs to work on them again.

SSD (solid-state drive)  Data storage device that uses flash memory to store data.

SSH  See Secure Shell.

SSID (service set identifier)  Parameter used to define a wireless network; otherwise known as the network name.

SSL  See Secure Sockets Layer.

ST  See straight tip.

standard user account  User account in Windows that has limited access to a system. Part of the Users group. Accounts of this type cannot alter system files, cannot install new programs, and cannot edit some settings by using the Control Panel without supplying an administrator password.

standby  See sleep mode.

standoffs  Small mechanical separators that screw into a computer case. A motherboard is then placed on top of the standoffs, and small screws are used to secure it to the standoffs.

star bus topology  A hybrid network topology where the computers all connect to a central bus—a switch—and have a layout resembling a star.

Start button  Clickable element on the Windows taskbar that enables access to the Start menu.

Start menu  Menu that can be accessed by clicking the Start button on the Windows taskbar. Enables you to see all programs loaded on the system and to start them.

Start screen  Windows 10 version of the Start menu, which functions as a combination of the traditional Start menu and Windows 8/8.1 Modern UI.

Startup Repair  A one-stop, do-it-all troubleshooting option that performs a number of boot repairs automatically.

Stateful Packet Inspection (SPI)  Used by hardware firewalls to inspect each incoming packet individually for purposes such as blocking traffic that isn’t in response to outgoing requests.

static IP address  Manually set IP address that will not change.

storage area network (SAN)  Storage setup in which, rather than using internal drives, a device accesses a separate block of hard drives on a network separate from the normal network, reading them logically as one drive.

storage pool  One or more physical drives grouped into a single Storage Space.

Storage Spaces  In Windows, a software RAID solution that enables users to group multiple drives into a single storage pool.

STP (shielded twisted pair)  Cabling for networks, composed of pairs of wires twisted around each other at specific intervals. Twists serve to reduce interference (also called crosstalk)—the more twists, the less interference. Cable has metallic shielding to protect the wires from external interference.

straight tip (ST)  Type of fiber optic connector. See fiber optic cable.

stranded core  A cable that uses a bundle of tiny wire filaments to transmit signals. Stranded core is not quite as good a conductor as solid core, but it will stand up to substantial handling without breaking.

streaming media  Broadcast of data that is played on your computer and immediately discarded.

string  In programming and scripting, a non-numeric sequence of alphanumeric data.

stripe set  Two or more drives in a group that are used for a striped volume.

striped volume  RAID 0 volumes. Data is spread across two drives for increased speed.

strong password  Password containing at least eight characters, including letters, numbers, and punctuation symbols.

structured cabling  ANSI/TIA standards that define methods of organizing the cables in a network for ease of repair and replacement.

Structured Query Language (SQL)  A language that enables a program to interact with a database using various commands and queries.

Structured Query Language (SQL) attack  An attack that occurs when an attacker enters SQL commands into an input field on a Web app in order to gain access to data or an entire database that the attacker isn’t supposed to see.

su  Older Linux command for gaining root access.

subfolder  A folder located inside another folder.

subnet mask  Value used in TCP/IP settings to divide the IP address of a host into its component parts: network ID and host ID.

sub-pixels  Tiny liquid crystal molecules arranged in rows and columns between polarizing filters used in LCDs. A pixel is composed of a red, a green, and a blue sub-pixel.

subscriber connector (SC)  Type of fiber optic connector. See fiber optic cable.

su/sudo  Linux command for gaining root access.

SuperSpeed USB  A fast form of USB, with speeds up to 5 Gbps. Also called USB 3.0, USB 3.1 Gen 1, or USB 3.2 Gen 1.

SuperSpeed USB 10 Gbps  Updated form of SuperSpeed USB providing speeds up to 10 Gbps. Also called USB 3.1 or USB 3.2 Gen 2.

supervisory control and data acquisition (SCADA)  Hardware and software combination used to monitor and control the operational technology used in industrial settings such as public transit systems, power plants, and refineries.

surge suppressor  Inexpensive device that protects your computer from voltage spikes.

suspend  See sleep mode.

swap file  See virtual memory.

swap partition  Special partition found on Linux and UNIX systems that behaves like RAM when your system needs more RAM than is installed.

swipe lock  Mobile device feature that uses a swipe gesture to unlock the mobile device.

switch  Device that filters and forwards traffic based on some criteria. A bridge and a router are both examples of switches. In the command-line interface, a switch is a function that modifies the behavior of a command.

swollen battery  A Li-Ion battery that has begun to swell as it fails, often due to manufacturing defects, heat, or overcharging. May also deform the device containing it. It is an explosion and fire risk if it ruptures, so dispose of it quickly and safely.

sync  The process of keeping files on mobile devices up to date with the versions on desktop computers or over the Internet via cloud-based services.

Sync Center  Windows Control Panel applet where network files marked as Always available offline may be viewed.

synchronize  See sync.

syntax (command)  The proper way to write a command-line command so that it functions and does what it’s supposed to do.

System (Windows Settings)  The proverbial “junk drawer” category of Windows Settings categories. System contains everything from display options, to sound settings, to notifications settings.

system BIOS  Primary set of BIOS stored on a flash ROM chip on the motherboard. Defines the BIOS for all the assumed hardware on the motherboard, such as keyboard controller, basic video, and RAM.

system bus speed  Speed at which the CPU and the rest of the PC operates; set by the system crystal.

System Configuration (msconfig.exe)  Windows tool to edit and troubleshoot operating system and program startup processes and services.

system crystal  Crystal that provides the speed signals for the CPU and the rest of the system.

system fan  Any fan controlled by the motherboard but not directly attached to the CPU.

System File Checker  See sfc.

System Information tool  See msinfo32.

system lockout  Protects against attempts to brute-force a lock screen or login system by locking the user out until they perform some more thorough authentication process. Occurs when too many consecutive login attempts fail.

system on a chip (SoC)  Single silicon die containing a CPU, GPU, and other important support logic.

System Preferences  macOS tool containing many administrative functions.

System Protection  Tab in Windows System Properties dialog box that enables you to configure how and when the system will create restore points and provides easy access to existing restore points via System Restore.

system resources  In classic terms, the I/O addresses, IRQs, DMA channels, and memory addresses. Also refers to other computer essentials such as hard drive space, system RAM, and processor speed.

System Restore  Utility in Windows that enables you to return your PC to a recent working configuration when something goes wrong. System Restore enables you to select a restore point and then returns the computer’s system settings to the way they were at that restore point—all without affecting your personal files or e-mail.

system ROM  Flash ROM chip that stores the system BIOS.

system setup utility  See CMOS setup program.

system tray  See notification area.

system unit  Main component of the desktop PC, in which the CPU, RAM, optical drive, hard drive, and power supply reside. All other devices—the keyboard, mouse, and monitor—connect to the system unit.

system/application log errors  May indicate the presence of a malware infestation and the scope of its effects.

%SystemRoot%  The path where the operating system is installed.

T568A  Wiring standard for Ethernet cable.

T568B  Wiring standard for Ethernet cable.

tablet  A mobile device consisting of a large touchscreen, enabling the user to browse the Web, view media, and even play games.

tailgating  Form of infiltration and social engineering that involves following someone else through a door as if you belong in the building.

Take Ownership  Special permission allowing users to seize control of a file or folder and potentially prevent others from accessing the file/folder.

Task Manager  Windows utility that shows all running programs, including hidden ones, and is accessed by pressing CTRL-SHIFT-ESC. You can use the Task Manager to shut down an unresponsive application that refuses to close normally.

Task Scheduler (taskschd.msc)  Windows utility enabling users to set tasks to run automatically at certain times.

taskbar  Contains the Start button, Search box, pinned apps, running apps, and the notification area. Located by default at the bottom of the desktop.

taskkill  Windows command-line tool for killing running processes.

tasklist  Windows command-line tool for listing and managing processes.

TCP  See Transmission Control Protocol.

TCP/IP (Transmission Control Protocol/Internet Protocol)  Communication protocols developed by the U.S. Department of Defense to enable dissimilar computers to share information over a network. TCP/IP is the primary protocol of most modern networks, including the Internet.

TCP/IP services  Services such as HTTP or SSH that run atop TCP/IP.

TDR (time-domain reflectometer)  Device for testing network cabling by measuring impedance (which is similar to resistance); any impedance means a bad cable.

tech toolkit  Tools a PC tech should never be without, including a Phillips-head screwdriver, a pair of plastic tweezers, a flat-head screwdriver, a hemostat, a star-headed Torx wrench, a parts retriever, and a nut driver or two.

telecommunications room  Area where all the cabling from individual computers in a network converges.

Telnet  Terminal emulation program for TCP/IP networks that allows one machine to control another as if the user were sitting in front of it. Uses port 23.

tera-  Prefix that usually stands for the binary number 1,099,511,627,776 (240). When used for mass storage, it’s often shorthand for 1 trillion bytes.

terminal  Dumb device connected to a mainframe or computer network that acts as a point for entry or retrieval of information.

Terminal  A command-line tool available in macOS and various Linux distros.

terminal emulation  Software that enables a computer to communicate with another computer or network as if the computer were a specific type of hardware terminal.

test the theory to determine the cause  Attempt to resolve the issue by either confirming the theory and learning what needs to be done to fix the problem, or by not confirming the theory and forming a new one or escalating. (Step 3 of 6 in the CompTIA troubleshooting methodology.)

tethering  The act of using a cellular network–connected mobile device as a mobile hotspot.

theory of probable cause  One possible reason why something is not working; a guess or hypothesis.

thermal compound  See thermal paste.

thermal pad  Heat-transferring pad that can be used as an alternative to thermal paste. Typically preapplied to OEM heat sinks supplied with processors and covers for M.2 drives.

thermal paste  Paste-like material with very high heat-transfer properties. Applied between the CPU and the cooling device, it ensures the best possible dispersal of heat from the CPU. Also called heat dope or thermal compound.

thermal printer  Printer that uses heated printheads to create high-quality images on special or plain paper. Common in retail receipt printers, which use large rolls of thermal paper housed in a feed assembly that automatically draws the thermal receipt paper over the heating element.

thin provisioning  Creating a Storage Space that reports a size greater than the actual capacity installed in the computer, with the ability to later add more physical capacity up to the reported size. See also Storage Spaces.

This PC  Commonly used interface for Windows Explorer that displays hard drives and devices with removable storage.

thread  Smallest logical division of a single program.

throttling  Power reduction/thermal control capability allowing CPUs to slow down during low activity or high heat build-up situations.

throw  Size of the image a projector displays at a certain distance from the screen.

Thunderbolt  An open standards connector interface that is primarily used to connect peripherals to devices, including mobile devices, if they have a corresponding port.

Time & Language (Windows Settings)  Windows Settings category that allows you to change the date, time, and language on a Windows system.

Time Machine  macOS backup tool that enables you to create full system backups, called local snapshots, and to recover some or all files in the event of a crash; it also enables you to restore deleted files and recover previous versions of files.

TLS  See Transport Layer Security.

TN (twisted nematic)  Older technology for LCD monitors. TN monitors produce a decent display for a modest price, but they have limited viewing angles and can’t accurately reproduce all the color information sent by the video card.

tone generator  See toner.

tone probe  See toner.

toner  Generic term for two devices used together—a tone generator and a tone probe (locator)—to trace cables by sending an electrical signal along a wire at a particular frequency. The tone probe then emits a sound when it distinguishes that frequency.

topology  The way computers connect to each other in a network.

touch interface  The primary user interface on modern mobile devices where keys are replaced with tactile interaction.

touch pen  Device designed to be used in conjunction with touchscreens to create a drawing or writing experience. Touch pens can be as simple as a plastic stylus, all the way to the advanced Apple Pencil, which uses sensors and a Bluetooth connection to the device to enhance its effectiveness.

touchscreen  Monitor with a type of sensing device (a digitizer) across its face that detects the location and duration of contact, usually by a finger or stylus.

traceroute  macOS and Linux command-line utility for following the path a packet takes between hosts. The Windows version is named tracert.

tracert  Windows command-line utility used to follow the path a packet takes between two hosts. The utility is traceroute in macOS and Linux.

traces  Small electrical connections embedded in a circuit board.

trackpad  Flat, touch-sensitive pad that serves as a pointing device for most laptops.

transfer rate  Rate of data transferred between two devices, especially over the expansion bus.

Transmission Control Protocol (TCP)  Connection-oriented protocol used with TCP/IP. See also User Datagram Protocol and TCP/IP.

transmit beamforming  Multiple-antenna technology that adjusts the signal when clients are discovered, to optimize quality and minimize dead spots. Employed in many 802.11n WAPs and standard in 802.11ac and 802.11ax WAPs.

Transport Layer Security (TLS)  Encryption protocol used to securely connect between servers and clients, such as when your Web browser securely connects to Amazon’s servers to make a purchase. Replaces SSL.

triple-channel architecture  A chipset feature similar to dual-channel RAM, but making use of three matched sticks of RAM instead of two.

Trojan  Program that does something other than what the user who runs the program thinks it will do. Used to disguise malicious code, also known as a Trojan horse.

troubleshooting methodology  Steps a technician uses to solve a problem. CompTIA A+ defines six steps: identify the problem; establish a theory of probable cause (question the obvious); test the theory to determine the cause; establish a plan of action to resolve the problem and implement a solution; verify full system functionality and, if applicable, implement preventive measures; and document findings, actions, and outcomes.

Trusted Platform Module (TPM)  A hardware platform for the acceleration of cryptographic functions and the secure storage of associated information. BitLocker, for example, requires a TPM chip on the motherboard or equivalent to validate on boot that the computer has not changed. Recent Intel and AMD processors include TPM functions.

trusted root CA  A highly respected certificate authority (CA) that has been placed on the lists of trusted authorities built into Web browsers.

trusted source  Legitimate app stores run by the major OS vendors such as Apple, Google, Microsoft, and Amazon.

tunneling  Creating an encrypted link between two programs on two separate computers.

two-factor authentication  Authentication process that provides additional security by requiring two different authentication factors. See also multifactor authentication.

UAC (User Account Control)  Windows feature implemented to stop unauthorized changes to Windows. UAC enables standard accounts to do common tasks and provides a permissions dialog box when standard and administrator accounts do certain things that could potentially harm the computer (such as attempt to install a program).

UDP  See User Data Protocol.

UEFI (Unified Extensible Firmware Interface)  Modern 32- or 64-bit firmware programming interface. Replaced the original 16-bit PC BIOS. UEFI supports large-capacity storage drives, additional features, and a more direct booting process.

unattended installation  A type of OS installation where special scripts perform all the OS setup duties without human intervention.

unauthorized access  Anytime a person accesses resources in an unauthorized way. This access may or may not be malicious.

UNC (Universal Naming Convention)  Describes any shared resource in a network using the convention \\<server name>\<name of shared resource>.

unified threat management (UTM)  Providing robust network security by integrating traditional firewalls with many other security services such as IPS, VPN, load balancing, anti-malware, and more.

unpatched system  Provides robust network security by integrating traditional firewalls with many other security services such as IPS, VPN, load balancing, anti-malware, and more.

unshielded twisted pair  See UTP.

untrusted source  Stores or sites where apps can be obtained outside of the legitimate trusted sources run by major vendors. See trusted source.

UPC (Universal Product Code)  Barcode used to track inventory.

update  See patch.

Update & Security (Windows Settings)  Windows Settings category that includes options related to Windows updates and security features, including Windows Defender.

upgrade installation  Installation of Windows on top of an earlier installed version, thus inheriting all previous hardware and software settings.

UPS (uninterruptible power supply)  Device that supplies continuous clean power to a computer system the whole time the computer is on. Protects against power outages and sags (and corresponding data loss).

URL (uniform resource locator)  An address that defines the location of a resource on the Internet. URLs are used most often in conjunction with HTML and the World Wide Web.

USB (universal serial bus)  General-purpose serial interconnect for keyboards, printers, joysticks, drives, scanners, and many other devices. Enables hot-swapping of devices.

USB host controller  Integrated circuit normally built into the chipset that acts as the interface between the system and every USB device that connects to it.

USB hub  Device that extends a single USB connection to two or more USB ports, almost always directly from one of the USB ports connected to the root hub.

USB root hub  Part of the host controller that makes the physical connection to the USB ports.

USB thumb drive  Flash memory device that has a standard USB connector.

USB Type-C (connector)  Reversible USB-type cable that supports up to USB 3.2 with a top speed of 10 Gbps. Quickly becoming the de facto standard port on Android devices. Thunderbolt-enabled USB Type-C ports can reach top speeds of 40 Gbps. See also Thunderbolt.

user account  Container that identifies a user to an application, operating system, or network. Includes name, password, username, groups to which the user belongs, and other information based on the user and the OS being used. Usually defines the rights and roles a user plays on a system.

User Accounts  Applet in Control Panel that enables you to make changes to local user accounts, and gives you access to the Settings app when you opt to add a new account.

User Datagram Protocol (UDP)  Connectionless protocol used with TCP/IP. See also Transmission Control Protocol and TCP/IP.

user interface  Visual representation of the computer on the monitor that makes sense to the people using the computer, through which the user can interact with the computer. This can be a graphical user interface (GUI) like Windows 10 or a command-line interface (CLI) like Windows PowerShell.

user password  Credentials assigned to a login account that does not have administrative capabilities.

user profile  Settings that correspond to a specific user account and may follow the user regardless of the computers where they log on. These settings enable the user to have customized environment and security settings.

Users  Tab in Task Manager that shows other logged-in users and enables you to log off other users if you have the proper permissions. Also includes information on resources consumed by programs the user is running.

Users folder  Windows default location for content specific to each user account on a computer. It is divided into several folders such as Documents, Pictures, Music, and Videos.

Users group  List of local users not allowed to edit the Registry or access critical system files, among other things. They can create groups, but can only manage the groups they create.

USMT (User State Migration Tool)  Advanced application for file and settings transfer of many users.

Utilities  macOS folder that contains tools for performing services on a Mac beyond what’s included in System Preferences, including Activity Monitor and Terminal.

UTP (unshielded twisted pair)  Popular type of cabling for telephone and networks, composed of pairs of wires twisted around each other at specific intervals. The twists serve to reduce interference (also called crosstalk). The more twists, the less interference. Unlike shielded twisted pair (STP), UTP cable has no metallic shielding to protect the wires from external interference. 1000BASE-T uses UTP, as do many other networking technologies. UTP is available in a variety of grades, called categories, as follows:

•   Cat 1 UTP Regular analog phone lines—not used for data communications.

•   Cat 2 UTP Supports speeds up to 4 Mbps.

•   Cat 3 UTP Supports speeds up to 16 Mbps.

•   Cat 4 UTP Supports speeds up to 20 Mbps.

•   Cat 5 UTP Supports speeds up to 100 Mbps.

•   Cat 5e UTP Supports speeds up to 1000 Mbps.

•   Cat 6 UTP Supports speeds up to 10 Gbps.

•   Cat 6a UTP Supports speeds up to 10 Gbps.

•   Cat 7 UTP Supports 10-Gbps networks at 100-meter segments; shielding for individual wire pairs reduces crosstalk and noise problems. Cat 7 is not an ANSI/TIA standard.

variables  In scripting and programming, named labels for some portion of in-memory data. The actions taken by the script or program may change or replace the data in the variable.

verify full system functionality and, if applicable, implement preventive measures  Making sure that a problem has been resolved and will not return. (Step 5 of 6 in the CompTIA troubleshooting methodology.)

vertical alignment (VA)  Display technology used in mid-range LCD panels. VA refers to how the liquid crystal matrix is arranged within the panel.

VESA mount  A screen or display bracket that follows the industry standard—established by the Video Electronics Standards Association (VESA)—which specifies size, location, and type of mounting points.

VGA connector  A 15-pin, three-row, D-type VGA monitor connector. Goes by many other names, such as D-shell, D-subminiature connector, DB-15, DE15, and HD15. The oldest and least-capable monitor connection type.

vi  Linux and macOS command-line tool for editing text files.

video capture  Computer jargon for the recording of video information, such as TV shows or movies.

video card  Expansion card that works with the CPU to produce the images displayed on your computer’s display.

video display  See monitor.

viewing angle  Width (measured from the center to the side of a display) range within which the image can be fully seen.

virtual assistant  Voice-activated technology that responds to user requests for information. Virtual assistants can be used to search the Internet, make reminders, do calculations, and launch apps.

virtual desktop infrastructure (VDI)  Hosting desktops (Windows, Linux, or macOS) on a server so they can be used in VMs on remote devices. Not to be confused with VDI virtual machine disk images.

virtual machine (VM)  A complete environment for a guest operating system to function as though that operating system were installed on its own computer.

virtual memory  Portion of the hard drive set aside by an OS to act like RAM when the system needs more RAM than is installed. A file containing this data is typically called a page file in Windows and a swap file in UNIX platforms like Linux and macOS.

Virtual Network Computing (VNC)  Protocol enabling remote desktop connections. See also remote desktop.

virus  A program that has two jobs: to replicate and to activate. Replication means it copies itself. Activation is when a virus damages a system or data. A virus can’t self-replicate across networks; it needs human action to spread to other drives. See also definition file.

virus shield  Passive monitoring of a computer’s activity, checking for viruses only when certain events occur, such as a program execution or file download.

vishing  A social engineering attack in which the attacker uses the phone to scam an unsuspecting user out of information that can be used to cause further harm.

VoIP (Voice over Internet Protocol)  Collection of protocols that makes voice calls over a data network possible.

VoIP phone  Device that looks like a regular landline phone but uses VoIP to communicate over a computer network.

volatile  Memory that must have constant electricity to retain data.

volts (V)  Measurement of the pressure of the electrons passing through a wire, or voltage.

volume  See partition.

VPN (virtual private network)  Encrypted connection over the Internet between a computer or remote network and a private network.

vulnerability  Weakness in a system, network, or organization that an attacker will exploit to gain access, steal information, and cause other harm.

WAN (wide area network)  A widespread group of computers connected using long-distance technologies.

WAP (wireless access point)  Device that centrally connects wireless network nodes.

wattage (watts or W)  Measurement of the amps and volts needed for a particular device to function.

Web browser  Program designed to retrieve, interpret, and display Web pages.

Web server  A computer that stores and shares the files that make up Web sites.

whaling  A phishing attack in which the attacker specifically targets someone high up in an organization, like the CEO.

wide area network  See WAN.

Wi-Fi  Common name for the IEEE 802.11 wireless Ethernet standard.

Wi-Fi 6  See 802.11ax.

Wi-Fi 6E  See 802.11ax.

Wi-Fi calling  Mobile device feature that enables users to make voice calls over a Wi-Fi network, rather than a cellular network.

wildcard  Character—usually an asterisk (*) or question mark (?)—used during a search to represent search criteria. For instance, searching for *.docx will return a list of all files with a .docx extension, regardless of the filename. The * is the wildcard in that search. Wildcards can be used in command-line commands to act on more than one file at a time.

Windows 10  Operating system developed by Microsoft that powers most desktop and portable computers in use today.

Windows 10 Enterprise  Windows edition that includes all the power and features of Windows 10 Pro for Workstations but also includes a feature called Long-Term Servicing Branch. LTSB turns off automatic updates, removes the Microsoft Store, and disables the automatic installation of Microsoft’s Edge browser. Windows 10 Enterprise is not available in stores; it has to be purchased through a Microsoft sales representative.

Windows 10 Home  The most basic edition of Windows. Designed for home users, it has the fewest features. Supports up to 128 GB of RAM.

Windows 10 Pro  A more robust edition of Windows, which supports up to 2 TB of RAM. Windows 10 Pro is the most basic edition that supports joining an Active Directory domain. It also allows the use of Remote Desktop Protocol and BitLocker encryption.

Windows 10 Pro for Workstations  A beefier edition of Windows Pro that supports up to 6 TB of RAM and is intended for the most high-end and resource-heavy systems. Along with the features of Windows 10 Pro. Windows 10 Pro for Workstations is intended for the most high-end and resource-heavy systems.

Windows 11  Operating system developed by Microsoft and released in 2021, intended to replace Windows 10 and become the default desktop and laptop operating system.

Windows Hardware Compatibility Program  Microsoft’s rigorous testing program for hardware manufacturers, which hardware devices must pass before their drivers can be digitally signed.

Windows key  Key on a keyboard bearing the Windows logo that traditionally brings up the Start menu, but is also used in some keyboard shortcuts.

Windows Memory Diagnostic  Windows tool that can automatically scan up to 4 GB of a computer’s RAM when a problem is encountered.

Windows PowerShell  Command-line tool included with Windows. Offers a number of powerful scripting tools for automating changes both on local machines and over networks.

Windows Preinstallation Environment (WinPE)  The installation program for Windows.

Windows Recovery Environment  See WinRE (Windows Recovery Environment).

Windows Update  Microsoft application used to keep Windows operating systems up to date with the latest patches or enhancements.

WinRE (Windows Recovery Environment)  A special set of tools in the Windows setup that enables you to access troubleshooting and system recovery options.

winver  Command that displays a system’s current Windows version.

wireless access point  See WAP.

wireless Internet service provider (WISP)  An Internet service provider for which the last segment or two uses a point-to-point long-range fixed wireless connection.

wireless mesh network (WMN)  A hybrid wireless topology in which most nodes connect in a mesh network while also including some wired machines. Nodes act like routers; they forward traffic for other nodes, but without wires.

wireless repeater/extender  Device that receives and rebroadcasts a Wi-Fi signal to increase coverage.

work area  In a basic structured cabling network, often simply an office or cubicle that potentially contains a PC attached to the network.

workgroup  A simple, decentralized network that Windows PCs are configured to use by default.

working directory  The current directory used by command-line commands unless they explicitly specify a target file or directory. The prompt usually indicates the working directory.

World Wide Web (WWW)  System of Internet servers that supports documents formatted in HTML and related protocols. Can be accessed by applications that use HTTP and HTTPS, such as Web browsers.

worm  Similar to a virus, except it does not need to attach itself to other programs to replicate. It can replicate on its own through networks, or even hardware like Thunderbolt accessories.

WPA2 (Wi-Fi Protected Access 2)  Wireless security protocol, also known as IEEE 802.11i. Uses the Advanced Encryption Standard (AES) and replaces WPA.

WPA3 (Wi-Fi Protected Access 3)  The successor to WPA2, addresses usability and security issues that affected its predecessor by including encryption to protect data of users on open (public) networks.

wrapper  See container file.

WWW  See World Wide Web.

x86  Describes 32-bit operating systems and software.

x86-64  Describes 64-bit operating systems and software. Sometimes known as x64.

zeroconf (zero-configuration networking)  Operating system feature that provides a random Class B IP address to a system set for DHCP when a DHCP server cannot be found. Enables networking without static IP addressing in such an environment. See also APIPA.

zero-day attack  Attack targeting a previously unknown bug or vulnerability that software or hardware developers have had zero days to fix.

ZIF (zero insertion force) socket  Socket for CPUs that enables insertion of a chip without the need to apply pressure. Intel promoted this socket with its Overdrive upgrades, but ZIF is currently used by both Intel and AMD. The chip drops effortlessly into the socket’s pin grid array holes or land grid array, and a small lever locks it in.

zsh  Command-line shell used by macOS. Short for Z Shell.

zombie  Computer infected with malware that has turned it into a botnet member.


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Glossary
Index
CompTIA A+ Certification All-in-One Exam Guide, Eleventh Edition (Exams 220-1101 & 220-1102), 11th Edition
42h 21m remaining
INDEX
2-in-1 laptops, 961–962

2.4-GHz band, 839

3-2-1 backup rule, 579

3-D printers

components, 1112–1113

installing, 1114

operation, 1112, 1114

troubleshooting, 1157–1158

4-second delays in power supplies, 251

5-GHz band, 839

6/8-pin power connectors, 253–254

6-GHz band, 840

10BASE-T Ethernet, 743

10GBASE-T Ethernet, 743

20-to-24-pin motherboard adapters, 253–254

62.5/125 multimode fiber optic cable,
748–749

64-bit processing CPUs, 91

80 Plus program, 258

100BASE-TX Ethernet, 743

110-punchdown blocks, 758

1000BASE-T Ethernet, 743

A

A and AAAA (address) records, 781

A1 SD card class, 406–407

A2 SD card class, 407

AAA (authentication, authorization, and accounting), 853

AAC (Advanced Audio Encoding), 399

absolute file paths, 604, 611

AC. See alternating current (AC)

Accelerated Graphics Port (AGP) interface, 701

accelerometers, 1019

acceptable use policies (AUPs), 1224

access

authentication. See authentication

cloud, 951–952

Internet, 904–908

levels, 521

mobile applications, 1092–1095

printers, 1142–1144

Registry, 458

remote. See remote access

shared folders, 804–806

unauthorized, 1165

access control lists (ACLs)

description, 1181

NTFS, 327

access control vestibules, 1166, 1172

Access Denied messages from malware, 1190

Accessibility preferences pane, 498

accessories for mobile devices, 1050–1051

accidental touches with mobile devices, 1061

Account Lockout Threshold policy, 1184

Account Policies container, 538

accounts. See users and user accounts

Accounts app, 514–515

Accounts screen on iPhone, 1038–1039

Accounts settings, 467, 713

ACLs (access control lists)

description, 1181

NTFS, 327

Acronis True Image program, 433

Action Center for malware, 1190–1191

action plans for problem resolution, 23

actions

documenting, 24–25

Task Scheduler, 555

activation

cameras and microphones, unauthorized, 1095–1096

DRM requirements for, 1239–1240

viruses, 1185

Windows installation, 444

Active Directory

administration, 810–815

computer installation in, 443

domains, 807–810

group policies, 1183

home folders, 814

Active Directory Users and Computers utility, 809–812

active listening, 7

active matrix LCD monitors, 689

active matrix OLED (AMOLED) devices, 1010

active partitions, 310–311

active power factor correction (active PFC), 256

activity lights on NICs, 793

actors, threat, 1162–1163

ad blockers, 895–897

adapters

AC supply, 238–240

cable, 697–698

display. See display adapters

Molex connectors, 250

USB, 974

adaptive sync for monitors, 730

Add Counters dialog box, 487–488

Add Hardware Wizard, 217–218

add-on video display features, 700

Add Printer Wizard, 1132, 1134

address bus

chipsets, 156–157

description, 154

memory, 80–84

patterns, 82–84

address records (A and AAAA), 781

address spaces in CPUs, 82

addresses

e-mail, 900

IP. See IP addresses

MAC. See media access control (MAC) addresses

ADFs (automatic document feeders)

description, 1122

scanners, 1117

adjustments for video displays, 698

administrative access threats, 1168

administrative shares, 533

Administrative Tools

applets, 470–472

Certificate Manager, 493

disk management, 335

Event Viewer, 489

firewalls, 1208

functions, 58–59

partitions, 315

Performance Monitor, 486

Print Management, 1137

Resource Monitor, 482

security policies, 537–538

services, 671

shared folders, 533

administrator passwords, 167, 543

Administrators group, 510, 513

ADSL (asymmetric DSL), 873

Advanced Attributes dialog box, 534–535

Advanced Audio Encoding (AAC), 399

Advanced display option, 711, 716

Advanced Encryption Standard (AES), 838

Advanced Host Controller Interface (AHCI)

enabling, 302

hard drives, 287

Advanced Micro Devices, Inc. (AMD) CPUs, 85–86

advanced packaging tool (APT), 634

Advanced RISC Machine (ARM) processors, 85, 1025

Advanced Sharing dialog box for folder sharing, 802–804

Advanced tabs

duplex settings, 791

Internet Options, 899

performance options, 572–575

print spoolers, 1143

system setup, 168–169

Advanced Technology Attachment (ATA) standards, 281–283

AES (Advanced Encryption Standard), 838

AFC (Automated Frequency Coordination), 840

AGP (Accelerated Graphics Port) interface, 701

AHCI (Advanced Host Controller Interface)

enabling, 302

hard drives, 287

Ai Tweaker tab, 167–168

air filter masks, 19

airborne particle protection, 1234–1235

AirDrop utility, 501

airflows in power supplies, 263–264

airplane mode

mobile devices, 1023

portable devices, 979

AirPlay feature, 1027

AirPrint feature, 1134

alarm systems, 1173

alerts from malware, 1189

all-in-one devices. See printers and multifunction devices

allocation units, 361

Allow this device to wake the computer option, 794

alternating current (AC)

adapters, 238–240

description, 236

grounding, 242

protecting, 242–246

spikes and sags, 242–246

supplying, 237–241

testing, 237–238, 241

UPSs, 244–246

ALUs (arithmetic logic units) in CPUs, 84, 94

Amazon Web Services (AWS)

IaaS, 948–949

rapid elasticity, 954

AMBER Alerts, 1022

AMD (Advanced Micro Devices, Inc.) CPUs, 85–86

AMD Memory Profile (AMP), 131

AMD Overdrive Utility, 112

American National Standards Institute (ANSI) standards

cabling, 748, 754–755

labeling, 759

patch cables, 760

UTP, 745, 748

American Standard Code for Information Interchange (ASCII) language, 1115

AMOLED (active matrix OLED) devices, 1010

AMP (AMD Memory Profile), 131

amperage, 235

amplitude of sound, 398

analog sound, 397–398

Android operating system

apps, 1032–1033

expansion options, 1028

mobile devices, 1018–1019

smartphones, 63, 1008

Android packages (APKs), 1094

ANSI. See American National Standards Institute (ANSI) standards

answers, obtaining, in effective communication, 8–9

antennas

802.11n, 841

LCD frames, 965

placement, 836, 994

wireless networks, 844–846

WISP, 876

anti-malware programs

boot media, 1196

mobile applications, 1088–1089

mobile devices, 1077–1078

rogue, 1190

working with, 1191–1194

anti-phishing training, 1194

antistatic bags, 13–14

antistatic tools, 12–15

antistatic wrist straps, 210

antivirus programs

mobile devices, 1077–1078

techniques, 1192–1193

Apache HTTP Server, 736

APFS (Apple File System), 330

APIPA (Automatic Private IP Addressing), 790

APKs (Android packages), 1094

App history tab in Task Manager, 478–479

app scanners, 1088–1089

App Store

apps in, 1030–1031

iOS operating system, 1016

macOS software installation, 565

appearance, professional, 2–3

Apple Business Manager, 501

Apple File System (APFS), 330

Apple ID accounts, 500–501, 1031–1032

Apple Keynote program, 1027

Apple mobile device expansion options, 1026–1027

Apple Pay system, 1022

Apple Pencil, 1018

applets, Control Panel. See Control Panel

appliances

backup, 591

Internet, 909, 1210–1211

Application events in Windows Logs, 490

Application Performance Class SD card ratings, 406–407

application protocols

functions and ports, 888

Internet, 886–888

applications

closing, 477, 1057–1058

crashes, 672, 681

description, 32, 475

encryption, 1212–1213

example, 34

installing, 641

launching issues, 1063

mobile. See mobile applications

security, firewalls, 1205

security, mobile devices, 1086–1096

security, troubleshooting tools, 1086–1090

settings, 466

troubleshooting, 653–654

uninstalling, 1059

virtualization, 934–935

Web, 949

Windows, 43, 47

Apps & features for software removal, 569–572

APT (advanced packaging tool), 634

apt-get command, 633–634

arithmetic logic units (ALUs) in CPUs, 84, 94

ARM (Advanced RISC Machine) architecture processors, 85, 1025

ASCII (American Standard Code for Information Interchange) language, 1115

aspect ratios

monitor resolution, 724–725

portable devices, 965

assertive communication, 6–7

asset management

barcodes, 1221

database system, 1220–1221

inventory lists, 1220

procurement life cycle, 1222

tags and IDs, 1221

warranty and licensing, 1222–1223

assigned users in asset management, 1223

assigning drive letters, 351

asterisks (*) for file wildcards, 619–620

ASUS devices, 831–832

asymmetric DSL (ADSL), 873

AT motherboards, 194–196

ATA (Advanced Technology Attachment) standards, 281–283

ATA/ATAPI hard drives, 281–283

Athlon CPUs, 86

attacks, 1162. See also threats

attire, professional, 2–3

ATX motherboards

overview, 195–197

power to, 250–251

ATX power supplies

removing, 260–261

testers, 266–267

ATX12V 1.3 power supplies, 251–252

ATX12V 2.0 power supplies, 253–254

audio. See sound

audio jacks in mobile devices, 1026

audit logs in network printers, 1140

Audit Success and Audit Failure levels, 491

audits for procurement, 1222

AUPs (acceptable use policies), 1224

authentication

fingerprint and facial recognition, 519

hardware, 1177–1181

mobile devices, 1082–1083

mobile synchronization, 1044

network printers, 1140

network security, 1211–1215

options, 516–520

overview, 1176–1177

personal identification numbers, 520

portable devices, 985

software, 1177

usernames and passwords, 517–519

users, 508–510

wireless networks, 837–838, 853–854

workgroups, 800–801

authentication, authorization, and accounting (AAA), 853

authentication servers, 815

authenticator applications

benefits, 1176

description, 1179

mobile devices, 1083

authorization

description, 508

NTFS permissions, 520–529

review questions, 547–549

auto-brightness for mobile device displays, 1060

auto-range meters, 240

auto-switching power supplies, 983

autodetection

configuring, 299

hard drive troubleshooting, 300

mass storage, 299–300

automated backups, 641

Automated Frequency Coordination (AFC), 840

automatic document feeders (ADFs)

description, 1122

scanners, 1117

Automatic Private IP Addressing (APIPA), 790

automation, scripts for, 640

automobiles, synchronization with, 1042

autorotation problems in mobile device displays, 1060

Autoruns utility, 479

autostarting programs

controlling, 556–559

deleting, 461

disabling, 478–479

services, 671

AUX connectors, 252–253

availability, cloud for, 954

AWS (Amazon Web Services)

IaaS, 948–949

rapid elasticity, 954

B

Babbage, Charles, 29

backbones, Internet, 868–870

backlights

issues with, 719, 998

keyboards, 979

LCD panels, 689–691

portable devices, 966

Backup and Restore applet, 580–581

backups

automated, 641

introduction, 575–576

media, 577–578

mobile applications, 1090

mobile devices, 1081

personal data, 580–585

rotation schemes, 579

settings, 465

testing, 578

third-party tools, 590–591

thumb drives, 637

troubleshooting methodology, 20–21

types, 576–577

Windows upgrades, 431

bad blocks, mapping, 319–321

badge readers, 1177

badges

facility security, 1174

network printers, 1140

bands in IEEE 802.11, 839

bandwidth

DDR, 131–134

display, 694

network, 488, 745, 921–922

PCIe, 207–208

SATA drives, 285

Thunderbolt, 380

unshielded twisted pair, 745

video memory, 703

banks, memory, 128

barcode scanners, 388–389

barcodes for asset management, 1221

bare-metal hypervisors, 945

baseband updates, 1035

bash (Bourne-Again Shell), 597

bash scripts, 639

basic disks, 308

Basic Service Sets (BSSs), 833–834

.bat (batch) files, 639

batteries

charging, 975, 996, 1068–1069

CMOS settings, 183–185

date and time issues, 682–683

mobile devices, 1065–1069

portable devices, 975, 996

power management, 979–981

replacing, 992

swollen, 1069

UPSs, 244–246

BD-R (recordable) format, 414

BD-RE (rewritable) format, 414

BD-ROM format, 413

beep codes in POST, 178–179

behavior issues

malware, 1186–1189

mobile applications, 1091

Berg connectors, 248

beta device drivers, 216

binary numbers

MAC addresses, 740

Registry, 461

biometric authentication

benefits, 1179–1180

examples, 385–387

fingerprint and facial recognition, 519

mobile devices, 1083–1084

portable devices, 985

smartphones, 387–388

BIOS

component information, 166

default and optimized settings, 181–182

flashing, 229

hardware virtualization support, 936

keyboards, 162

mass storage support, 299–301

passwords, 167

BIOS (on-board NIC) setting, 446

bit depth in sound, 398

BitLocker, support for, 424, 426–427

BitLocker Drive Encryption

enabling, 536–537

TPM requirements, 176, 536

BitLocker To Go option, 536

bits in MAC addresses, 740

black ! indicator in Device Manager, 218–219

black screens, 677–678

black-to-white (BtW) monitor response rate, 727

BlackBerry PDA, 1006–1007

blacklists in MAC addresses, 1176

blank pages from laser printers, 1154

blank passwords, 519

blocks, hard drive, 306–307

blotchy print from laser printers, 1156

Blu-ray Disc media, 412–413

Blue Screen of Death (BSoD)

catastrophic failures, 115

driver issues, 723

NMIs, 148–149

troubleshooting, 666

Bluetooth wireless technology

configuring and troubleshooting, 856–858

expansion options, 1028–1029

headphones, 968

mobile devices, 1047–1048

overview, 846–848

pairing issues, 1092

portable devices, 971

speakers, 1047

troubleshooting, 998–999

BNC connectors, 751

bollards, 1172–1173

Bonjour Print Service, 1134

books, motherboard, 221–222

Boot Manager, 180–181

boot sector viruses, 1185

boot sectors, 180

boot sequence, 180

missing operating systems, 674

POST, 180–181

problems, 668

secure, 176–177

system setup utility, 168

Boot tab

boot device selection, 168, 170

boot options, 173–174

System Configuration, 463

Bootable device not found message, 364–365

bootable media

anti-malware tools, 1196

boot sectors, 180

overview, 331–332

USB drives, 655

bootleg APK applications, 1094

boots

methods, 429

order priority, 301

patch cables, 762–763

system setup utility option, 173

bootstrap loaders, 180

botnets, 1188–1189

Bourne-Again Shell (bash), 597, 639

boxes

lifting, 18

RAID, 295

branch statements in CPUs, 78

brightness

battery life, 1065–1066

dim displays, 1060

dynamic range, 729

mobile device controls, 1060

monitors, 718, 726

portable devices, 979

projectors, 692–693

bring your own device (BYOD)

mobile devices, 1075

vulnerabilities, 1171

broadcast domains

LANs, 751–752

WANs, 765

broken screens in mobile devices, 1062

browsers. See Web browsers

brute-force attacks, 1164

BSoD. See Blue Screen of Death (BSoD)

BSSs (Basic Service Sets), 833–834

BTRFS file system, 330

BtW (black-to-white) monitor response rate, 727

buffered memory, 136–137

built-in CLI commands, 607

built-in sound, 397

Builtin folder, 810

burn-in, display, 719

burn-in motherboard failures, 227

burners, CD-R, 409–410

burning smells, 680–681

bus-powered USB hubs, 377

buses

address, 80–84, 154, 156–157

chipsets, 156

data, 154

expansion. See expansion buses and cards

business casual attire, 2–3

businesses, software impact on, 564

BYOD (bring your own device)

mobile devices, 1075

vulnerabilities, 1171

bytes

description, 79

DRAM, 127

C

C shell (csh), 597

cable Internet connections, 873–874

cable locks

laptops, 1169

portable devices, 984

cable strippers, 760–761

cable testers for patch cables, 763

cables

display adapters, 704–705

hard drives, 297–298

IDE, 282, 284

safety issues, 17–18

structured, 752–755

telecommunications rooms, 757–760

troubleshooting, 817–821

USB, 374–376

video, 718

caches

CPUs, 94–97

Web browsers, 895–896

calibration

batteries, 975

inkjet printer printheads, 1150

laser printer color, 1154

mobile device displays, 1061–1062

printer color, 1139–1140

touch, 1001

cameras

connections, 396

description, 395–396

mobile application activation, 1095–1096

mobile devices, 1010–1011

portable devices, 965

storage media, 395

webcams, 396–397

candelas, 726

capacitors, swelling, 682

capacity

DVD-media, 412

RAM, 127, 142–144

capture cards, 704

card readers, 407

carriages and carriage belts in inkjet printers, 1103

carrier sense multiple access/collision avoidance (CSMA/CA) networking scheme, 832

cartridges

disposal, 1147

inkjet printers, 1105–1106, 1150–1151

laser printers, 1108–1109, 1129

replacing, 1150

CAs (certificate authorities), 893–894, 1213–1214

case fan support in motherboards, 203

cases

fans, 263

mobile devices, 1076–1078

motherboards, 220–223

cat command, 618

catastrophic failures

CPUs, 114–115

motherboards, 226–228

NMIs, 148

categories (Cats)

RJ45 connectors, 764

UTP cables, 745–746

cathode-ray tube (CRT) displays, 688

CBL Data Shredder, 451–452

CCFLs (cold cathode fluorescent lamps) for LCD panels, 690

cd command, 610–611

CD (Compact disc) media, 408–411

CD-Digital Audio (CDDA), 408

CD File System (CDFS), 408

CD media, 408

CD quality sound, 398

CD-R (CD-recordable) standard, 409–410

CD-ROM format, 408–409

CD-RW (CD-rewritable) format, 410

CDDA (CD-Digital Audio), 408

CDFS (CD File System), 408

CDMA (code division multiple access), 876

cell tower analyzers, 1087–1088

cellular services

data, 1035

Internet, 876–878

location, 1011–1012

central processing units (CPUs)

64-bit processing, 91

buses, 156–157

caches, 94–97

catastrophic failures, 115

clock, 73–76

clock multipliers, 90–91

cooling, 107–111

core components, 67–78

description, 35, 67

desktop vs. mobile, 88–89

developers, 84–89

EDBs, 76–77

graphics processing units, 100

hardware virtualization support, 936

hybrid cores, 116

installing, 104–114

integrated memory controllers, 100

keyboard controllers, 157–160

man in the box concept, 68–71

memory, 78–84

microarchitectures, 86–88

mobile devices, 1025

model names, 86

modern, 83–84

multicore processing, 99–100

multithreading, 98

overclocking, 112–113

overheating, 114–115

parallel execution, 92

pipelining, 92–94

process nodes, 116

processor numbers, 103–104

registers, 71–73

review questions, 117–119

security, 100–101

selecting, 102–104

sockets, 102–107

software requirements, 560

technology, 89–101

troubleshooting, 114–115

virtualization support, 92

certificate authorities (CAs), 893–894, 1213–1214

Certificate Manager, 492–493

certificate warnings, 1214

certificates

encryption, 536, 1213–1214

Web browsers, 891, 893–894

certificates of destruction for hard drives, 451

CF (CompactFlash) cards, 405

CFexpress format, 407

chain of custody in incidents, 1241

chamfers in Molex connectors, 248

change boards, 1232

change management

documented business processes, 1229–1230

introduction, 1228–1229

process, 1230–1231

Change permissions

description, 521

folder sharing, 803

changing drive letters, 351

channels

controllers, 299

IEEE 802.11, 839–840

speaker, 399

WAPs, 850, 854–855

character types in passwords, 518

charge rollers in laser printers, 1110

chargers and charging batteries

battery health concerns, 996

issues, 1068–1069

mobile devices, 1051

optimized, 975

portable devices, 983–984

charging step in laser printers, 1126–1127

checkpoints in virtualization, 932

checksums

polymorphic virus detection, 1194

software, 890

chemical hazardous materials, 1235–1236

chip readers in mobile devices, 1048–1049

chipsets

controllers, 154–156

motherboards, 192, 199–201

chkdsk tool, 356, 624

chmod command, 529

chown command, 528

chromaticity diagrams, 728

Chromebooks, 961

CIDR (Classless Inter-Domain Routing), 773

CIFS (Common Internet File System), 888

circuit breakers, 235

circuit testers, 241

CITE (color infrastructure and translation engine), 1140

clamping voltage in surge suppressors, 243

classes

Bluetooth devices, 847

fire extinguishers, 268

IP addresses, 773

SD cards, 406–407

classification of data, 1236–1237

Classless Inter-Domain Routing (CIDR), 773

clean command for partitions, 662

clean installs

malware, 1197

Windows, 430, 434–445

cleaning

disks, 359–360

inkjet printers, 1152

keyboards, 384–385

laser printers, 1153

mice, 385–386

monitors, 720–721

portable devices, 981

touchscreens, 1061

cleaning step in laser printers, 1129

clearing

CMOS, 182–183

Web browser caches, 896

CLI. See command-line interface (CLI)

clicking sounds in hard drives, 364

client-side virtualization, 929–930

clients

DNS, 782–783

Web pages, 736–737

clocks

expansion buses, 204–205

time drift, 675–676

clocks, CPU, 73

cycles, 74–75

multipliers, 90–91

overclocking, 76, 112–113

speed, 75–76

wires, 73–74

clogged extruders in 3-D printers, 1157

Clonezilla program, 433

closed source development models, 1015

closed source licenses, 1239

closing

applications, 477, 1057–1058

Terminal app, 603

closing the lid options, 670

cloud

backups, 577–578

characteristics, 953–955

desktop virtualization, 955

Infrastructure as a Service, 948–949

mobile synchronization, 1043

overview, 945–946

ownership and access, 951–952

Platform as a Service, 949–950

printing, 1115

service layers, 947–951

shared resources, 953

Software as a Service, 951

cloud-based wireless network controllers, 856

cloud bursting, 953

CLRTC setting, 113

clusters

FAT 32, 320–322

NTFS, 329

CMOS (complementary metal-oxide semiconductor)

battery issues in date and time, 682–683

clearing, 113, 182–183

lost settings, 183–185

mass storage settings, 299–302

overclocking settings, 112–113

setup settings. See system setup utility

coaxial cable, 750–751

code division multiple access (CDMA), 876

code signing in Web browsers, 890

codebooks, CPU, 72

codecs (compressor/decompressor programs)

sound, 399

video, 402–403

cold cathode fluorescent lamps (CCFLs) for LCD panels, 690

collate option in printers, 1139

colons (:)

drive references, 604, 612

IPv6 addresses, 774–776

color

cabling, 748

inkjet printer cartridges, 1105

laser printers, 1154

printers, calibration, 1139–1140

printers, issues, 1147–1148

USB connectors, 375

video, 718, 722

color depth

monitors, 728–729

scanners, 1119–1121

color infrastructure and translation engine (CITE), 1140

color inkjet printers, 1105–1107

color laser printers, 1108

Color Management applet, 708–709

Color profile video setting, 708

color spaces, 728–729

.com domain, 780

command-line interface (CLI)

accessing, Linux and macOS, 600–602

accessing, Windows, 598–600

assorted commands, macOS and Linux, 629–638

assorted commands, Windows, 624–628

cd command, 610–611

closing, 603

command types, 607–608

deciphering, 596–597

dir command, 609

drive changes, 612

drives and folders, 603–605

file manipulation, 617–624

introduction, 50–52, 595–596

keyboard shortcuts, 628–629

ls command, 610

md and mkdir commands, 613–614

package managers, 633–635

prompt, 596–598, 602–603

rd and rmdir commands, 614–615

Registry, 462

review questions, 648–650

running programs, 615–617

scripting. See scripting

shells, 597

syntax and switches, 605–606

text editors, 635–636

utilities, 51

command-line interpreters, 597

Command Prompt, 597

CLI access, 598

WinRE, 661–662

comments in scripts, 645–646

Common Internet File System (CIFS), 888

communication

effective. See effective communication

mobile devices, 1045–1051

community clouds, 952

Compact disc (CD) media, 408–411

CompactFlash (CF) cards, 405

compatibility

802.11 devices and versions, 842

drivers, 214

dynamic disks, 313

memory, 129

operating systems, 42

power connectors, 254, 285

SD cards, 406

software, 562

touch pens, 1018

USB, 371–374, 379, 1046

wireless devices, 839

WPA2, 838

complementary metal-oxide semiconductor. See CMOS (complementary metal-oxide semiconductor)

complexity requirements for passwords, 517–518

compliance

regulations, 1238

requirements, 1226

for safety, 17

component failures on motherboards, 227, 229

compressed air, 981

compression

disks, 340–341

NTFS, 327–328

sound files, 399

compressor/decompressor programs (codecs)

sound, 399

video, 402–403

Computer Management

disks, 294

groups, 511–513

partitions, 315

printers, 1143

shared folders, 533

computer programmers, 30

computers, 29–30

computing parts, 32–34

computing process, 30–32

hardware, 37–41

review, 63–65

software. See software

stages, 35–37

Computers folder, 810

conditional loops in scripts, 644–645

conditions in Task Scheduler, 555

conductors, 235

confidence, projecting, 7

configurable scanner variables, 1120–1121

Configuration tab in system setup utility, 170, 172

conflicts in IP addresses, 773

connection-oriented protocols, 783, 914

connectionless protocols, 783, 914

connections and connectivity

digital cameras, 396

hard drives, 280–288

Internet, 870–871, 917–919

mobile applications, 1091–1092

mobile devices, issues, 1071–1072, 1092

mobile devices, network, 1033–1037

printer troubleshooting, 1142

printers and multifunction devices, 1123–1124

resource issues, 822

video displays, 694–698

Web browsers, 893–894

wireless network issues, 860–862

Connections tab for Internet Options, 899

connectors

coax, 751

display adapters, 704–705

Ethernet, 746–749

front panel, 203

locks, 1174

mobile devices, 1045–1046

patch cables, 760–761

portable devices, 972

power, 237–238, 248–254

serial ports, 370

USB, 374–376

video, 694–697, 718

work areas, 764

consumables, printer, 1108, 1146–1147

container files for video formats, 402–403

Content tab for Internet Options, 899

context menus in Windows, 43–44

contrast ratio in monitors, 728

Control Panel

Administrative Tools, 470–472

audio, 967

backups, 580–581

certificates, 493

Color Management, 708–709

domains, 810

Ease of Access Center, 470

File Explorer, 472–474

File History, 585

firewalls, 1208–1209

GPS, 999

Indexing Options applet, 469–471

Microsoft Management Console, 57–60

NIC settings, 791

offline files, 980

overview, 467–469

pointing devices, 385

power settings, 977–978

printer sharing, 816

printers, 1131–1133, 1137–1139

Reliability Monitor, 673

security policies, 537–538

settings overview, 464

software removal, 571–572

Sound applet, 469–470

System applet, 469

System Restore, 1197

touch screens, 390

trackpads, 964

UAC, 544–545

User Accounts applet, 516

virtual machines, 939

Wake-on-LAN, 794

Web browsers, 897–899

workgroups, 798

controllers

configuring, 299

domains, 806–807

firmware, 153–155

game, 391–393, 1051

keyboard, 157–160

NICs, 740

RAID, 289–290, 294

USB, 370–371, 672–673

Convert to Dynamic Disk option, 341–342

convertible laptops, 961

convertible power supply adapters, 254

converting

AC power to DC, 238–240

dynamic disks, 341–342

cooling

CPUs, 107–111

power supplies, 261–265

cooling fans

danger from, 18

video cards, 706

cooling fins, 18–19

copied files, NTFS permissions with, 525–526

copy command, 621

copy components, 1122

copying

files, 621–624

hard drives, 637

Core i7 CPUs, 87

cores, CPU, 99, 116

corona wires in laser printers, 1110

corporate-owned mobile devices, 1075

corporate restrictions, 501

corporate use licenses, 1238

corrupted data, 362–363

Cortana virtual assistant, 1021

costs of solid-state drives, 279

counters in Performance Monitor, 487–488

coverage optimization for wireless networks, 843–846

covers for mobile device screens, 1051

cp command, 621, 624

CPU identifier (CPUID) function, 91

CPU tab in Resource Monitor, 484

CPU-Z utility

CPU details, 90–91

memory, 144, 146

CPUID (CPU identifier) function, 91

CPUs. See central processing units (CPUs)

crash screens

catastrophic failures, 115

driver issues, 723

NMIs, 148–149

proprietary, 677

RAID, 365

troubleshooting, 666

crashes

applications, 672, 681

system, 1169

CRCs (cyclic redundancy checks) in frames, 741–742

creased paper in laser printers, 1156

Create Virtual Hard Disk wizard, 941

credentials for routers, 883

credit card readers, 1048–1049

credit card transactions, 1237

crimping patch cables, 760–762

Critical event levels in Event Viewer, 491–492

cross-platform virtualization, 935

cross-site scripting (XSS) attacks, 1165

CRT (cathode-ray tube) displays, 688

cryptographic hash functions, 890

cryptominers, 1186

crystals

clock speed, 75–76

expansion buses, 204–205

csh (C shell), 597

CSMA/CA (carrier sense multiple access/collision avoidance) networking scheme, 832

cultural sensitivity, 6

currency settings, 435

current, electrical, 235

cursor drift, 1001

custom views in Event Viewer, 492

Cyberduck client, 913

cyclic redundancy checks (CRCs) in frames, 741–742

D

D-Cache in CPUs, 99

D-shell connectors, 694

D-subminiature connectors, 694

DACs (digital-to-analog converters), 402

daisy-wheel printers, 1103

damage protection for mobile devices, 1076–1078

damage to mobile device displays, 1062

damaged ports, charging issues from, 1068–1069

data

classification, 1236–1237

corrupted, 362–363

destruction of, 451–452

destruction threats, 1168

encryption, 534–537, 1182, 1212

file system structures, 318

mobile applications, access issues, 1092–1093

mobile applications, usage limit notifications, 1091

mobile devices, cellular services, 1038

mobile devices, security, 1081–1086

mobile devices, usage issues, 1071–1072

RAID protection of, 288–295

regulated, 1237–1238

restoring after installation, 449

retention requirements, 1237

data-at-rest encryption, 1182

data bus

chipsets, 156–157

description, 154

Data Collector Sets in Performance Monitor, 488–489

Data Execution Prevention (DEP)

CPUs, 100–101

performance options, 572–574

data integrity and preservation in chain of custody, 1241

data networks for mobile devices, 1035

data roaming, 1038

data storage stage in computing, 36

data types in scripts, 643–644

database systems for asset management, 1220–1221

Datacolor Spyder calibrators, 1140

date and time

issues, 682–683

settings, 465

date documentation in change management, 1231

DB9 connectors, 370

DC (direct current)

description, 236

supplying, 247

testing, 249

dd command, 637

DDoS (distributed denial of service) attacks, 1164–1165

DDR SDRAM (double data rate SDRAM), 129–130

DDR3 DRAM, 131–132

DDR4 DRAM, 132–133

DDR5 DRAM, 133–134

dead pixels, 718

dead spots in wireless coverage, 843

debris issues in thermal printers, 1149

decode stage in CPUs, 92–93

decryption, 1074

dedicated GPUs, 561

dedicated RAID boxes, 295

default credentials for routers, 883

default gateways

Internet, 870–871

LANs, 771

default groups, 512–513, 1182

default user accounts, 1182

Defender Antivirus, 1190–1191

definition files for antivirus programs, 1196

defragmentation of hard drives, 358

degaussing hard drives, 451

Déjà Dup tool, 586

del command, 620–621

deleted files in FAT 32 file system, 323–325

deleting files, 620–621

deliveries, procurement, 1222

demilitarized zones (DMZs), 1204–1205

denial of service (DoS) attacks, 1164–1165

DEP (Data Execution Prevention)

CPUs, 100–101

performance options, 572–574

dependability, 5–6

desktop

Linux environments, 50

macOS, 47–49

management software, 912

styles, 42–47

virtualization, 955

Desktop & Screen Saver display settings, 713

desktop alerts from malware, 1189

desktop computer CPUs, 88–89

Desktop folder, 55

destruction, data, 451–452

Details tab in Task Manager, 480–481

developer mode access issues in mobile applications, 1093–1094

developers for CPUs, 84–89

developing step in laser printers, 1127

development models for mobile operating systems, 1014–1016

development testing for virtual machines, 934

device chargers, 1051

device drivers. See drivers

Device Manager

device status, 59, 216–217

drivers, issues, 723

drivers, listing, 158–159

expansion card troubleshooting, 217–220

hardware troubleshooting, 859

ports, 380–381

USB power, 378

wireless devices, 860

devices

drivers. See drivers

network security settings, 1086

portable vs. mobile, 960–961

software impact on, 563

Devices and Printers applet

game controllers, 392

paper settings, 1144

printer detection, 1131–1132

printer settings, 1137–1139

printer sharing, 816

printer spoolers, 1143

Devices settings, 466–467

df command, 637–638

DHCP (Dynamic Host Control Protocol)

functions and ports, 888

settings, 782–783

diagnostics

mobile device displays, 1061–1062

print pages, 1154

touch-screens, 1000

dial-up Internet, 872

dictionary attacks, 1164

differential backups, 577

dig command, 786–787

digital cameras. See cameras

digital certificates

encryption, 1213–1214

Web browsers, 891

Digital Light Processing (DLP) technology for projectors, 692

digital multimeters (DMMs) for AC supply tests, 238

digital rights management (DRM), 1239–1240

digital sound, 397–398

digital subscriber line (DSL) connections, 872–873

digital-to-analog converters (DACs), 402

digital versatile discs (DVD) media, 411–412

Digital Visual Interface (DVI), 694–695, 704

digitizers

mobile devices, 1011, 1060

overview, 393–395

dim displays

mobile devices, 1060

portable devices, 998

troubleshooting, 719

DIMMs (dual inline memory modules)

banks, 128–129

double-sided, 134

installing, 145–146

dipole antennas, 844–845

dir command

directory contents, 607–609

wildcards, 619–620

direct burial cable, 746

direct current (DC)

description, 236

supplying, 247

testing, 249

direct LED backlighting for LCD panels, 691

direct thermal printers, 1107

directional antennas, 845–846

directories

changing, 610–611

CLI, 603–604

contents, 607–610

creating, 613–614

removing, 614–615

Dirtbox device, 1091

dirty air, 1234

dirty mobile device screens, 1061

dirty printouts with laser printers, 1155

Disable inheritance option, 524

Disable Windows Installer policy, 1184

disabling

applications, 557–559

AutoRun, 564

autostarting programs, 478–479

backlit keyboards, 979

cellular data, 1072

controllers, 299, 380–381

device roaming, 1067

fast startup, 669

guest accounts, 836–837

programs, 667–668

SSID broadcasts, 836

system restores, 1197

unused accounts, 1181

USB ports, 378

Wi-Fi, 855

disassembling laptops, 985–988

Disk Cleanup tool, 360

disk duplexing in RAID, 290

Disk Management program

disk initialization, 336–338

diskpart utility, 661–662

drive letters, 351

dynamic disks, 341–348

mounting partitions as folders, 348–350

overview, 334–335

partition and volume creation, 338–341

partition formatting, 351–352

partitioning, 315–317

RAID, 293–294

disk quotas in NTFS, 328

Disk tab in Resource Monitor, 484

disk thrashing, 142

Disk Utility, 356–357

diskpart tool

partitions, 315

working with, 661–662

disks. See drives; hard drives

Display adapter properties, 711, 716

display adapters, 687

connector types and cables, 704–705

drivers, 706–707, 716–717

graphics processors, 701–703

integrated GPUs, 703–704

introduction, 700

motherboard slots, 700–701

review questions, 731–734

settings, macOS and Linus, 713–715

settings, Windows, 707–713

software, 706–715

troubleshooting, 717–724

video displays, 688–700

video installation and configuration, 705–706

video memory, 703

Display preference pane, 496

DisplayPort

audio, 401

display connectors, 696

portable devices, 968

video cards, 704–705

displays

battery usage, 1065–1066

macOS settings, 496

mobile device issues, 1059–1062

mobile devices, 1009–1010

monitors. See monitors

portable devices, 965–966

portable devices, issues, 998–999

portable devices, ports, 968–970

power management, 979

replacing, 993–994

technologies, 687

distance limits for fiber optic cable, 749

distractions, avoiding, 7

distributed denial of service (DDoS) attacks, 1164–1165

distribution methods for software, 562–563

distributions, Linux, 50

DKIM (DomainKeys Identified Mail) records, 781

DL (dual-layer) DVD formats, 412

DLP (Digital Light Processing) technology for projectors, 692

DMARC (Domain-based Message Authentication, Reporting, and Conformance) records, 781

DMMs (digital multimeters) for AC supply tests, 238

DMZs (demilitarized zones), 1204–1205

DNAT (dynamic NAT), 880

DNS. See Domain Name System (DNS)

Dock & Menu Bar option, 714–715

docking stations

mobile devices, 1051

portable devices, 973–974

documentation, 1224–1225

articles, 1228

CLI commands, 606

end-user termination checklists, 1227

expectations, 11

incidents, 1240

knowledge bases, 1228

laptop disassembly, 985

new-user setup checklists, 1226

operational procedures, 1223–1227

regulatory compliance requirements, 1226

troubleshooting, 24–25

documented business processes in change management, 1229–1230

Documents folder, 52, 55

Domain-based Message Authentication, Reporting, and Conformance (DMARC) records, 781

Domain Controllers folder, 810

Domain Name System (DNS)

client information, 782–783

domain names, 780–781

functions and ports, 888

purpose, 779–780

servers, 779–780

Domain networks, 1206–1207

DomainKeys Identified Mail (DKIM) records, 781

domains

administration, 810–815

introduction, 806–807

organization, 809–810

vs. workgroups, 421–423, 443

door locks, 1174

DoS (denial of service) attacks, 1164–1165

dot-matrix printers, 1103–1104

dots per inch (dpi) resolution in inkjet printers, 1106–1107

dotted-decimal notation in IP addresses, 772

double data rate SDRAM (DDR SDRAM), 129–130

double images from laser printers, 1155

double-pumped frontside buses in CPUs, 97

double-sided DIMMs, 134

double-sided (DS) DVD formats, 412

downloaded program files, deleting, 359

Downloads folder, 55

downstream USB host controllers, 371

dpi (dots per inch) resolution in inkjet printers, 1106–1107

draft quality with impact printers, 1103

DRAM. See dynamic random-access memory (DRAM)

dress code, 2–3

drilling hard drives, 451

drive errors in Windows installation, 448

drive letters

assigning, 338–339, 351

changing, 351

description, 52

drivers

beta, 216

Blue Screen of Death problems, 666

expansion cards, 211–217

fast startup issues, 669

installing, 213–215

keyboard, 158–160

newest, 212–213

printer, 1115

removing, 214

rollbacks, 215–216

scanners, 1118–1119

shutdown issues, 670

troubleshooting, 723–724

unsigned, 214

updates, 218–219, 716–717

upgrading, 449

USB devices, 378

verifying, 216–217

video, 706–707, 716–717

drives

CLI commands, 603–605

flash. See flash drives

hard. See hard drives

initialization, 336–338

mapping, 815–816

moving between, 612

remapping, 641

SSD. See solid-state drives (SSDs)

status, 337

virtual machines, 941–942

Windows installation, 429

DRM (digital rights management), 1239–1240

DS (double-sided) DVD formats, 412

DSL (digital subscriber line) connections, 872–873

dual-band operation in 802.11n, 841

dual-channel architecture in DRAM, 130

dual-core CPUs, 99

dual inline memory modules (DIMMs)

banks, 128–129

double-sided, 134

installing, 145–146

dual-layer (DL) DVD formats, 412

dual-link DVI, 695

dual voltage power supplies, 237

dumpster diving, 1166–1167

duplex settings for printers, 1138

duplexing, RAID, 290–291

duplexing assemblies for printers, 1111, 1117

dust

cleaning, 1234

laser printers, 1153

overheating from, 679–680, 997

DVD (digital versatile discs) media, 411–412

DVD-ROM, 412

DVI (Digital Visual Interface), 694–695, 704

DVI-I connectors, 704

DVI-to-HDMI cable, 698

DWORD values in Registry, 461

dying hard drives, 364–365

dynamic contrast ratio for monitors, 728

dynamic disks

creating, 341–342

description, 308

mirrored volumes, 346–347

mount points, 348, 350

overview, 312–313

RAID, 346–347

simple volumes, 342–343

spanning volumes, 344–346

striped volumes, 346–347

Dynamic Host Control Protocol (DHCP)

functions and ports, 888

settings, 782–783

dynamic IP addresses, 776

dynamic NAT (DNAT), 880

dynamic random-access memory (DRAM), 121

amount needed, 137–138

description, 80

latency, 134–136

old, 127

organizing, 123

overview, 122–123

practical, 123–125

registered and buffered, 136–137

sticks, 125–127

types, 127–134

variations, 134–137

working with, 137

dynamic range in monitors, 729–730

E

e-mail

application protocols, 886

hijacked accounts, 1189

malware in, 1189

mobile devices, 1038–1041

ports, 1040–1041

scanner feature, 1121

viruses in, 1198

Web browsers, 900–903

e-waste, recycling, 1236

E911 (Enhanced 911) system, 1022

EAS (Emergency Alert System), 1022

EAS (Exchange ActiveSync), 1042

Ease of Access Center, 470

EB (exabytes), 91

EBSSs (Extended Basic Service Sets), 833–834

ECC (error checking and correction), 136

ECC (error correction code) for hard drives, 363

ECC RAM (error correction code RAM), 136

echo images from laser printers, 1155

EDB (external data bus) for CPUs, 68–71, 76–77

edge-blurring techniques in monitor resolution, 724

edge LED backlighting, 691

EDGE technology, 876

editing Registry, 460–462

editions, Windows, 420–427

editors, text, 635–636

EDR (Enhanced Data Rate) Bluetooth, 847

.edu domain, 780

education

malware, 1194, 1199–1200

mobile application security, 1086–1087

effective communication, 6

answers, 8–9

assertive, 6–7

expectations and follow-up, 10–11

respectful, 7–8

effective permissions, 1182

efficiency cores in CPUs, 116

EFS (Encrypting File System)

encryption with, 534–536

NTFS, 328

eGPUs (external graphics processing units), 731

elasticity, cloud for, 954

electrical fire safety equipment, 18–19

electricity basics, 234–236

electro-photographic imaging in laser printers, 1107

electromagnetic interference (EMI)

description, 15

power lines, 244

STP cable, 746

electromagnetic pulse (EMP), 11

electronic contact cleaning solution for expansion cards, 211

electrostatic discharge (ESD)

antistatic tools, 12–15

expansion card installation, 210

mats, 13

motherboard installation, 223

overview, 11–12

straps, 12–13

elevated privileges, 511

embedded systems

industrial control systems, 915

Internet of Things, 915–916

introduction, 914

NFC, 1048

USB hubs, 376

Web servers, 738

embossed effect in laser printers, 1156

Emergency Alert System (EAS), 1022

emergency capabilities of mobile devices, 1022

EMI (electromagnetic interference)

description, 15

power lines, 244

STP cable, 746

EMP (electromagnetic pulse), 11

emulation, printer, 1136

emulators, terminal, 600

Enable inheritance option, 524

enclosures, RAID, 295

encoding schemes in transfer rate, 207

Encrypting File System (EFS)

encryption with, 534–536

NTFS, 328

encryption

BitLocker, 424

BitLocker Drive Encryption, 536–537

data, 534–537

data-at-rest, 1182

EFS, 534–536

FileVault, 502

mobile devices, 1074, 1079

network security, 1211–1215

NTFS, 328

VPNs, 909, 1023–1025

wireless networks, 852–854

end-of-file markers in FAT 32 file system, 320–321

end-of-life (EOL) operating systems, 1171

end points in USB devices, 374

End process tree option in Task Manager, 480–481

end-user acceptance in change management, 1232–1233

end-user device configuration options for mobile devices, 1075

end-user license agreements (EULAs)

description, 1239–1240

Windows installation, 433–434, 439

end-user termination checklists, 1227

endpoint management servers for VPNs, 909–910

endpoint management software for desktop management, 912

endpoints in USB controllers, 672

energy savings in virtualization, 932

engine test pages for printers, 1154

engines in anti-malware programs, 1196

Enhanced 911 (E911) system, 1022

Enhanced Data Rate (EDR) Bluetooth, 847

Enhanced Virus Protection in CPUs, 101

entry control rosters, 1166

environment variables in scripts, 646–647

environmental controls

hazardous materials, 1235–1236

introduction, 1233

temperature, humidity, and ventilation, 1233–1235

EOL (end-of-life) operating systems, 1171

EPS12V power supplies, 252

equipment

grounding, 13

locks, 1174

placement, 1235

equipment racks, 756–757

erase command, 620–621

erase lamps in laser printers, 1109, 1129

erasing hard drives, 451

error checking and correction (ECC), 136

error checking hard drives, 356–357

Error checking tool, 356

error codes

laser printers, 1154

printer troubleshooting, 1142

error correction code (ECC) for hard drives, 363

error correction code RAM (ECC RAM), 136

Error event levels in Event Viewer, 491

errors, benefits of, 610

eSATA (external SATA), 286

escalating problems in troubleshooting, 23

ESD. See electrostatic discharge (ESD)

essential software in Windows installation, 450

ethereal symptoms in motherboards, 227

Ethernet networks

coaxial, 750–751

fiber optic, 748–750

introduction, 743

LANs, 751–752

portable devices, 971–972

review questions, 766–768

shielded twisted pair, 746

star bus, 743–744

structured cabling, 752–755

telecommunications rooms, 755–763

unshielded twisted pair, 745–748

WANs, 765

work areas, 763–765

Ethernet over Power, 752

Ethic of Reciprocity, 5, 8

EUI-64 (Extended Unique Identifier, 64-bit), 776

EULAs (end-user license agreements)

description, 1239–1240

Windows installation, 433–434, 439

event levels in Event Viewer, 491–492

Event Viewer

custom views, 492

event levels, 491–492

overview, 489–490

Windows Logs, 490–491

Everyone group

folder sharing, 803

Linux permissions, 527–528

evidence, chain of custody for, 1241

evil twin attacks, 1167

exabytes (EB), 91

Exchange ActiveSync (EAS), 1042

Exchange Server, 902

exclamation points (!) in Device Manager, 859

Execute permission, 528

execute stage in CPUs, 92–93

exFAT file system, 329–330

exiting system setup utility, 177

expansion buses and cards, 203–204

device drivers, 211–217

handling, 209–211

installing, 209–217

learning about, 209

PCI, 205–206

PCIe, 206–208

portable device slots, 972–974

replacing, 992–993

structure and function, 204–205

troubleshooting, 217–220

expectations in effective communication, 10–11

expiration

licenses, 1239

passwords, 518, 538–539

exploits, 1162. See also threats

exposing step in laser printers, 1127

ext4 (Fourth Extended File System), 330

Extend these displays option, 710

Extend Volume Wizard, 344–346

Extended Basic Service Sets (EBSSs), 833–834

extended partitions, 310–312

extended read/write times in hard drives, 364

Extended Unique Identifier, 64-bit (EUI-64), 776

extensions

File Explorer, 473–474

Web browsers, 891–892

external batteries, 1065

external CLI commands, 607

external data bus (EDB) for CPUs, 68–71, 76–77

external drives for Windows installation, 429

external graphics processing units (eGPUs), 731

external hard drive enclosures, 286

external hardware tokens, 562

external interference in wireless networks, 862

external monitors

mobile devices, 1070

portable devices, 969

external power banks for mobile devices, 1051

external SATA (eSATA), 286

external speakers for mobile devices, 1050

external USB wireless network adapters, 830

Extreme Memory Profile (XMP), 131

extruders in 3-D printers, 1157

F

F-type connectors, 751

fabless semiconductor companies for CPUs, 85

fabrication companies for CPUs, 85

facial recognition

authentication, 519

mobile devices, 1079–1080

smartphones and tablets, 1180–1181

facility security, 1172–1174

factory resets for mobile devices, 1059

faded prints from laser printers, 1154

failed login attempt restrictions, 1079

Failed status in Disk Management, 337

fake security warnings in mobile applications, 1091

false alerts from malware, 1189

fans

cases, 263

CPUs, 111

dust, 1234

grinding noises, 682

motherboard support, 203

noises, 264–265

overheating, 680

portable devices, 982, 997

power supplies, 262

projectors, 722

system setup utility, 175

video cards, 706, 723–724

Fast Ethernet networks, 743

fast startup feature, 669

FAT (file allocation table) system

cluster size, 322

fragmentation, 322–325

overview, 318–320

working with, 320–322

fax components, 1122

fdisk tool, 315

feature updates in patch management, 552

feed assemblies in thermal printers, 1107

feeders

inkjet printers, 1103

laser printers, 1156–1157

scanners, 1117

fences, 1172

fetch stage in CPUs, 92–93

FHD monitor resolution, 725

fiber optic cable

Internet, 874–875

standards, 748–750

fiber-to-the-node (FTTN), 874

fiber-to-the-premises (FTTP), 874

field replaceable units (FRUs), 234

fields in IPv6 addresses, 774–775

FIFO (first in, first out) rotation backup scheme, 579

file allocation table (FAT) system

cluster size, 322

fragmentation, 322–325

overview, 318–320

working with, 320–322

File Explorer

extensions settings, 473–474

general options, 52–53, 474

introduction, 472

Show Hidden Files option, 472–473

view options, 473–474

File History applet, 585

file servers, 815–816

file structures and paths

Linux, 56

macOS, 56

Windows, 52–55

file systems

checking, 624

exFAT, 329–330

FAT 32, 318–325

in formatting, 317–318

Linux, 330

macOS, 330

NTFS, 325–329

Windows, 318–330

File Transfer Protocol (FTP)

application protocols, 886

functions and ports, 888

overview, 913

files

associations, 52

copying and moving, 621–624

deleting, 620–621

extensions, 52

finding, 632–633

Linux, 617

names, 605

offline, 980–981

ownership, 521

paths, 604, 611

permissions. See NTFS permissions

plaintext, 618–619

sharing, 530–532, 912–914

sound formats, 399

synchronization in cloud, 954–955

transferring, 911–914

wildcards, 619–620

working with, 617–618

FileVault storage encryption, 502

FileZilla client, 913

Filter Keys app, 470

filter masks, 19

filters

DSL, 872

grep, 632

IP addresses, 1176

MAC addresses, 837, 850–851, 1176

privacy, 1175

find command, 632–633

Find My iPhone app, 1012–1013

Finder in macOS, 56

findings, documenting, 24–25

fingerprint locks for mobile devices, 1080

fingerprint scanners

Apple keyboard, 1179–1180

authentication, 386, 519

portable devices, 985

smartphones, 387

finishing issues in printers, 1146

fire safety

burning smells, 680–681

equipment, 18–19

power supplies, 268

firewalls

hardware, 1200–1204

introduction, 1200

mobile devices, 1085–1086

software, 1204–1210

firmware

CMOS, clearing, 182–183

CMOS, lost settings, 183–185

controllers, 153–155

default and optimized settings, 181–182

introduction, 153–154

keyboard, 157–160

laser printers, 1112

mobile devices, 1035–1037

POST, 178–181

review questions, 186–189

ROM, flashing, 185–186

ROM, overview, 160–161

routers, 884–885

setup settings. See system setup utility

WAPs, 860

first in, first out (FIFO) rotation backup scheme, 579

first response in incidents, 1240

Fish shell, 597

flash drives

backups, 577

bootable, 405, 1198

booting from, 429

file systems, 329–330

overview, 404–405

flash memory, 404–407

flash ROM

motherboards, 161

RAID configuration, 295

flashing

BIOS, 229

ROM, 185–186, 1112

flashing screens, 718

flat-panel video displays, 688–691

flatbed scanners, 1117–1119

flickering displays, 998

floating point units (FPUs) in CPUs, 94

FN (Function) key in portable devices, 962

Folder Options settings, 53

folder redirection, 814

folder trees, pruning and grafting, 622–624

folders

access, 804–806

Active Directory, 809–810

CLI, 603–605

mounting partitions as, 348–350

names, 605

ownership, 521

permissions. See NTFS permissions

shared, 533

sharing, 530–532, 801–804

follow-up in effective communication, 10–11

footers setting for printers, 1139

for loops, 645

force stopping applications, 1057–1058

Foreign drive status, 337

form factors

hard drives, 276

motherboards, AT, 194–196

motherboards, ATX, 195–197

motherboards, description, 192

motherboards, ITX, 197–198

motherboards, proprietary, 198

solid-state drives, 277–279

format command

overview, 624–626

partitions, 662

formats for CD media, 408

formatting hard drives

data destruction in, 451

errors, 361

file systems. See file systems

format command, 624–626

installation media, 332–334

overview, 317–318

partitions, 351–352, 662

Formatting status in Disk Management, 337

forwarding, port, 1202

Fourth Extended File System (ext4), 330

Fox and Hound toners, 821

FPUs (floating point units) in CPUs, 94

fragmentation in FAT 32 file system, 322–325

frames, NIC processing of, 740–743

FreeSync technology, 730

freezes in mobile devices, 1069–1070

frequencies

IEEE 802.11 versions, 842

sound, 398

front panel connectors for sound support, 203

front-view projectors, 691–692

FRUs (field replaceable units), 234

fsck tool, 356

FTP (File Transfer Protocol)

application protocols, 886

functions and ports, 888

overview, 913

FTTN (fiber-to-the-node), 874

FTTP (fiber-to-the-premises), 874

full backups, 576

Full Control permissions, 522–523, 803

full-duplex mode in NICs, 791–792

full facial recognition, 1180–1181

full formatting file systems, 319

Full-Speed USB, 371–372

Function (FN) key in portable devices, 962

fuser assemblies in laser printers, 1111, 1154

fuses

overview, 235–236

power supplies, 268

fusing step in laser printers, 1128, 1155

fuzzy images, 722

G

G-sync technology, 730

gain, antenna, 845

game controllers

mobile devices, 1051

overview, 391–393

gaming laptops, 961

Gaming section in Windows setting, 467

garbage print, 1146

gateways

Internet, 870–871

LANs, 771

GDDR (Graphics DDR), 703

GDI (graphical device interface), 1116

gear packs in laser printers, 1111

General Data Protection Regulation (GDPR), 1237

general protection faults (GPFs), 149

general-purpose ports in portable devices, 972–974

general-purpose registers in CPUs, 72

General tab

card drivers, 716

encryption, 534

File Explorer, 474

folders, 53–54

Internet Options, 899

System Configuration, 463

geotracking, 1013

gestures

mobile devices, 1019

multi-touch, 385

Get-Command cmdlet, 607

Get-Help command, 606

Get-Location cmdlet, 607

GFS (grandfather-father-son) backup rotation scheme, 579

gibi prefix, 83

Gigabit Ethernet networks, 743

gigabytes, 82

GIMP (GNU Image Manipulation Program), 1118–1119

global positioning system (GPS) services

battery usage, 1067

mobile applications, 1095

mobile devices, 1011–1012, 1072–1074

portable devices, 999

Global System for Mobile Communications (GSM), 876, 1036

global unicast IP addresses, 777–779

global user account authentication, 509

globally unique identifiers (GUIDs), 314

GMA (Graphics Media Accelerator), 703

Gnome 3 launch point in Linux, 62

GNOME Terminal, 600

GNU Image Manipulation Program (GIMP), 1118–1119

goggles, 19

Golden Rule, 5

Google Pay system, 1022–1023

Google Play store, 1019, 1032

.gov domain, 780

government regulations, compliance with, 17

GPFs (general protection faults), 149

gpresult command, 627

GPRS technology, 876

GPS. See global positioning system (GPS) services

GPTs (GUID partition tables), 308, 313–314

gpupdate command, 626

GPUs (graphics processing units)

display adapters, 701–703

integrated, 100, 703–704

software requirements, 561

grafting folder trees, 622–624

Grand Unified Bootloader (GRUB), 310

grandfather-father-son (GFS) backup rotation scheme, 579

Graphic Device setup option, 172

graphical device interface (GDI), 1116

graphical mode errors in Windows installation, 447

graphical user interfaces (GUIs)

description, 32

mobile devices, 1019

graphical user interfaces (GUIs) programs, opening from command line, 599

graphics, software requirements for, 560–561

Graphics DDR (GDDR), 703

Graphics Media Accelerator (GMA), 703

graphics processing units (GPUs)

display adapters, 701–703

integrated, 100, 703–704

software requirements, 561

gray-to-gray (GtG) monitor response rate, 727

grayscale depth in scanners, 1120–1121

grep command, 632

grinding noises

causes, 682

hard drives, 364

printers, 1145–1146

grounding equipment, 14, 242

Group Policy Driver Installation policy, 1131

Group Policy Editor, 424–425, 538

groups

authenticating, 508–510

configuring, 511–516

creating, 514–516

default, 512–513

introduction, 507

Linux permissions, 527–528

policies, security, 1182–1184

policies, updating, 626–627

policies, Windows 10 Pro, 424–425

review questions, 547–549

security, 1181–1184

types, 510

GRUB (Grand Unified Bootloader), 310

GSM (Global System for Mobile Communications), 876, 1036

GtG (gray-to-gray) monitor response rate, 727

guards

access control vestibules, 1166

tools for, 1173

guest networks, 836–837, 1206–1207

Guest users, 511

guests and guest accounts

security, 1182

virtualization, 928

Guests group, 511

GUID partition tables (GPTs), 308, 313–314

GUIDs (globally unique identifiers), 314

GUIs (graphical user interfaces)

description, 32

mobile devices, 1019

GUIs (graphical user interfaces) programs, opening from command line, 599

gyroscopes, 1019

H

habits, automating, 641–642

half-duplex mode

fiber optic cable, 749

NICs, 791–792

hand tools for laptop disassembly, 986

Hard Drive Initialization Wizard, 336

hard drives

backups, 577

bootable media, 331–332

cleaning up, 359–360

connecting, 280–288, 297–298

copying, 637

corrupted, 362–363

data destruction, 451–452

defragmentation, 358

dying, 364–365

dynamic disks, 312–313

error checking, 356–357

file systems. See file systems

form factors, 276

formatting. See formatting hard drives

grinding noises, 682

GUID partition tables, 313–314

heat issues, 297

installing, 302, 361

laptop upgrades, 990–991

low-level formatting, 451

maintaining, 356–361

managing. See Disk Management program

master boot records, 308–312

partitions. See partitions

RAID issues, 365–366

review questions, 366–368

selecting, 296–297

space used, 637–638

speed, 275–276

spindle speed, 275–276

SSDs. See solid-state drives (SSDs)

Storage Spaces, 352–355

troubleshooting, 361–366

types, 273

hard tokens in authentication, 1178–1179

hardware

authentication, 1177–1181

black screen issues, 678

computing, 37–41

description, 32

failures, 1169

mobile device enhancements, 1025–1029

replacing in laptops, 991–995

virtual machines, 935–936

wireless networks, 859

hardware-assisted virtualization, 170

hardware firewalls, 1200–1204

hardware RAID, 293–295

hardware tokens, 562

hardware virtualization

benefits, 930–933

client-side, 929–930

introduction, 927–929

purpose, 933–935

server-side virtualization, 945

virtual machines. See virtual machines (VMs)

harmonics in power supplies, 256

hash tables, 1164

hashing

passwords, 1164

Web browsers, 890

hazardous materials, 1235–1236

HBAs (host bus adapters), 283

HBM (High Bandwidth Memory), 703

HD monitor resolution, 725

HDBaseT connectors, 697

HDCP (High-bandwidth Digital Content Protection), 702

HDMI (High-Definition Multimedia Interface)

connectors, 695

ports, 968

headers

mobile devices, 1050

motherboards, 202

printers, 1139

headphones, Bluetooth, 968

headset jacks, 967

headsets, 402

health of batteries, 996

healthcare data, 1238

heat dope for CPUs, 110

heat issues

CPUs, 114–115

hard drives, 275, 297

laser printers, 1154

mobile devices, 1063–1064

portable devices, 981–982, 997

projectors, 722

troubleshooting, 679–680

video cards, 705–706, 724

heat-sensitive thermal paper, 1107

heat sinks for CPUs, 107–111

heating elements in thermal printers, 1107, 1149

heating, ventilation, and air conditioning (HVAC) systems, 1233–1235

heavy boxes, 18

help command for CLI commands, 607

HEW (high efficiency wireless), 841–842

hexadecimal notation for MAC addresses, 740–741

hextets in IPv6 addresses, 774–775

HFS+ (Hierarchical File System Plus)., 330

Hi-Speed USB, 371–372

hibernate mode in portable devices, 977

hidden partitions, 314

Hide protected operating system files option, 472

hiding file extensions, 473

Hierarchical File System Plus (HFS+)., 330

high availability, cloud for, 954

High-bandwidth Digital Content Protection (HDCP), 702

High Bandwidth Memory (HBM), 703

High contrast video settings, 713

High-Definition Multimedia Interface (HDMI)

connectors, 695

ports, 968

high dynamic range, 729–730

high efficiency wireless (HEW), 841–842

high-level formatting of file systems, 319

high network traffic in mobile applications, 1090–1091

high-pitched squeals in hard drives, 364

high-resolution monitors, troubleshooting, 719–720

hijacked e-mail accounts, 1189

hijacking, session, 1164

hints for passwords, 518

hives in Registry, 458

HKEY_CLASSES_ROOT root key, 458–459

HKEY_CURRENT_CONFIG root key, 459

HKEY_CURRENT_USER root key, 459

HKEY_LOCAL_MACHINE root key, 459

HKEY_USERS root key, 459

hole punches for printers, 1146

home directories in CLI, 605

home folders in domains, 814

home theater PCs (HTPCs), 222

honesty, 3–5

horizontal cabling, 754–755

host bus adapters (HBAs), 283

host computers in virtualization, 927

host controllers for USB ports, 370–371

host IDs in IP addresses, 772–773

hostname command, 626

hosts, network, 735–738

hosts file, malware in, 1190

hot components, 18–19

hot-swappable drives for Windows installation, 429

hot swapping

hard drives, 285

RAID, 294

hotspots

IEEE 802.11, 841

locating, 846

mobile, 877, 1049–1050

tethering, 878, 1049–1050

HTPCs (home theater PCs), 222

HTTP (Hypertext Transfer Protocol)

functions and ports, 888

purpose, 886

HTTP over TLS protocol, 1213

HTTPS (Hypertext Transfer Protocol Secure)

encryption in, 886–887

functions and ports, 888

hubs

Ethernet, 744–745

USB, 370, 376–377

humidity issues, 1233–1235

HVAC (heating, ventilation, and air conditioning) systems, 1233–1235

hybrid clouds, 952–953

hybrid cores in CPUs, 116

hybrid laptops, 961

hybrid topologies, 744

Hypertext Transfer Protocol (HTTP)

functions and ports, 888

purpose, 886

Hypertext Transfer Protocol Secure (HTTPS)

encryption in, 886–887

functions and ports, 888

hyperthreading CPUs, 98

hypervisors

types, 945

virtualization, 927–928, 930

I

I-Cache in CPUs, 99

IaaS (Infrastructure as a Service), 948–949

ICANN (Internet Corporation for Assigned Names and Numbers), 780

ICC (International Color Consortium) color profiles, 1139–1140

ICCID (Integrated Circuit Card Identifier) numbers, 1037

iCloud service

e-mail, 900, 1038

Find My iPhone app, 1012

Keychain, 502, 1031

location services, 1080–1081

synchronization, 500, 1041, 1043–1044

ICSs (industrial control systems), 915

ID badges for facility security, 1174

IDE (Integrated Drive Electronics) drives, 282

identification in workgroups, 800–801

IDs, RFID, 1221

IDSs (intrusion detection systems), 1210

IE (Internet Explorer), 897–898

IEC-320 connectors, 237–238

IEEE 802.11-based wireless networking

802.11a, 840

802.11ac, 841–842

802.11ax, 841–843

802.11b, 840

802.11g, 840

802.11n, 841–842

components, 829

introduction, 838–839

portable devices, 970–971

Wi-Fi channels, 839–840

IETF (Internet Engineering Task Force), 774

if statements in scripts, 645

ifconfig command, 785

iFixit toolkits

benefits, 16–17

laptop disassembly, 988

IIS (Internet Information Services), 736

images

backups, 584

projector technologies, 692

reimaging computers, 660

Windows deployment, 432–433

Windows installation errors, 448

imaging drums in laser printers, 1109, 1153

imaging process in laser printers, 1108, 1124–1125

IMAP (Internet Message Access Protocol)

e-mail, 900

functions and ports, 888

mobile devices, 1039–1041

IMCs (integrated memory controllers), 100

IMEI (International Mobile Equipment Identity) numbers, 1036

impact determination in change management, 1231–1232

impact paper, 1103

impact printers

description, 1103

troubleshooting, 1148–1149

impedance in coaxial cable, 750

impersonation in social engineering attacks, 1166

improper charging

batteries, 996

mobile devices, 1068

IMSI (International Mobile Subscriber Identity) numbers, 1037

IMT-2020 specifications, 877

in-place Windows upgrades, 431

in-plane switching (IPS) panels

mobile devices, 1009

overview, 689–690

portable devices, 966

incident reports, 25

incident response, 1240–1241

incomplete characters in laser printers, 1156

incorrect chroma display in printers, 1147

incremental backups, 576

indexes, package, 634

Indexing Options applet, 469–471

industrial control systems (ICSs), 915

industrial, scientific, and medical (ISM) radio bands, 839

industry standard architecture (ISA) for CPUs, 85

infiltration in social engineering attacks, 1166

Information event levels in Event Viewer, 491

information gathering

scripts, 641

social engineering attacks, 1166–1167

Information tab in system setup utility, 169, 171

Infrared Data Association (IrDA) standard, 1049

infrared for mobile devices, 1049

Infrastructure as a Service (IaaS), 948–949

infrastructure of wireless networks, 833–834

inheritance of NTFS permissions, 523–525

init system, 556

initialism in monitor resolution, 725

initialization of disks, 336–338

injection attacks, 1165

injectors, PoE, 832

inkjet printers

maintaining, 1150–1152

overview, 1103–1107

problems, 1152

input devices for portable devices, 962–965

input in computing process, 35

input/output operations per second (IOPS)

SD cards, 407

solid-state drives, 280

input problems in portable devices, 999–1001

input validation in SQL injection, 1165

insider threats, 1168

installation media for partitioning and formatting, 332–334

installing

applications, 641

CPUs, 104–114

device drivers, 213–215

expansion cards, 209–217

hard drives, 361

KVM switches, 391

LANs, wired, 791–797

mass storage, 296–302

motherboards, 223–226

NICs, 791–795

optical media, 414–415

power supplies, 259–261

printers and multifunction devices, 1114, 1124, 1130, 1132–1137

RAM, 145–148

software, 559–569

video, 705–706

virtual machine OS, 942–944

virtual machines, 939

Web browsers, 890–891

Windows. See Windows operating system

instruction sets for CPUs, 73, 85

insulators, 235

.int domain, 780

integer units in CPUs, 94

integers in scripts, 644

integral parts, replacing, 994–995

Integrated Circuit Card Identifier (ICCID) numbers, 1037

Integrated Drive Electronics (IDE) drives, 282

integrated e-mail solutions, 900

integrated GPUs, 561, 703–704

integrated memory controllers (IMCs), 100

integrated print servers, 1124

Integrated Services Digital Network (ISDN), 872

integrity, 3–5

Intel 8088 CPU, 68

address bus, 81–83

clock speed, 75

command size, 123–124

EDBs, 77, 79

machine language, 72–73

Intel Core i7 CPUs, 87

Intel Extreme Tuning Utility (Intel XTU), 112

Intel Virtual Technology option, 170

Intel Virtualization Technology (Intel VT), 170

intelligent controllers for RAID, 294

interconnecting LANs, 769–771

interface IDs in IPv6 addresses, 776–777

interference

description, 15–16

EMI, 15

power lines, 244

RFI, 15–16

STP cable, 746

wireless networks, 843, 861–862

intermittent problems from power supplies, 267

intermittent shutdowns

CPUs, 115

projectors, 722

intermittent wireless connectivity, 860

internal connectors for motherboards, 202

internal networks for virtual machines, 938

International Color Consortium (ICC) color profiles, 1139–1140

International Mobile Equipment Identity (IMEI) numbers, 1036

International Mobile Subscriber Identity (IMSI) numbers, 1037

Internet

appliances, 909, 1210–1211

application protocols, 886–888

browsing. See Web browsers

cable, 873–874

cellular, 876–878

communicating on, 899–900

connecting to, 879–880

connection concepts, 870–871

connectivity issues, 917–919, 1092

desktop management software, 912

DSL, 872–873

e-mail, 900–903

embedded systems, 914–916

fiber, 874–875

file transfer software, 911–912

files, deleting, 359

introduction, 867

ISPs, 870

latency and jitter, 922–923

mobile devices, 1092

operation, 867–869

remote access, 904–908

remote monitoring and management, 912

review questions, 924–926

routers, 880–885

satellite, 879

sharing and transferring files, 912–914

slow speed issues, 919–922

TCP/IP, 870–871

troubleshooting, 916–924

video conferencing, 908

virtual private networks, 908–911

VoIP issues, 923–924

VoIP overview, 903–904

Wi-Fi, 875

WISP, 876

Internet Corporation for Assigned Names and Numbers (ICANN), 780

Internet Engineering Task Force (IETF), 774

Internet Explorer (IE), 897–898

Internet Information Services (IIS), 736

Internet Message Access Protocol (IMAP)

e-mail, 900

functions and ports, 888

mobile devices, 1039–1041

Internet of Things (IoT), 915–916

Internet Options applet, 897–899

Internet service providers (ISPs)

Internet, 870

LANs, 771

interpolation in monitor resolution, 724

interpreters, command-line, 597

interrupts, NMIs, 148

intrusion detection systems (IDSs), 1210

intrusion prevention systems (IPSs), 1210–1211

inventory lists, 1220

invert setting for printers, 1138

invoices, procurement, 1222

IOPS (input/output operations per second)

SD cards, 407

solid-state drives, 280

iOS operating system

airplane mode, 1023

apps, 1030–1031

cellular data, 1072

expansion options, 1027

facial recognition, 1083

Find My iPhone app, 1012–1013

jailbreaks, 1093–1094

Lightning standard, 1046

mobile devices, 1016–1018

smartphones, 1008

synchronization, 1041

tech utility launch points, 63

tethering, 878

IoT (Internet of Things), 915–916

IP addresses

APIPA, 790

configuring, 795

DNS, 779–783

dotted-decimal notation, 772

filtering, 1176

global unicast addresses, 777–779

Internet, 880

IPv4, 772–774

IPv6, 774–777

LANs, 770

NAT, 1201

printers, 1133, 1135

routers, 881–884

subnet masks, 772–773

ip command, 785

iPad expansion options, 1026–1027

iPadOS operating system

apps, 1030–1031

e-mail, 1038

mobile devices, 1016–1018

synchronization, 1041

ipconfig command

cable troubleshooting, 818

Internet connectivity issues, 919

network settings, 785–786

ipconfig /all command

MAC addresses, 742

network settings, 785–786

ipconfig /flushdns command, 918

iPhones

Apple Pay, 1022

cameras, 1010

elements, 1006

expansion options, 1026–1027

facial recognition, 1181

Find My iPhone app, 1012–1013

hotspot mode, 878

introduction of, 1006–1007

Lightning connector, 1045

synchronization, 1041–1042

Wi-Fi calling, 1020

IPS (in-plane switching) panels

mobile devices, 1009

overview, 689–690

portable devices, 966

IPsec encryption, 1212

IPSs (intrusion prevention systems), 1210–1211

IrDA (Infrared Data Association) standard, 1049

ISA (industry standard architecture) for CPUs, 85

ISDN (Integrated Services Digital Network), 872

ISM (industrial, scientific, and medical) radio bands, 839

ISPs (Internet service providers)

Internet, 870

LANs, 771

ITX motherboards, 197–198

J

jacks

portable devices, 967–968

sound, 203, 400–401

jailbreaks, 1093–1095

jams

laser printers, 1156

staple, 1146

JavaScript language, 639

JBOD (just a bunch of disks), 291

jitter, Internet, 922

joining domains, 810

joules rating for surge suppressors, 243

joysticks, 391–393

.js files, 639

just a bunch of disks (JBOD), 291

K

KDE Plasma Desktop, 61–62

Keep my files option, 662

Kerberos authentication, 854, 1212

kernels, 929

key fobs

authentication, 1178

RFID, 1180

Keyboard Control Panel applet, 382–383

keyboard, video, mouse (KVM) switches, 390–391

keyboards

AT motherboards, 194–195

BIOS, 162

controllers, 157–160

display options, 968–969

mobile devices, 1029

on-screen, 470

overview, 382–385

portable devices, 962–963

power management, 979

replacing, 992

ROM, 160–161

settings, 435

shortcuts, 628–629

troubleshooting, 1000

UEFI, 161–162

Keychain feature, 501–502, 1031

keyloggers, 1186

keys, encryption, 1074

kibi prefix, 83

kill command, 631

kilobytes, 82

knowledge bases, 1228

knowledge factor in authentication, 1082

Konsole Terminal, 600

KVM (keyboard, video, mouse) switches, 390–391

L

L1 cache in CPUs, 95–96

L2 cache in CPUs, 96

L2TP (Layer 2 Tunneling Protocol), 1024

L3 cache in CPUs, 96

lamps in projectors, 693–694

land grid array (LGA) packages for CPUs, 104

Landscape mode in video, 710

language settings, 435, 465

languages

printer, 1115–1117

scripting. See scripting

LANs. See local area networks (LANs)

laptop computers. See also portable devices

description, 960

protecting, 1169

types, 961–962

laser printers

charging step, 1126–1127

cleaning step, 1129

components, 1108–1112

description, 1107–1108

developing step, 1127

exposing step, 1127

fusing step, 1128

imaging process, 1124–1125

processing step, 1125–1126

resolution, 1126

transferring step, 1128

troubleshooting, 1152–1157

latency

Internet, 922–923

RAM, 134–136

satellite connections, 879

solid-state drives, 280

wireless networks, 860

launchctl command, 558

launchd system, 556

launchers for mobile devices, 1019

launching issues with applications, 1063

law enforcement for incidents, 1240–1241

Layer 2 Tunneling Protocol (L2TP), 1024

layer shifting in 3-D printers, 1157

layers, motherboard, 192

Layout settings for printers, 1138

LBA (logical block addressing), 306–307

LC (lucent) connectors, 749

LCD (liquid crystal display)

panels, 688–691

portable device displays, 965–966

projectors, 692

LCI (liquid contact indicator) stickers, 1062

LDAP (Lightweight Directory Access Protocol)

e-mail, 807

functions and ports, 888

leases for IP addresses, 783

least privilege principle, 1181

LEDs. See light-emitting diodes (LEDs)

legacy software, 935

legacy systems

embedded, 915

Web servers, 738

length of USB cables, 376

less command, 619

letter quality impact printing, 1103

letters for drives, 604, 612

level of risk in change management, 1232

levels

access, 521

event, 491–492

UAC, 544–546

LGA (land grid array) packages for CPUs, 104

Li-Ion (Lithium-Ion) batteries, 975

licenses

asset management, 1222–1223

digital rights management, 1239–1240

EULA, 1239

open source, 1239

personal use vs. corporate use, 1238

validity and expiration, 1239

Windows installation, 433–434, 439

life cycle

operating systems, 553

procurement, 1222

lifting techniques, 18

light-emitting diodes (LEDs)

AC testers, 241

backlights, 965–966

fiber optic cable, 749

hard drives, 364

LCD panels, 690–691

monitor brightness, 726

motherboards, 224–225

NICs, 791–793

POST cards, 179

projectors, 693–694

light sources for projectors, 693–694

lighting for facility security, 1173

Lightning ports and connectors

expansion options, 1026–1027

mobile devices, 1045–1046

lightning strikes, 243

lights

cable troubleshooting, 818–819

NICs, 791–793

Lightweight Directory Access Protocol (LDAP)

e-mail, 807

functions and ports, 888

limited-Internet connectivity issues, 919

line in jacks, 400

line-interactive UPSs, 245

line of sight in infrared, 1049

line out jacks, 400

lines down printed page with laser printers, 1155

lines of code for CPUs, 73

link lights

cable troubleshooting, 818–819

NICs, 791–793

link-local addresses in IPv6, 776–777

link state of wireless networks, 861

Linux operating system

autostarting software, 558–559

backups, 586–587

CLI access, 600–602

CLI commands, 629–638

display settings, 713–715

drive changes, 612

file listings, 617

file structures and paths, 56

file systems, 330

patch management, 553–554

permissions, 527–529

running programs, 616–617

scheduling maintenance, 555–556

shells, 597

software installation, 567–569

software removal, 571–572

tech utility launch points, 61–62

user interface, 50

workgroups, 800

liquid contact indicator (LCI) stickers, 1062

liquid cooling for CPUs, 108–109

liquid crystal display (LCD)

panels, 688–691

portable device displays, 965–966

projectors, 692

liquid damage of mobile device displays, 1062

List Folder Contents permission, 522

listening rules, 7

lit pixels, 718

Lithium-Ion (Li-Ion) batteries, 975

load balancing in redundant power supplies, 268

Load Default Settings option, 181

loading MMC snap-ins, 485

local area networks (LANs)

addressing. See IP addresses

cables, 817–821

common problems, 822–825

domains, 806–815

file servers and drive mapping, 815–816

installing, wired, 791–797

interconnecting, 769–771

introduction, 751–752, 769

printer sharing, 816–817

review questions, 825–827

shared resources, 797–798

switch connections, 795–797

TCP/IP configuration, 789–790

TCP/IP settings, 784

TCP/IP tools, 784–789

TCP vs. UDP, 783–784

troubleshooting, 817–825

workgroups, 798–806

local hosts in networks, 735–736

local Internet connectivity issues, 919

local printers, installing, 1132–1134

Local Security Policy, 537–538, 1182–1183

local shares, 533

local snapshots in Time Machine, 585–586

local user account authentication, 508

local usernames in workgroups, 421–422

Local Users and Groups snap-in, 511–514

location factor in authentication, 1082

location services

battery usage, 1067

lost devices, 1079

mobile devices, 1011–1014, 1072–1074

tracking issues, 1095

lock down systems, 1174–1175

locks

biometric, 1179

facility security, 1174

fingerprint, 1080

laptops, 1169

portable devices, 984

screen, 1079–1080

screensaver, 1175

lockups

malware, 1189

from overclocking, 112

from RAM, 148–149

video cards, 723

Windows installation, 448

Log On Locally policy, 1184

logical addresses for LANs, 770

logical block addressing (LBA), 306–307

logical drives, 311–312

logical security, 1176

authentication, 1176–1181

MAC address filtering, 1176

policies, 1182–1185

users and groups, 1181–1182

logons for domains, 807–809, 813

logs

app errors, 1063

network printers, 1140

Windows installation, 448

Windows Logs, 490–491

long-range fixed wireless networks, 834, 846

Long Term Evolution (LTE) technology, 877

long-term servicing branch (LTSB), 427

loopback plugs in NICs, 819

loops in scripts, 644–645

lost chains in hard drives, 356

lost mobile devices, 1079–1080

loud noises on motherboards, 226–227

low-level formatting of hard drives, 451

low memory warnings, 672

low-power modes for portable devices, 976

Low-Speed USB, 371–372

ls command, 610

LTE (Long Term Evolution) technology, 877

LTSB (long-term servicing branch), 427

lucent (LC) connectors, 749

lumens in projectors, 692–693


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
Skip to Content
Topics
Start Learning
Featured
Search 50,000+ courses, events, titles, and more


Index
CompTIA A+ Certification All-in-One Exam Guide, Eleventh Edition (Exams 220-1101 & 220-1102), 11th Edition
CompTIA A+ Certification All-in-One Exam Guide, Eleventh Edition (Exams 220-1101 & 220-1102), 11th Edition
42h 21m remaining
M

M.2 form factor

laptops, 990–991

solid-state drives, 277–279

M1 chips, 704

MAC (media access control) addresses

filters, 837, 850–851, 1176

NICs, 740–741

searches, 742

machine language commands, 73

macOS operating system

AirDrop, 501

Apple ID, 500–501

autostarting software, 558–559

backups, 585–586

CLI access, 600–602

CLI commands, 629–638

display settings, 713–715

drive changes, 612

file structures and paths, 56

file systems, 330

FileVault, 502

Keychain, 501–502

maintenance scheduling, 555–556

patch management, 553–554

permissions, 527–529

preferences and features, 493–502

preferences overview, 493–494

running programs, 616–617

software installation, 565–567

software removal, 570–571

Spotlight, 501

System Preferences, 494–499

tech utility launch points, 60–61

user interface, 47–49

workgroups, 800

Made for iPhone (MFi) program, 1046

magic packets, 793–794

Magic Trackpad, 385

magnetic readers in mobile devices, 1048–1049

magnetic tapes for backups, 577

magnetometers, 1172

Magnifier app, 470

mail exchanger (MX) records, 781

mail servers, 738

main speaker out jacks, 400

Main tab in system setup utility, 166–167

maintaining

hard drives, 356–361

laser printers, 1153–1154

malicious actors, 1162–1163

malicious software

APKs, 1094

network security, 1185–1189

malware

anti-malware, 1191–1194

behavior, 1186–1189

education about, 1194, 1199–1200

forms, 1185–1186

mobile devices, 1077–1079

networks, 1170

prevention and recovery, 1191–1200

prevention tips, 1194–1196

recognizing and quarantining, 1197

recovery tips, 1196

remediation, 1198–1199

scripts, 643

searching for and destroying, 1197–1198

signs and symptoms, 1189–1191

sluggish performance, 668

Malwarebytes program, 1192–1193

MAM (mobile application management), 1075

man-in-the-middle attacks, 1163

man pages for CLI commands, 606

Managed Apple IDs, 501

managed file transfer, 912

managed switches for LAN connections, 796

management involvement in incidents, 1240–1241

MANs (metropolitan area networks), 875

mantraps, 1166

manual feed printer paper, 1138

manuals for motherboards, 221–222

Map Network Drive dialog box, 815

mapping

bad blocks, 319

drives, 641, 815–816

network shares, 823

ports, 1202

printers, 1137

marker threads for patch cables, 762

masks

air filter, 19

subnet, 772–773

mass storage

AHCI, 302

boot order, 301

CMOS settings, 299–302

connecting, 280–288

drives. See flash drives; hard drives; solid-state drives (SSDs)

installing, 296–302

introduction, 273

RAID, 288–295

review questions, 302–304

selecting, 296–297

troubleshooting installation, 302

master boot records (MBRs)

hard drives, 308–312

protective, 314

master file tables (MFTs), 326–327

matching RAM, 144

material safety data sheets (MSDSs)

hazardous materials, 1236

printers, 1147

mats, ESD, 13

Maximum password age setting, 538–539

MBRs (master boot records)

hard drives, 308–312

protective, 314

MCCs (memory controller chips), 80–82, 123–125

md command, 613–614

MDM (mobile device management)

policies, 1075

software, 1037

mDP (Mini DisplayPort), 696

mebi prefix, 83

mechanical off mode for portable devices, 976

media access control (MAC) addresses

filters, 837, 850–851, 1176

NICs, 740–741

searches, 742

Media Creation Tool, 434

media for backups, 577–578

media in Windows installation

errors, 447

sources, 428–430

megabytes, 82

memory

address bus, 80–84

display adapters, 703

graphics processors, 702

laptops, 989–990

laser printers, 1112

low memory warnings, 672

overview, 78

printer troubleshooting, 1142

RAM. See dynamic random-access memory (DRAM); random-access memory (RAM)

raster image processors, 1125–1126

Task Manager, 477–478

video cards, 723

virtual, 138–142

virtual machines, 937

memory cards, 404–405

memory controller chips (MCCs), 80–82, 123–125

memory controllers, 100

memory leaks, 652

Memory tab in Resource Monitor, 484

Memtest86+ software, 149–150

mental reinstallation of hard drives, 362

menu bars in macOS, 47

menus for video displays, 698–699

mesh networks, 835

metal detectors, 1172

metered cloud utilization, 954

metered Internet connections, 878

meters

AC supply tests, 237–238, 240–241

printer troubleshooting, 1142

metric system for memory, 82–83

metropolitan area networks (MANs), 875

MFA (multifactor authentication)

mobile devices, 1082–1083

security, 1176–1177

wireless networks, 853

MFDs (multifunction devices). See printers and multifunction devices

MFi (Made for iPhone) program, 1046

MFTs (master file tables), 326–327

mice, 385

Micro-B USB connectors, 374

Micro-B 3.0 USB connectors, 374

micro-DIMM packages, 128

Micro-HDMI ports, 1028

micro-USB ports, 1045

microarchitectures for CPUs, 86–88

microATX motherboards

description, 195, 197

power supplies, 255

microfilters, DSL, 872

microLED (µLED) displays, 731

Micron site, 123

microphones

activation issues, 1095–1096

description, 401

jacks, 400

mobile devices, 1011

portable devices, 965

video displays, 700

webcams, 397

microprocessors. See central processing units (CPUs)

microSD cards

Android devices, 1051

description, 406

mobile devices, 1025

slots for, 1028

Microsoft Management Console (MMC)

Certificate Manager, 492–493

Event Viewer, 489–492

Local Users and Groups, 531

overview, 484–486

Performance Monitor, 486–489

Task Scheduler, 555

Windows, 57–60

Microsoft Remote Assistance (MSRA), 906

Microsoft Store, 47

migrating systems in Windows installation, 450–452

.mil domain, 780

MIMO (multiple in/multiple out) feature, 841

Mini-B USB connectors, 374

mini connectors, 248

Mini DisplayPort (mDP), 696

mini-ITX motherboards

description, 197–198

power supplies, 255

mini-USB ports, 1045

Minimum Password Length policy, 1184

miniSD memory cards, 406, 1051

mirror spaces, 353–354

mirrored volumes in dynamic disks, 313, 346–347

mirroring, RAID, 203, 289–290, 292

misaligned printing, 1146

misfeeds in inkjet printers, 1152

missing boot device in Windows installation, 447

Missing Drive in OS message in RAID, 365

missing operating systems, 674–675

Mission Control in macOS, 48–49

mkdir command, 613–614

MLC (multi-level cell) memory technology, 279

MMC. See Microsoft Management Console (MMC)

mmc command, 615–616

MMX (multimedia extensions) in CPUs, 91

mobile application management (MAM), 1075

mobile applications

behavior issues, 1091

camera and microphone activation issues, 1095–1096

connection issues, 1091–1092

location tracking issues, 1095

resource issues, 1090–1091

unauthorized data access, 1092–1095

mobile device management (MDM)

policies, 1075

software, 1037

mobile devices. See also portable devices

Airplane mode, 1023

application security, 1086–1096

apps, 1029–1033

BYOD vs. corporate-owned, 1075

cameras, 1010–1011

communication and ports, 1045–1051

CPUs, 88–89

data, 1038

data security, 1081–1086

digitizers, 1011

e-mail, 900, 1038–1041

emergency capabilities, 1022

encryption, 1074

firewalls, 1085–1086

hardware enhancements, 1025–1029

introduction, 1005–1006

location services, 1011–1014

lost, 1079–1080

malware, 1077–1079

microphones, 1011

multifactor authentication, 1082–1083

network connectivity, 1033–1037

operating systems, Android, 1018–1019

operating systems, development models, 1014–1016

operating systems, features, 1019–1025

operating systems, iOS and iPadOS, 1016–1018

payment services, 1022–1023

physical damage protection, 1076–1078

profile requirements, 1076

review questions, 1052–1054

screen technologies, 1009–1010

securing, 1074–1086

smartphones, 1006–1008

software development kits, 1021–1022

synchronization, 1041–1045

tablets, 1008–1009

theft recovery, 1080–1081

troubleshooting. See troubleshooting mobile devices

user interfaces, 1019

variants, 1006–1009

virtual assistants, 1020–1021

virtual private networks, 1023–1025

Wi-Fi calling, 1020

mobile hotspots, 877

model names for CPUs, 86

modems

cable, 750–751, 874

DSL, 872–873

fiber, 874

Internet, 872, 874

satellite, 879

VoIP, 903–904

modifier keyboard keys, 383

Modify permission, 522

modular power supplies, 268–269

Molex connectors in power supplies, 248, 250

monaural sound, 398

monitors

adaptive sync, 730

brightness, 726

cleaning, 720–721

color depth, 728–729

contrast ratio, 728

dynamic range, 729–730

eGPUs, 731

evaluating, 724–730

external, 1070

microLED, 731

panel technology, 729

portable devices, 969

PPI, 726

privacy, 721

refresh rate, 727

resolution, 724–725

response rate, 727

review questions, 731–734

troubleshooting, 718–721

viewing angle, 726–727

more command, 618–619

motherboards

case fan support, 203

cases, 220–223

chipsets, 192, 199–201

choosing, 220–223

display adapter slots, 700–701

expansion buses. See expansion buses and cards

form factors, 192–198

installing, 223–226

introduction, 191–192

layers, 192

networking support, 203

power supplies, 266–267

power to, 247–248

RAID support, 203

review questions, 230–232

sound support, 203

speaker connections, 399

standard components, 202

technical manuals, 221–222

troubleshooting, 226–229

USB ports, 202–203

video support, 203

motion sensors in facility security, 1173

mount points, 348, 350

mounting

CLI process, 603

partitions as folders, 348–350

mounts for video displays, 698–699

Mouse Control Panel applet, 385

moved files, NTFS permissions for, 525–526

Movieland service, 1187

moving files, 621–622

moving-picture response time (MPRT) for monitors, 727

mSATA form factor

laptops, 990–991

solid-state drives, 277–278

msconfig command, 463–464

MSDSs (material safety data sheets)

hazardous materials, 1236

printers, 1147

msinfo32.exe (System Information Utility)

NICs, 741

version identification, 427

MSRA (Microsoft Remote Assistance), 906

MU-MIMO (Multiuser MIMO) feature, 841

multi-level cell (MLC) memory technology, 279

multi-rail systems in power supplies, 253

multi-touch gestures, 385

multicast addresses, 777

multicore processing in CPUs, 99–100

multifactor authentication (MFA)

mobile devices, 1082–1083

security, 1176–1177

wireless networks, 853

multifunction devices (MFDs). See printers and multifunction devices

multimedia devices and formats

digital cameras, 395–396

removable storage devices, 404–415

sound components, 397–402

video formats, 402–403

webcams, 396–397

multimedia extensions (MMX) in CPUs, 91

multimeters

AC supply tests, 238–241

printer troubleshooting, 1142

multimode fiber optic cables, 749

multipage misfeeds

inkjet printers, 1152

laser printers, 1156

multipage printer setting, 1138

multiple Desktops in macOS, 48–49

multiple in/multiple out (MIMO) feature, 841

multiple monitors

privacy, 721

settings, 710

multithreading in CPUs, 98

multitouch trackpads in portable devices, 964

Multiuser MIMO (MU-MIMO) feature, 841

Music folder, 55

MUX switch for portable devices, 979

mv command, 621, 624

MX (mail exchanger) records, 781

N

NAC (network access control), 1079

names

files and folders, 605

folder shares, 803

NetBIOS, 824

partitions, 316–317

USB connectors, 374

virtual machines, 941

workgroups, 798–800

nano text editor, 635–636

Narrator app, 470

nasty silver goo for CPUs, 110

NAT (Network Address Translation)

firewalls, 1201

routers, 880

National Institute of Technology and Standards (NIST) for passwords, 518

native command queuing (NCQ) for hard drives, 287

native resolution in monitors, 724–725

nbtstat command, 824–825

NCQ (native command queuing) for hard drives, 287

Near Field Communication (NFC)

mobile devices, 1048

payment services, 1022

troubleshooting, 999

near-field scanners, 969

near-letter quality (NLQ) impact printers, 1103

negotiation in procurement, 1222

Nest smart thermostat, 916

nested RAID levels, 292

net command, 822–823

net config command, 823

.net domain, 780

net use command

administrator passwords, 547

network shares, 823

profile rebuilding, 664

net view command, 823

NetBIOS

functions and ports, 888

names, 824

NetBT functions and ports, 888

netstat command, 920

Network & Internet settings, 467

network access control (NAC), 1079

Network access dialog box for resource sharing, 531–532

Network Address Translation (NAT)

firewalls, 1201

routers, 880

Network and Sharing Center

NIC settings, 791

printers, 1133

Wake-on-LAN, 794

Network Discovery setting, 1207

Network File System (NFS) protocol, 797

network IDs in IP addresses, 772–773

network interface controllers (NICs), 830

cable, 818–819

description, 739–740

frames, 740–743

installing, 791–795

Internet, 874

LANs, 769–770

link lights, 791–793

QoS, 794–795

troubleshooting, 819

Wake-on-LAN, 793–794

Windows installation, 446

network names in wireless networks, 835

Network preferences pane, 496–497

network printers

installing, 1134–1137

security, 1140–1141

network protocols for LANs, 770

network security

authentication and encryption, 1211–1215

firewalls, 1200–1210

Internet appliances, 1210–1211

malicious software, 1185–1189

malware prevention and recovery, 1191–1200

malware signs and symptoms, 1189–1191

review questions, 1216–1218

wireless networks, 1215–1216

Network tab in Resource Monitor, 484

network taps, 1211

network topology diagrams, 1224–1225

network traffic in mobile applications, 1090–1091

Network troubleshooter, 918

networks

connections, 36

drive remapping, 641

Ethernet. See Ethernet networks

frames and NICs, 740–743

host roles, 735–738

Internet. See Internet

introduction, 735

LANs. See local area networks (LANs)

macOS settings, 496–497

malware, 1170

mobile application attacks, 1086–1087

mobile devices, 1033–1037

motherboard support for, 203

paths, 823

portable devices, 969–972

printers and multifunction connections, 1123–1124

resource sharing, 738

review questions, 766–768

scan services, 1121

software impact on, 563

technologies, 739–751

virtual machines, 937–938

Windows installation over, 445–447

wireless. See wireless networks

New Object - User dialog box, 811–812

New Simple Volume Wizard, 338–340, 342–343

New Technology File System (NTFS), 325–326

cluster sizes, 329

compression, 327–328

disk quotas, 328

encryption, 328

permissions. See NTFS permissions

security, 327

structure, 326–327

new-user setup checklists, 1226

NFC (Near Field Communication)

mobile devices, 1048

payment services, 1022

troubleshooting, 999

NFS (Network File System) protocol, 797

niche-market power supplies, 255

NICs. See network interface controllers (NICs)

Night light video setting, 708

NIST (National Institute of Technology and Standards) for passwords, 518

nits, 726

NLQ (near-letter quality) impact printers, 1103

NMIs (non-maskable interrupts), 148

no connectivity Internet issues, 917–918

noises

fans, 264–265

grinding, 682

motherboards, 226–227

printers, 1145–1146

non-compliant system vulnerabilities, 1171

non-contact thermometers, 18

non-expired licenses, 1239

non-maskable interrupts (NMIs), 148

Non-Volatile Memory Express (NVMe) specification, 287–288

nonoverlapping channels in 5-GHz band, 839

nonvolatile memory, 160–161

northbridge chipsets, 154–155, 199

Norton Ghost program, 433

notebook computers, 960

notification sound settings, 466

notifications area for background programs, 43

nozzles in inkjet printers, 1151

nslookup command, 786–787

NTFS. See New Technology File System (NTFS)

NTFS permissions

concepts, 521–522

inheritance, 523–525

introduction, 507

propagation, 525–526

resource sharing, 530–532

review questions, 547–549

technician issues, 526–527

NVMe (Non-Volatile Memory Express) specification, 287–288

NX bit technology for CPUs, 100–101

O

objects in Performance Monitor, 487–488

OCP (over-current protection) for rails, 253

OCR (optical character recognition) in scanners, 1119

octets in IP addresses, 772–773

OEM (original equipment manufacturer) coolers for CPUs, 107–108

Offline disk status, 338

offline files, designating, 980–981

offsite backup storage, 576

ohms, 235

OLED (organic light-emitting diode) panels, 688

mobile devices, 1009–1010

overview, 691

portable devices, 966

on-board NIC (BIOS) setting, 446

on-path attacks, 1163

On-Screen Keyboard, 470

onboarding new-user setup checklist, 1226

Online disk status, 338

online storage for backups, 577–578

online UPSs, 245

Only allow a magic packet to wake the computer option, 794

onscreen display (OSD) menus, 698–699

ONTs (optical network terminals), 874

oozing in 3-D printers, 1157

open-ended questions, 8

open source development models, 1015

open source licenses, 1239

operating procedures

acceptable use policies, 1224

asset management, 1220–1223

change management, 1228–1233

compliance, 1238

data classification, 1236–1237

documentation, 1223–1227

environmental controls, 1233–1236

incident response, 1240–1241

introduction, 1219

licenses, 1238–1239

regulated data, 1237–1238

review questions, 1242–1244

standard operating procedures, 1223–1227

ticketing systems, 1227–1228

operating system maintenance and optimization

backups, 575–587

introduction, 551

patch management, 552–554

performance options, 572–575

review questions, 591–593

scheduling maintenance, 554–556

software, autostarting, 556–559

software, distribution methods, 562–563

software, installing, 559–569

software, removing, 569–572

system restores, 587–590

operating systems (OSs)

Android. See Android operating system

description, 32–33

development models, 1014–1016

functions, 41–42

introduction, 457

iOS. See iOS operating system

iPadOS. See iPadOS operating system

lifespans, 1171

Linux. See Linux operating system

macOS. See macOS operating system

maintenance and optimization. See operating system maintenance and optimization

missing, 674–675

OS-based lockups, 1189

primary partitions, 310–311

Registry, 457–462

reinstallation for malware prevention, 1197

review questions, 503–505

smartphones, 63, 1008

supervisors, 929–930

tech utility launch points, 56–63

troubleshooting. See troubleshooting operating systems procedures

virtual machines, 942–944

Windows. See Windows operating system

operations, software impact on, 563–564

optical character recognition (OCR) in scanners, 1119

optical drives

backups, 577

bootable, 1198

optical media

CD, 408–411

DVD, 411–414

installing, 414–415

overview, 408

optical network terminals (ONTs), 874

optical resolution of scanners, 1120

optimization

operating systems. See operating system maintenance and optimization

printers, 1139–1140

wireless network coverage, 843–846

Optimize Drives tool, 325, 358

optimized battery charging, 975

Optional features settings page, 572–573

.org domain, 780

organic light-emitting diode (OLED) panels, 688

mobile devices, 1009–1010

overview, 691

portable devices, 966

organization e-mail, 902–903

organizational policies, 1224

organizational units (OUs), 814, 1183

orientation

autorotation problems, 1060

mobile device screens, 1019

portable device screens, 998

printers, 1138, 1146

video, 710

original equipment manufacturer (OEM) coolers for CPUs, 107–108

OS Optimized Defaults option, 181

oscillators for clock speed, 75–76

OSD (onscreen display) menus, 698–699

OSs. See operating systems (OSs)

OUs (organizational units), 814, 1183

outcomes, documenting, 24–25

OuterVision Power Supply Calculator, 259

outlets

testing, 240–241

work areas, 764–765

output in computing process, 35

over-current protection (OCP) for rails, 253

overclocking CPUs, 76, 112–113

overheating

CPUs, 114–115

laser printers, 1154

mobile devices, 1063–1064

portable devices, 981–982, 997

troubleshooting, 679–680

overlapping channels in 2.4-GHz band, 839

overloaded networks with mobile devices, 1071–1072

overprinting in laser printers, 1157

Owner permissions for folder sharing, 802

ownership

authentication, 1082

cloud, 951–952

files, 521

Linux permissions, 527–528

ozone filters in laser printers, 1112, 1154

P

P1 power connectors, 247

P4 power connectors, 251

PaaS (Platform as a Service), 949–950

package indexes, 634

package managers, 633–635

packages in Linux, 567–569

PacketFence software, 1197

page faults, 148

page files, 138–142

Page Setup interface, 1144–1145

pagers for CLI commands, 606

pages in solid-state drives, 306–307

pages per minute (ppm) speed for inkjet printers, 1106–1107

pairing process for Bluetooth, 856–857, 1047, 1092

palmprint readers, 1179–1180

panel technology

IPS, 729, 966, 1009

LCD, 688–691

OLED, 691, 966, 1009–1010

panes in System Preferences, 494–495

PANs (personal area networks), 846–847

paper

impact printers, 1103, 1148–1149

settings, 1138

thermal printers, 1107, 1149

troubleshooting, 1143–1144

paper dander, 1153

paper jams in laser printers, 1156

parallel ATA (PATA), 282–283

parallel CPU execution, 92

parity, RAID, 290–292

parity spaces, 354

partition boot sectors, 309

partition tables, 309

PartitionMagic tool, 316

partitions

creating, with Disk Management, 338–341

creating, with installation media, 332–334

creating, tools for, 315–316

diskpart, 661–662

errors, 361

exFAT, 330

extended, 311–312

formatting, 351–352

GUID partition tables, 313–314

hard drives, 305–308

mounting as folders, 348–350

names, 316–317

primary, 309–311

recovering, 430, 663

types, 314–315

Windows installation, 441–442

parts retrievers, 16

passcodes for mobile devices, 1079–1080

password managers, 892–893

Password Policy subcontainer, 538

passwords

administrator, 167, 510, 543

attacks, 1164

authentication, 517–519

BIOS/UEFI, 167

domains, 813

expiration, 538–539

Keychain, 501

password managers, 892–893

proper, 1177

routers, 881

single sign-on, 423

user, 167

WEP, 852

Windows installation, 443

workgroups, 421–422, 800–801

PATA (parallel ATA), 282–283

patch cables

description, 760

making, 760–762

troubleshooting, 820

patch panels in telecommunications rooms, 757–760

patches

macOS and Linux, 553–554

and malware, 1191

Windows, 552–553

Windows installation, 449

pathping command, 787

paths

files, 604, 611

networks, 823

pattern locks, fingerprint, 1080

patterns, address bus, 82

Payment Card Industry Data Security Standard (PCI DSS), 1237

payments

mobile device services, 1022–1023

procurement, 1222

PC-based lockups, 1189

PCBs (printed circuit boards) in motherboards, 192

PCHs (Platform Controller Hubs), 154–156

PCI (Peripheral Component Interconnect) bus architecture, 205–206

PCI DSS (Payment Card Industry Data Security Standard), 1237

PCI Express (PCIe) interface

bus architecture, 206–208

display adapters, 701

power supply connectors, 254

Thunderbolt cards, 379–380

PCL (Printer Command Language), 1116

PCM (pulse code modulation) for sound, 399

PCMCIA (Personal Computer Memory Card International Association) standards for portable devices, 972

PDAs (personal digital assistants), 1006

Pegasus software, 1089

pen tablets, 393–395

pens for portable devices, 964–965

Pentium CPUs, 86

performance

CPUs, 115

Internet, 919–922

mobile applications, 1090

mobile device displays, 1061

options, 572–575

portable devices, 995–996

printers, 1139–1140

RAID, 366

sluggish, 667–668, 679

wireless networks, 860

performance cores in CPUs, 116

Performance Monitor

Data Collector Sets, 488–489

objects and counters, 487–488

overview, 486–487

tools, 487–488

Performance Options dialog box, 572–575

Performance tab in Task Manager, 477–478

performance variables for solid-state drives, 279–280

periodic maintenance for laser printers, 1153–1154

Peripheral Component Interconnect (PCI) bus architecture, 205–206

peripherals

barcode scanners and QR scanners, 388–389

common, 381–382

digitizers, 393–395

game controllers and joysticks, 391–393

keyboards, 382–385

KVM switches, 390–391

multimedia devices and formats. See multimedia devices and formats

pointing devices, 385

ports. See ports

power to, 248–249

review questions, 415–417

touch screens, 389–390

permissions

folder sharing, 802–804

Linux and macOS, 527–529

network shared resources, 797–798

NTFS. See NTFS permissions

security, 1181–1182

USB, 173–174, 378

Permissions dialog box

NTFS permissions, 521–522

resource sharing, 530–531

persistence, image, 719

personal area networks (PANs), 846–847

Personal Computer Memory Card International Association (PCMCIA) standards for portable devices, 972

personal data backups, 580–585

personal digital assistants (PDAs), 1006

personal documents, 55

personal government-issued information, 1237

personal identification numbers (PINs)

authentication, 520

Bluetooth, 1047

personal safety, 17–18

personal use licenses, 1238

Personalization section for Windows setting, 465

Personalization Settings for video, 711–713

personally identifiable information (PII), 1237–1238

PFC (power factor correction), 256

PGA (pin grid array) packages for CPUs, 105–106

PGP (Pretty Good Privacy), 1074

PHI (protected health information), 1238

Phillips-head screwdrivers, 16

phishing attacks, 1167

phones

iPhones. See iPhones

smartphones. See smartphones

VoIP, 903–904

photoconductive properties of laser printers, 1107–1108

physical cables, troubleshooting, 817–821

physical damage to mobile devices

displays, 1062

protection from, 1076–1078

physical security

facilities, 1172–1174

lock down systems, 1174–1175

physical theft, 1169

physical tools, 16–17

physically damaged ports, charging issues from, 1068–1069

pickup rollers in laser printers, 1111

Pictures folder, 55

PIDs (process identifiers), 477

PII (personally identifiable information), 1237–1238

PIN codes for mobile devices, 1079–1080

pin grid array (PGA) packages for CPUs, 105–106

pinching mobile devices, 1019

ping command

latency checks, 923

no connectivity issues, 917–918

working with, 785

pinned applications, 43

PINs (personal identification numbers)

authentication, 520

Bluetooth, 1047

pipe operator (|) in CLI commands, 608

pipelining CPUs, 92–94

pixels

LCD panels, 688–689

monitor issues, 718–719

monitor resolution, 724

scanners, 1120

pixels per inch (PPI) metric for monitors, 726

plaintext files, 618–619

Plane to Line Switching (PLS), 690

plans, change management, 1232

plans of action in problem resolution, 23

plastic filaments in 3-D printers, 1112–1114

platen issues in impact printers, 1149

Platform as a Service (PaaS), 949–950

Platform Controller Hubs (PCHs), 154–156

platters in hard drives, 274

plenum cabling, 747–748

PLS (Plane to Line Switching), 690

plug-ins for Web browsers, 891–892

PMICs (power management integrated circuits), 133

point of sale (POS) machines, 1103

point-to-point wireless network connections, 846

pointing devices

overview, 385

portable devices, 963–964

policies

AUPs, 1224

common, 1184–1185

group, 424–425, 626–627, 1182–1184

MDM, 1075

organizational, 1224

security, 537–539

polymorphic viruses, 1194

polyvinyl chloride (PVC) cabling, 747–748

Pooled NAT, 880

pools for IP addresses, 783

poorly formed characters with laser printers, 1157

pop-ups

blockers, 895–897

random, 1190

POP3 (Post Office Protocol version 3)

e-mail, 900

functions and ports, 888

mobile devices, 1039–1041

port flapping, 818

portable battery rechargers, 1065

portable devices. See also mobile devices

audio, 999

batteries, 975

cleaning, 981

component replacement, 991–995

disassembling, 985–988

display ports, 968–970

display problems, 998–999

display types, 965–966

expansion slots, 972–974

extending, 967–969

heat issues, 981–982, 997

input devices, 962–965

input problems, 999–1001

introduction, 959–964

laptops, 961–962

managing, 974–975

memory installation, 147–148

vs. mobile, 960–961

networking options, 969–972

power management, 977–981

protecting, 982–983

RAM, 989–990

review questions, 1001–1003

single-function ports, 967–969

storage upgrades, 989–990

taxonomy, 960–962

troubleshooting, 995–1001

types, 961–962

upgrading, 988–991

wireless devices, 998–999

Portrait video mode, 710

ports

charging issues, 1068–1069

e-mail, 1040–1041

Ethernet, 744

expansion options, 1026–1027

forwarding, 1202

issues, 380–381

mobile devices, 1045–1051

overview, 38–40

portable devices, 967–969, 972–974

replicators, 973–974

security, 1205

serial, 369–370

Thunderbolt, 379–380

triggering, 1202–1203

USB, 370–379

POS (point of sale) machines, 1103

positive attitudes in effective communication, 7

possession factor in authentication, 1082

POST. See Power-On Self-Test (POST)

post-installation tasks, 449–453

Post Office Protocol version 3 (POP3)

e-mail, 900

functions and ports, 888

mobile devices, 1039–1041

PostScript page description language, 1116

power and power management

DRAM, 133

missing, 678

portable devices, 976–981, 995–996

SATA drives, 297

soft power, 251

USB devices, 378–379

video cards, 706

Wake-on-LAN, 794

power banks for mobile devices, 1051

power conditioning, 244

power factor correction (PFC), 256

power good wire, 180

power management integrated circuits (PMICs), 133

Power Management tab

USB devices, 378–379

Wake-on-LAN, 794

Power-On Self-Test (POST), 178

beep codes, 178–179, 677

boot process, 180–181

POST cards, 179

text errors, 179

Power Options app, 977–979

Power over Ethernet (PoE), 831–832

power packs for mobile devices, 1065

power plans for portable devices, 977

power-saving modes for mobile devices, 1066

power savings from virtualization, 931–932

power supplies

AC supply. See alternating current (AC)

active PFC, 256

ATX motherboards, 250–251

ATX12V 1.3, 251–252

ATX12V 2.0, 253–254

cooling, 261–265

description, 247

direct current, 236

electricity basics, 234–236

EPS12V, 252

fire safety, 268

fuses, 268

installing, 259–261

introduction, 233–234

laser printers, 1111

modular, 268–269

motherboards, 193, 247–248, 266–267

needs calculations, 259

niche-market, 255

peripherals, 248–249

portable devices, 983

rails, 252–253

redundant, 268–269

review questions, 270–272

SATA drives, 249–250

testing, 249

troubleshooting, 265–269

wattage requirements, 257–259

Power Supply Calculator, 259

power supply units (PSUs), 233–234

power surges, 242–246

Power Users group, 510, 541–542

powered USB hubs, 377

PowerShell

accessing, 51

CLI, 597

description, 639

help for, 606

PPI (pixels per inch) metric for monitors, 726

ppm (pages per minute) speed for inkjet printers, 1106–1107

Preboot Execution Environment (PXE)

description, 180

Windows installation, 445–446

Precision Touchpad, 385

Preferred Roaming Lists (PRLs) for firmware updates, 1035

prefix lengths in IPv6 addresses, 776–777

preparation for safety, 11

Pretty Good Privacy (PGP), 1074

Prevent Access to the Command Prompt policy, 1184

Prevent Registry Edits policy, 1184

preventive measures in troubleshooting, 23–24

PRI (product release instruction) for firmware updates, 1035

primary corona wires in laser printers, 1110

primary partitions, 309–311

principle of least privilege, 1181

print beds in 3-D printers, 1112

Print Management console, 1137

print servers, 737–738

print to PDF option, 1115

printed circuit boards (PCBs) in motherboards, 192

Printer Browsing policy, 1184

Printer Command Language (PCL), 1116

Printer Properties dialog box, 1142

Printers & Scanners preferences pane, 496–497

printers and multifunction devices

3-D, 1112–1114

configuring, 1137–1139

connectivity, 1123–1124

copy and fax components, 1122

impact, 1103–1104

inkjet, 1103–1107

installing, 1124, 1130

introduction, 1101–1102

languages, 1115–1117

laser, 1107–1112, 1124–1129

layout settings, 1138

macOS, 496–497

managing, 1140–1141

paper settings, 1138

performance, 1139–1140

quality settings, 1138–1139

review questions, 1158–1160

scanners, 1117–1122

setting up, 1130–1137

sharing, 816–817

thermal, 1107

troubleshooting, 3-D printers, 1157–1158

troubleshooting, general issues, 1141–1148

troubleshooting, impact printers, 1148–1149

troubleshooting, inkjet printers, 1150–1152

troubleshooting, laser printers, 1152–1157

troubleshooting, thermal printers, 1149–1150

virtual, 1115

printheads

impact printers, 1103

inkjet printers, 1103, 1150

privacy

geotracking, 1013–1014

Internet Options settings, 899

macOS settings, 498

multiple monitors, 721

privacy filters, 1175

settings, 444, 466

Web browsers, 896

Privacy preferences pane, 498–499

Privacy tab in Internet Options, 899

private-browsing mode in Web browsers, 896

private clouds, 952

private IP addresses, 773

private networks, 1206–1207

privileges

administrator, 510

CLI access, 601–602

elevated, 511

least privilege principle, 1181

PRLs (Preferred Roaming Lists) for firmware updates, 1035

probable cause in troubleshooting, 21–22

problem identification in troubleshooting, 20–21

process identifiers (PIDs), 477

process nodes in CPUs, 116

processes, listing, 629–632

Processes tab in Task Manager, 476–477

processing stage in computer process, 35–37

processing step in laser printers, 1125–1126

processor numbers for CPUs, 103–104

processors. See central processing units (CPUs)

procurement life cycle, 1222

product keys in Windows installation, 437–439

product release instruction (PRI) for firmware updates, 1035

professionalism, 1

appearance and attire, 2–3

effective communication, 6–11

review, 26–28

traits, 3–6

troubleshooting methodology, 19–25

profiles

color, 1139–1140

load speed issues, 675

mobile devices, 1076

networks, 1034

rebuilding, 663–665

programs

autostarting, 478–479

deleting, 359

disabling, 667–668

essential files folder, 54–55

Programs and Features applet

installed updates, 553

software removal, 569–572

virtual machines, 939

Programs tab in Internet Options, 899

projectors, 691–692

image technologies, 692

light sources, 693–694

lumens, 692–693

throw, 693

troubleshooting, 722

prompts, CLI, 596–598, 602–603

propagation of NTFS permissions, 525–526

Properties dialog box for printers, 1143–1144

Properties settings for NTFS permissions, 521–522

proprietary crash screens

catastrophic failures, 115

description, 677

NMIs, 148

RAID, 365

proprietary development models, 1015

proprietary motherboards, 198

proprietary vendor-specific ports and connectors, 1046

protected health information (PHI), 1238

protecting AC power, 242–246

protective covers for mobile device screens, 1051

protective MBRs, 314

provisioning virtual machines, 934

proxy servers, 898–899

pruning folder trees, 622–624

ps command, 631–632

.ps1 files, 639

PSTN (Public Switched Telephone Network), 1022

PSUs (power supply units), 233–234

public clouds, 952

public IP addresses

description, 773

Internet, 880

public networks, 1206–1207

Public Switched Telephone Network (PSTN), 1022

pulse code modulation (PCM) for sound, 399

punchdown blocks, 758

punchdown tools, 758

purchase orders in procurement, 1222

purpose in change management, 1230–1231

PVC (polyvinyl chloride) cabling, 747–748

pwd utility, 605

PXE (Preboot Execution Environment)

description, 180

Windows installation, 445–446

.py files, 639

Python language scripts, 639

Q

Qi standard, 1051

QoS (Quality of Service)

Internet speed issues, 921–922

NICs, 794–795

QR (Quick Response) codes, 388–389

quad-channel memory architecture, 131

quad-pumped frontside buses in CPUs, 97

quality

printer settings, 1138–1139

sound, 398–399

VoIP calls, 923–924

Quality of Service (QoS)

Internet speed issues, 921–922

NICs, 794–795

quality patch management updates, 552

quarantining malware, 1197

quartz oscillators for clock speed, 75–76

question marks (?) for file wildcards, 619–620

questions in fact-seeking, 8

Quick Link menu, 46

Quick Response (QR) codes, 388–389

quotas in NTFS, 328

QWORD values in Registry, 461

R

radio firmware in mobile devices, 1035–1037

radio frequency identification (RFID)

assets, 1221

authentication, 1180

facility security, 1174

radio frequency interference (RFI), 15–16

radio frequency (RF) technologies, 838

radio power in WAP placement, 836

RADIUS (Remote Authentication Dial-In User Service), 853–854

RAID. See redundant array of independent disks (RAID)

rails in power supplies, 252–253

rainbow tables, 1164

Rambus DRAM (RDRAM), 129

random-access memory (RAM). See also memory

capacity, 142–144

dynamic. See dynamic random-access memory (DRAM)

introduction, 121–122

matching, 144

overview, 78–80

raster image processors, 1125–1126

recommendations, 142

review questions, 150–152

software requirements, 561

speed, 144–145

troubleshooting, 148–150

random pop-ups, 1190

random read/write performance in solid-state drives, 280

random reboots and freezes in mobile devices, 1069–1070

range

IEEE 802.11 versions, 842

wireless network coverage, 844

ransomware, 1187–1188

rapid elasticity, cloud for, 954

RAs (router advertisements) in IP addresses, 777

raster image processors (RIPs) in laser printers, 1125–1126

raster images in laser printers, 1125–1126

RCA connectors for sound, 401

rd command, 614–615

RDP (Remote Desktop Protocol), 905

application protocols, 886

functions and ports, 888

Windows 10 Pro, 424, 426

RDRAM (Rambus DRAM), 129

Read & Execute permission, 522–523

read-only memory (ROM) chips

firmware, 160–161

flashing, 185–186

laser printers, 1112

RAID configuration, 295

Read permissions

folder sharing, 802–803

folders, 522–523

Linux, 528

Read/Write permissions, 802

reading plaintext files, 618–619

rear out jacks, 400

reboots

mobile devices, 1069–1070

from overclocking, 112

for troubleshooting, 652

rebuilding profiles, 663–665

receivers, DSL, 872–873

recognizing malware, 1197

recordable (BD-R) format, 414

recordable DVD, 412

recorded sound formats, 399

records, procurement, 1222

recovering deleted files, 323

recovery partitions, 430, 663

recovery procedures in troubleshooting

profile rebuilding, 663–665

WinRE, 654–663

recovery tips for malware, 1196

Recycle Bin

deleting files in, 359

FAT 32 file system, 323–324

recycling

batteries, 975

devices, 450–452

e-waste, 1236

Red Hat Package Manager (RPM), 634–635

redirection

browser, 1190

folder, 814

redundant array of independent disks (RAID)

dedicated boxes, 295

dynamic disks, extending and spanning, 345–346

dynamic disks, volumes on, 313

dynamic disks, working with, 348

implementing, 293

levels, 291–292

motherboard support, 203

SCSI, 288–291

software vs. hardware, 293–295

troubleshooting, 365–366

Windows installation, 435

redundant power supplies (RPSs), 268–269

refresh rate in monitors, 727

reg command for Registry, 462

region settings, 465

Regional Internet Registries (RIRs) for IPv6 addresses, 777

regional settings, 435

registered jack (RJ) designation, 746–748

registered memory, 136–137

registers

CPUs, 71–73

keyboard, 158

registration

inkjet printer color, 1150

laser printer color, 1154

Registry

accessing, 458

command-line tools, 462

components, 458–459

editing, 460–462

introduction, 457–458

profiles, 663–665

Registry Editor, 458

regsvr32 command, 462

regulated data, 1237–1238

regulations

compliance requirements, 1226

hazardous materials, 1235–1236

reimaging computers, 660

reinstalling applications, 653–654, 1059

relative file paths, 604, 611

Reliability Monitor, 673

remapping network drives, 641

remote access

desktop management software, 912

file transfer software, 911–912

Remote Desktop, 904–908

remote monitoring and management, 912

SSH, 904

Telnet, 904

video-conferencing software, 908

VPNs, 908–911

Remote Assistance, 906–907

Remote Authentication Dial-In User Service (RADIUS), 853–854

remote backup mobile applications, 1081, 1090

Remote Desktop, 904–908

Remote Desktop Connection, 424, 426, 905–906

Remote Desktop Protocol (RDP), 905

application protocols, 886

functions and ports, 888

Windows 10 Pro, 424, 426

remote hosts for networks, 735–736

remote monitoring and management (RMM), 912

remote network installations, 432

remote printing, 1115

remote wipes for mobile devices, 1081

removable antennas, 845

removable storage devices, 404

digital cameras, 395–396

flash memory, 404–407

optical, 408–415

Remove everything option, 662

removing

ATX power supplies, 260–261

computers from domains, 811

device drivers, 214

directories, 614–615

software, 569–572

repair installations, 431

Repair your computer option, 436

repairing portable devices, 985

repeaters

Ethernet, 745

wireless networks, 833–834

replace and pray RAM troubleshooting method, 149

replacing printer cartridges, 1150

replication of viruses, 1185–1186

replicators, port, 973–974

reports, incident, 1240

request forms in change management, 1230

Request to Send/Clear to Send (RTS/CTS) protocol, 832–833

research in troubleshooting, 22

reservations in DHCP, 783

Reset Password dialog box, 813

Reset this PC option, 662–663

resetting devices

mobile, 1058–1059

for troubleshooting, 652–653

resiliency mechanism in Storage Spaces, 353

resin in 3-D printers, 1112

resistance, electrical, 235

resistors in ESD straps, 13

resolution

monitors, 720, 724–725

printers, 1138

printers, inkjet, 1106–1107

printers, laser, 1126

scanners, 1120

video, 709

resolution enhancement technology (RET), 1126

Resource Monitor, 482–484

resource warnings, USB controller, 672–673

resources

cloud, 953

connection issues, 822

mobile application issues, 1090–1091

network, 738

requirements, 654

sharing. See sharing resources

virtual machine requirements, 935–936

virtualization savings, 930–932

respectful communication, 7–8

response issues

mobile applications, 1090

mobile device touchscreens, 1060

mobile devices, 1064–1065

response rate in monitors, 727

responsibility, 5–6

responsible staff members (RSMs) in change management, 1229–1230

restarting machines, scripts for, 640

restarting services for troubleshooting, 652

restore points, 587, 658–659

restores

system, 587–590

user data files in Windows installation, 449

RET (resolution enhancement technology), 1126

retina scanners, 1180

retiring systems in Windows installation, 450–452

reverse printer setting, 1138

revolutions per minute (RPMs) in hard drives, 275–276

rewritable (BD-RE) format, 414

RF (radio frequency) technologies, 838

RFI (radio frequency interference), 15–16

RFID (radio frequency identification)

assets, 1221

authentication, 1180

facility security, 1174

RG-6 cable, 750

RG-6QS cable, 750

RG-59 cable, 750

ribbons in impact printers, 1103

RIM BlackBerry PDA, 1006–1007

ripcords in patch cables, 762

RIPs (raster image processors) in laser printers, 1125–1126

RIRs (Regional Internet Registries) for IPv6 addresses, 777

risk level in change management, 1232

RJ (registered jack) designation, 746–748

RJ11 connectors, 747

RJ45 connectors

Ethernet, 746–748

locks, 1174

patch cables, 760–761

portable devices, 972

work areas, 764

rm command, 621–622

rmdir command, 614–615

RMM (remote monitoring and management), 912

roaming mobile devices, 1035, 1038

robocopy command, 623

rogue anti-malware programs, 1190

roles in network hosts, 735–738

rollback plans in change management, 1229

rollbacks

device drivers, 215–216

updates, 661

rollers

inkjet printers, 1103

laser printers, 1110–1111, 1153

ROM. See read-only memory (ROM) chips

root access issues for mobile applications, 1093–1094

root directories

CLI, 604

Windows, 52

root hubs for USB, 370

root privileges, 601–602

rootkits, 1186

rotation backup schemes, 579

router advertisements (RAs) in IP addresses, 777

router solicitation (RS) messages in IP addresses, 777

routers

configuring, 881–885

description, 880

firewalls, 1200

firmware, 884–885

Internet, 868

WANs, 765, 770

routing

LANs, 771

WANs, 765

RPM (Red Hat Package Manager), 634–635

RPMs (revolutions per minute) in hard drives, 275–276

RPSs (redundant power supplies), 268–269

RS (router solicitation) messages in IP addresses, 777

RS232 connectors, 370

RSA tokens in authentication, 1178

RSMs (responsible staff members) in change management, 1229–1230

RTS/CTS (Request to Send/Clear to Send) protocol, 832–833

RU measurements for equipment racks, 757

rules for firewalls, 1208–1210

Run as administrator option

command line, 600

context menu option, 511

running programs

closing, 1057–1058

macOS and Linux, 616–617

Windows, 615–616

runs, cable, 754

S

S.M.A.R.T. (Self-Monitoring, Analysis, and Reporting Technology) program, 283

S/MIME (Secure/Multipurpose Internet Mail Extensions)

e-mail, 1074

mobile devices, 1041

S/PDIF (Sony/Philips Digital Interface) connectors, 400

S-video connectors, 704

SaaS (Software as a Service), 951

Safe mode

boots, 463

driver issues, 723–724

profile rebuilding, 663–664

safety

antistatic tools, 12–15

EMI, 15

ESD, 11–12

personal, 17–18

physical tools, 16–17

preparation, 11

review, 26–28

RFID, 15–16

safety goggles, 19

sags in AC supply, 242–246

sampling digital sound, 397–398

Samsung Pay system, 1022

sandboxes

change management, 1229

virtual machines, 933–934

sanitizing hard drives, 451

SANs (storage area networks), 798

SAS (Serial Attached SCSI) hard drives, 288

SATA Express (SATAe), 285

SATA (serial ATA) drives

connections, 297–298

overview, 283–285

power to, 249–250

SATAe (SATA Express), 285

satellite Internet connections, 879

SC (subscriber connectors), 749

SCADA (supervisory control and data acquisition) systems, 915

scaling printer setting, 1138

scan codes, keyboard, 158

scanners

authentication, 1179–1180

barcode and QR, 388–389

mobile applications, 1088–1089

network services, 1121

operation, 1117–1119

portable devices, 969

selecting, 1119–1121

tips, 1121–1122

scheduling maintenance, 554–556

scope

change management, 1231

IP addresses, 783

screen locks for mobile devices, 1079–1080

screen orientation in mobile devices, 1019

Screen Sharing app, 905

screen technologies in mobile devices, 1009–1010

screened subnets, 1203–1205

screens. See displays; monitors

screensaver locks, 1175

screwdrivers, 16

scripting

comments, 645–646

considerations, 642–643

data types, 643–644

environment variables, 646–647

loops, 644–645

overview, 638–639

rules, 643

types and languages, 639–640

use cases, 640–642

variables, 644

SCSI (small computer system interface), 288–291

SD (Secure Digital) cards

digital cameras, 395–396

forms of, 405–406

SDHC (Secure Digital High Capacity) cards, 406

SDKs (software development kits), 1021–1022

SDN (software-defined networking), 796

SDR (standard dynamic range), 729–730

SDRAM (synchronous DRAM), 127–129

SDSL (symmetric DSL), 873

SDXC (Secure Digital Extended Capacity) cards, 406

sealed systems, 142

searches

find and grep commands, 632–633

MAC addresses, 742

sectors in hard drives, 306

Secure Boot feature, 172–173, 176–177

secure connections and sites with Web browsers, 893–894

Secure Digital Extended Capacity (SDXC) cards, 406

Secure Digital High Capacity (SDHC) cards, 406

Secure Digital (SD) cards

digital cameras, 395–396

forms of, 405–406

Secure FTP (SFTP)

application protocols, 886

functions and ports, 888

working with, 914

Secure/Multipurpose Internet Mail Extensions (S/MIME)

e-mail, 1074

mobile devices, 1041

Secure Shell (SSH)

functions and ports, 888

virtual private networks, 909

working with, 904

Secure Sockets Layer (SSL), 1212

Secure Sockets Layer (SSL)/Transport Layer Security (TLS), 1024–1025

security

concepts, 1171–1172

CPUs, 100–101

introduction, 1161

logical, 1176–1185

mobile devices, 1074–1086

network. See network security

network printers, 1140–1141

NTFS, 327

physical, 1172–1175

policies, 537–539

portable devices, 984–985

threats, 1162–1170

virtualization, 932

vulnerabilities, 1170–1171

wireless networks, 835–838

Security events in Windows Logs, 490

security groups in Active Directory, 811

security guards

access control vestibules, 1166

tools for, 1173

Security tab

Internet Options, 899

NTFS permissions, 521–524, 798

printer access, 1142

resource sharing, 530

system setup utility, 172–173

segments

Ethernet, 745

LANs, 796

Select Users or Groups dialog box for folder sharing, 803

Self-Monitoring, Analysis, and Reporting Technology (S.M.A.R.T.) program, 283

Sender Policy Framework (SPF) records, 781

senses in troubleshooting, 22

sensitive information, protecting, 1175

sensitivity trait, 6

sensors in laser printers, 1112

separation pads in laser printers, 1111

sequential read/write performance in solid-state drives, 279–280

serial ATA (SATA) drives

connections, 297–298

overview, 283–285

power to, 249–250

Serial Attached SCSI (SAS) hard drives, 288

serial interfaces, 1049

serial ports, 369–370

serial presence detect (SPD), 145–146

Server Message Block (SMB) protocol

file and print sharing, 797

functions and ports, 888

scan services, 1121

server-side virtualization, 929, 945

Server System Infrastructure (SSI), 252

servers

authentication, 815

DHCP, 783

DNS, 779–780

file, 815–816

locks, 1174

print, 1123–1124

rack-mounted, 757

Web, 736–738, 889

Web browsers, 898–899

service layers in cloud, 947–951

service menu for mobile device displays, 1061–1062

service modes in laptops, 148

service packs in Windows installation, 449

service set identifiers (SSIDs)

configuration issues, 862

configuring, 848–850

profiles, 1034

wireless networks, 835–837

services

backup, 591

restarting, 652

starting issues, 671

UEFI, 162

Services console for printers, 1143

Services tab

System Configuration, 464

Task Manager, 481–483

session hijacking, 1164

Session Initiation Protocol (SIP)

functions and ports, 888

VoIP, 903

Set time automatically option, 465

Set time zone automatically option, 465

Settings app

cellular data networks, 1035

external monitors, 969

Microsoft Management Console, 57

mobile devices, 1034

Setup events in Windows Logs, 490

sfc (System File Checker) command, 627–628, 653

SFF (Small Form Factor) committee, 281

SFTP (Secure FTP)

application protocols, 886

functions and ports, 888

working with, 914

SFX12V power supplies, 255

.sh files, 639

shared folders, locating, 533

shared resources

cloud, 953

LANs, 797–798

sharing resources

files, 530–532, 912–914

folders, 530–532, 801–804

printers, 816–817

secure, 529

Sharing Wizard, 531, 801–802

shell scripts, 638

shells, 597

shield icons, 543–544

shielded twisted pair (STP) cable, 746

shields in coaxial cable, 750

shipping portable devices, 984

shortcuts, keyboard, 628–629

shoulder surfing, 1167

Show Hidden Files option, 472–473

showing file extensions, 473

shredding hard drives, 451

shunts, 114

Shut Down System policy, 1184

shutdown command, 628, 638

shutdowns

CPUs, 115

frequent, 681

from overclocking, 112

projector, 722

troubleshooting, 668–669

side-by-side apps feature, 46

sideloading issues in mobile applications, 1093–1094

Sign-in option, 516–517

signal strength for mobile devices, 1071–1072

signature pads, 395

signatures

antivirus programs, 1079, 1088, 1192, 1194, 1196

code, 890–891

drivers, 214

secure boots, 176–177

signing in with Web browsers, 896

SIMMs (single inline memory modules), 126

Simple Mail Transfer Protocol (SMTP)

e-mail, 900

functions and ports, 888

mobile devices, 1040–1041

Simple Network Management Protocol (SNMP)

functions and ports, 888

remote monitoring, 912

simple storage spaces, 353

simple volumes

creating, 342–343

dynamic disks, 312–313

Singer, June, 457

single-core CPUs, 99

single-factor authentication, 1082

single-function ports for portable devices, 967–969

single inline memory modules (SIMMs), 126

single-layer (SL) DVD formats, 412

single-level cell (SLC) technology for solid-state drives, 279

single-link DVI, 695

single-mode fiber optic cabling, 749

single-rail power supply systems, 253

single-sided RAM, 134

single-sided (SS) DVD formats, 412

single sign-on (SSO)

authentication, 520

domains, 423, 807

mobile devices, 1043

SIP (Session Initiation Protocol)

functions and ports, 888

VoIP, 903

Siri virtual assistant, 1020–1021

size

FAT 32 clusters, 322

monitors, 720

NTFS clusters, 329

printer issues, 1144–1145

printer paper, 1138

virtual machine drives, 941–942

SL (single-layer) DVD formats, 412

slashes (/) in CLI, 603–605

SLC (single-level cell) technology for solid-state drives, 279

sleep mode

issues, 670

portable devices, 976

slot covers, airflow affected by, 264

slots for expansion buses, 204

slow speed issues

Internet, 919–922

profiles load, 675

sluggish performance

CPUs, 115

mobile application response time, 1090

symptoms, 679

troubleshooting, 667–668

small computer system interface (SCSI), 288–291

Small Form Factor (SFF) committee, 281

small-outline DIMM (SO-DIMM) form factors

installing, 147–148

overview, 128

Smart Cache in CPUs, 96

smart card readers, 969

smart cards

authentication, 1177

facility security, 1174

RFID, 1180

smart devices, 914

smartphones

battery usage, 1066

biometric authentication, 387–388

cameras, 1010

elements, 1006–1008

facial recognition, 1180–1181

microphones, 1011

OS tech utility launch points, 63

resolution, 725

wireless technology, 830–831

SMB (Server Message Block) protocol

file and print sharing, 797

functions and ports, 888

scan services, 1121

smells, burning, 680–681

SMTP (Simple Mail Transfer Protocol)

e-mail, 900

functions and ports, 888

mobile devices, 1040–1041

smudged printouts from laser printers, 1155

snap-ins, MMC, 484–486

snapshots

backups, 576

system restores, 587

Time Machine, 585–586

virtualization, 932–933

SNMP (Simple Network Management Protocol)

functions and ports, 888

remote monitoring, 912

SO-DIMM (small-outline DIMM) form factors

installing, 147–148

overview, 128

SoC (system on a chip)

CPUs, 85

mobile devices, 1025

social engineering attacks, 1166–1167

sockets for CPUs, 102–107

soft power in ATX motherboards, 251

soft power-off mode in portable devices, 976

soft resets in mobile devices, 1058

software, 41

authentication, 1176

autostarting, 556–559

distribution methods, 562–563

file structures and paths, 52–56

installing, 559–569

OS functions, 41–42

removing, 569–572

requirements, 559–562

tech utility launch points, 56–63

trusted vs. untrusted sources, 1083–1084

user interfaces, 42–52

video, 706–715

Windows installation, 450

wireless networks, 832–833, 860

Software as a Service (SaaS), 951

software-defined networking (SDN), 796

software development kits (SDKs), 1021–1022

software firewalls, 1204–1210

software RAID, 293–295

Software Update pane, 553–554

solid core UTP, 755

solid-state drives (SSDs)

connecting, 298–299

costs, 279

form factors, 277–279

fragmentation, 325

laptop upgrades, 990–991

mobile devices, 1025

NVMe specification, 287–288

overview, 276–278

pages, 306–307

performance variables, 279–280

Sony/Philips Digital Interface (S/PDIF) connectors, 400

SOPs (standard operating procedures), 1223–1224

sound

analog and digital components, 397–398

hard drive noises, 364

motherboard support for, 203

portable devices, 967–968, 999

settings, 466

troubleshooting, 718

video formats, 402

Sound applet, 469–470

sound cards, 397

source setting for printer paper, 1138

southbridge chipsets, 154–155, 199

Spaces in macOS, 48

spam

botnets, 1189

description, 1170

TXT records, 781

spam management records, 901

spanned volumes

creating, 344–346

dynamic disks, 313

SPD (serial presence detect), 145–146

speakers

Bluetooth, 1047

mobile devices, 1050, 1070–1071

replacing, 992

support for, 399–400

spear phishing attacks, 1167

Special Publication 800-63B, 518

speckling on laser printer pages, 1155

Speech settings, 465

speed

CD-ROM, 409

clock, 75

coaxial cables, 751

CPUs, 560

disk striping, 290

expansion buses, 204–205

fiber optic cable, 749

hard drives, 275–276

IMT-2020, 877

inkjet printers, 1106

Internet issues, 919–922

LTE, 877

NIC settings, 791–792

overclocking, 112–113

RAM, 144–145

scanners, 1121

SD card classes, 406–407

USB, 371–373

wireless networks, 860

SPF (Sender Policy Framework) records, 781

SPI (Stateful Packet Inspection) firewalls, 1201–1202

spikes in AC supply, 242–246

spindle speed in hard drives, 275–276

spinning pinwheel of death (SPoD) from NMIs, 148

splash screens, 1226

splitters for SATA drive power, 250

SPoD (spinning pinwheel of death) from NMIs, 148

spoofing

description, 1163

mobile applications, 1094

spoolers, print, 1125, 1130–1132, 1143–1144

spot color in laser printers, 1108

Spotlight tool, 501, 601

spotty print in laser printers, 1156

spudgers, 16

spyware, 1186–1187

SQL (Structured Query Language) injection, 1165

SRAM (static RAM), 95–96

SS (single-sided) DVD formats, 412

SSDs. See solid-state drives (SSDs)

SSE (Streaming SIMD Extensions) in CPUs, 91

SSH (Secure Shell)

functions and ports, 888

virtual private networks, 909

working with, 904

SSI (Server System Infrastructure), 252

SSIDs. See service set identifiers (SSIDs)

SSL (Secure Sockets Layer), 1212

SSL (Secure Sockets Layer)/Transport Layer Security (TLS), 1024–1025

SSO (single sign-on)

authentication, 520

domains, 423, 807

mobile devices, 1043

ST (straight tip) connectors, 749

stages in computers, 35–37

stalls, pipeline, 93

Standard Account group, 511

standard accounts

authentication, 508–511

elevated privileges, 511

standard dynamic range (SDR), 729–730

standard operating procedures (SOPs), 1223–1224

standard SD cards, 406

standby mode for portable devices, 976

standby UPSs, 245

standoffs in motherboards, 223–224

staple jams, 1146

star networks

cabling, 753

Ethernet bus, 743–744

Start button, 43–44

Start menu, 44–46

Startup Repair utility

missing operating systems, 675

repairs performed by, 660–661

Startup Settings option, 659

Startup tab

program disabling, 667–668

System Configuration, 464

Task Manager, 478–479, 556–557

Stateful Packet Inspection (SPI) firewalls, 1201–1202

static charge eliminators in laser printers, 1110

static electricity, 11–12

static IP addresses

configuring, 790

creating, 783

description, 776

routers, 884

static RAM (SRAM), 95–96

static wide-area network (WAN) IP, 884

status indicator lights for NICs, 791–793

status window for printer spoolers, 1143

stealth viruses, 1194

stereo sound, 398

Stingray device, 1091

storage

devices, 36

digital camera media, 395–396

images, 637

laptop upgrades, 989–990

mass. See drives; flash drives; hard drives; solid-state drives (SSDs)

portable devices, 982

software requirements, 561–562

virtual machines, 937

storage area networks (SANs), 798

storage card slots for portable devices, 972

Storage Sense feature, 360

Storage Spaces, 313, 352–355

STP (shielded twisted pair) cable, 746

straight tip (ST) connectors, 749

stranded core UTP, 755

Streaming SIMD Extensions (SSE) in CPUs, 91

streaming sound media, 399

string values

Registry, 461

scripts, 644

stringing 3-D printers, 1157

striped volumes in dynamic disks, 313, 346–347

striping, RAID, 203, 290–292

strong passwords, 517–518

structured cabling in Ethernet networks, 752–755

Structured Query Language (SQL) injection, 1165

stuck pixels, 718

sub-pixels in LCD panels, 688

subfolders in CLI, 604

subnet masks in IP addresses, 772–773

subnets, screened, 1203–1205

subscriber connectors (SC), 749

subwoofers, 399

sudo command, 602

Super I/O chips in motherboards, 199–200

super user privileges, 601–602

super-wide (160 MHz) channels, 840

SuperSpeed USB, 371–372

supervisors, 929–930

supervisory control and data acquisition (SCADA) systems, 915

suppliers, procurement, 1222

supply voltages in portable devices, 983

support systems information management, 1226

surge suppressors, 242–244

surround sound, 399

suspend mode in portable devices, 976

SVGA monitor resolution, 725

swap files, 138–142

swap partitions, 315

swelling capacitors, 682

swipe locks, fingerprint, 1080

switches

CLI commands, 605–606

Ethernet, 744–745

KVM, 390–391

LANs, 771, 795–797

laser printers, 1112

link lights, 792

PoE-capable, 831

portable devices, 971

structured cabling, 753

swollen batteries

mobile devices, 1069

portable devices, 996

symmetric DSL (SDSL), 873

Sync Center applet, 980

Sync your settings option, 713

synchronization

accounts, 1044–1045

automobiles, 1042

cloud files, 954–955

Exchange ActiveSync, 1042

issues, 1044

methods, 1043

mobile devices, 1041–1045

synchronous DRAM (SDRAM), 127–129

syntax of CLI commands, 605–606

synthetic backups, 577

Sysinternals tools, 479

syslog standard, 489

System applet

description, 469

remote access, 908

System Restore, 1197

viruses, 1197

workgroup names, 798–799

system boards in laser printers, 1112

System Configuration utility, 463–464

system crashes, 1169

system crystals for clock speed, 75–76

system date and time issues, 682–683

system disks, 180

System events in Windows Logs, 490

System File Checker (sfc) command, 627–628, 653

system files, scanning, 627–628

system image backups, 584

System Image Recovery tool, 659–660

System Image Repair, 661

System Information Utility (msinfo32.exe)

NICs, 741

version identification, 427

system instability, troubleshooting, 673–674

system lockups from overclocking, 112

system management for virtualization, 932

system on a chip (SoC)

CPUs, 85

mobile devices, 1025

system package managers, 634

System Preferences

autostarting software, 558–559

display settings, 713–714

keyboard settings, 383–384

launch points, 60

macOS, 60, 494–499

patch management, 553–554

pointing devices, 385

sound, 967

speakers, 401

workgroups, 800

System Properties dialog box

performance options, 572–573

system restores, 587–589

workgroup names, 798–799

System Protection tab, 590

System Recovery Options

malware remediation, 1198–1199

missing OS, 674

recovery settings, 654–663

system requirements, verifying, 654

System Restore tool

disabling, 1197

restore points, 658–659

system restores, 587–590

system ROM chips, 200

System Settings app in Linux, 61–62

System settings in Windows setting, 466

system setup utility

accessing, 164–166

Advanced Mode, 166

Ai Tweaker tab, 167–168

Advanced tab, 168–169

boot options, 173

Boot tab, 168, 170, 173–174

CMOS settings, 163–164

Configuration tab, 170, 172

fans, 175

Information tab, 169, 171

Main tab, 166–167

saving settings, 177

secure boots, 176–177

Security tab, 172–173

Tool tab, 168–169, 171

Trusted Platform Modules, 175–176

USB permissions, 173–174

system trays in Windows, 43

systemctl command for autostarting software, 558

systemd system, 556

T

T568A and T568B standards, 748

tablets

description, 1008–1009

facial recognition, 1180–1181

pen-tablets, 393–395

TACACS+ (Terminal Access Controller Access-Control System Plus), 853–854

tags, asset, 1221

tailgating, 1166

Take Ownership permission, 521, 523

tap pay devices, 1048

tapes for backups, 577

Task Manager

App history tab, 478–479

autostarting software, 556

Details tab, 480–481

multithreading, 98

overview, 475–476

Performance tab, 477–478

Processes tab, 476–477

program disabling, 667–668

Services tab, 481–483

Startup tab, 478–479

Users tab, 479–480

Task Scheduler, 555

taskbars in Windows, 43

TCP (Transmission Control Protocol), 783–784

TCP/IP. See Transmission Control Protocol/ Internet Protocol (TCP/IP)

TDP (thermal design power) in CPUs, 89

TDRs (time-domain reflectometers), 820

tearing effect in monitor sync, 730

tebi prefix, 83

tech traits, 3–6

tech utility launch points, 56

Linux, 61–62

macOS, 60–61

smartphone OSs, 63

Windows, 57–60

technical assistance, ticketing systems for, 1227–1228

technical manuals for motherboards, 221–222

technician issues in NTFS permissions, 526–527

techno-babble, 4

Technology Without an Interesting Name (TWAIN) drivers, 1118

Telecommunication Industry Association (TIA) UTP categories, 745

telecommunications rooms

description, 755

equipment racks, 756–757

patch panels and cables, 754, 757–763

telephone lines

Internet, 872

surge suppressors, 243

Telnet

application protocols, 886

functions and ports, 888

working with, 904

temperature issues, 1233–1235

temporal factor in authentication, 1082

Temporal Key Integrity Protocol (TKIP), 838

temporary files, deleting, 359–360

terabytes, 82

Terminal Access Controller Access-Control System Plus (TACACS+), 853–854

Terminal app

closing, 603

working with, 600–601

Terminal program, 598

Terminal CLI, 51–52

terminal emulators, 600

test development, virtual machines for, 934

test pages for printers, 1150

testing

AC supply, 237–238

AC voltage, 241

ATX power supplies, 266–267

backups, 578

cable, 763, 819–820

power supplies, 249

troubleshooting theories, 22–23

tethering

hotspots, 878

IEEE 802.11, 841

mobile devices, 1049–1050

text errors in POST, 179

text files

editors, 635–636

reading, 618–619

text (TXT) records, 781

TFTP (Trivial FTP), 914

TFTs (thin film transistors) in LCD monitors, 689

TFX12V power supplies, 255

theft

mobile devices, 1080–1081

physical, 1169

portable devices, 984–985

theories in troubleshooting, 21–23

thermal design power (TDP) in CPUs, 89

thermal paste for CPUs, 110

thermal printers

description, 1107

troubleshooting, 1149–1150

thermal throttling

CPUs, 89

mobile devices, 1064–1065

thermal wax transfer printers, 1107

thermometers, non-contact, 18

thin clients in virtualization, 932

thin film transistors (TFTs) in LCD monitors, 689

third parties

apps, 1084–1085

backup tools, 590–591

migration tools, 450

threads

CPUs, 94

processes, 475

threats

administrator access, 1168

data destruction, 1168

insider, 1168

malicious actors, 1162–1165

malware, 1170

social engineering, 1166–1167

spam, 1170

system crashes, 1169

theft, 1169

unauthorized access, 1165

throttling

CPUs, 88–89

mobile devices, 1064–1065

throughput

IEEE 802.11 versions, 842

solid-state drives, 279–280

throw, projector, 693

thumb drives

backing up, 637

description, 404

Thunderbolt

portable devices, 973

ports, 379–380

video display connectors, 696–697

TIA (Telecommunication Industry Association) UTP categories, 745

ticketing systems, 1227–1228

TightVNC, 905

tildes (~) for home directories, 605

timbre in sound, 398

time

drift, 675–676

settings, 435, 465

Time & Language settings, 464

time documentation in change management, 1231

time-domain reflectometers (TDRs), 820

Time Machine tool

backups, 585–586

macOS, 498–499

time zone settings, 465

timelines for expectations, 10–11

timeouts, screen, 1175

TKIP (Temporal Key Integrity Protocol), 838

TLDs (top-level domains), 780

TLS (Transport Layer Security), 1024–1025, 1212–1213

TN (twisted nematic) technology

description, 689

mobile devices, 1009

portable devices, 966

tokens

authentication, 1082, 1178–1179

software, 562

toner cartridges

disposal, 1147

laser printers, 1108–1109

toner vacs for laser printers, 1153

toners

cable troubleshooting, 820–821

laser printers, 1110–1111, 1129, 1152

Tool tab in system setup utility, 168–169, 171

Tools tab in System Configuration, 464

top command, 629–630

top-level domains (TLDs), 780

topology diagrams, network, 1224–1225

touch calibration, 1001

touch pens

mobile devices, 1018

portable devices, 964–965

touch screens

functions, 389–390

mobile devices, 1059–1062

portable devices, 964

troubleshooting, 1000

touchpads, 385

tower spoofing, 1091

TPMs (Trusted Platform Modules)

BitLocker, 536

overview, 175–176

traceroute command, 787–789

tracert command, 787–789

traces on motherboards, 191

tracing cable, 820–821

trackballs, 963

trackpads

portable devices, 964

troubleshooting, 1000

TrackPoint device, 963

tracks, sound, 398

tractor-feed paper for impact printers, 1103

training

malware, 1194, 1199–1200

mobile application security, 1086–1087

traits of techs, 3–6

transducers in hard drives, 274

transfer belts in laser printers, 1129

transfer corona in laser printers, 1110, 1154

transfer rate in PCIe, 207

transfer rollers in laser printers, 1110

transferring files, 911–914

transferring step in laser printers, 1128

transformers in chargers, 984

Transmission Control Protocol (TCP), 783–784

Transmission Control Protocol/ Internet Protocol (TCP/IP)

configuring, 789–790

Internet, 870–871

LANs, 770

settings, 784

tools, 784–789

transmission power in wireless networks, 844–845

transmit beamforming in 802.11n, 841

Transport Layer Security (TLS), 1024–1025, 1212–1213

travel issues with portable devices, 983–984

tray settings for printer paper, 1138

triggers

ports, 1202–1203

Task Scheduler, 555

trim feature in solid-state drives, 325

triple-channel memory architecture in DRAM, 131

tripping hazards

cables, 18

portable devices, 982

Trivial FTP (TFTP), 914

Trojans, 1186

troubleshooting

Bluetooth, 856–858

CPUs, 114–115

expansion cards, 217–220

hard drive installation, 302

hard drives, 361–366

Internet, 916–924

LANs, 817–825

methodology, 19–25

mobile devices. See troubleshooting mobile devices

monitors, 718–721

motherboards, 226–229

operating systems. See troubleshooting operating systems procedures; troubleshooting operating systems symptoms

portable devices, 995–1001

power supplies, 265–269

printers, 3-D, 1157–1158

printers, general issues, 1141–1148

printers, impact, 1148–1149

printers, inkjet, 1150–1152

printers, laser, 1152–1157

printers, thermal, 1149–1150

projectors, 722

RAID, 365–366

RAM, 148–150

tools for application security issues, 1086–1090

USB, 377–378

video, 717–724

video cards and drivers, 723–724

Windows installation, 447–448

wireless networks, 858–862

troubleshooting mobile devices

applications, closing, 1057–1058

applications, launching issues, 1063

applications, uninstalling, 1059

battery issues, 1065–1069

configuration settings, 1057

connectivity and data usage, 1071–1072

external monitors, 1070

factory resets, 1059

introduction, 1055–1056

overheating, 1063–1064

reboots and freezes, 1069–1070

response issues, 1064–1065

review questions, 1097–1099

soft resets, 1058

speakers, 1070–1071

tools, 1056–1059

touchscreen and display issues, 1059–1062

update failures, 1064

troubleshooting operating systems procedures

applications, 653–654

introduction, 651–652

recovery, 654–665

resetting devices, 652–653

resource requirements, 654

review questions, 683–685

system file check, 653

troubleshooting operating systems symptoms

application crashes, 672, 681

black screens, 677–678

Blue Screen of Death, 666

boot problems, 668

burning smells, 680–681

capacitor swelling, 682

crash screens, 677

date and time issues, 682–683

grinding noises, 682

introduction, 665–666

low memory, 672

OS missing, 674–675

overheating, 679–680

performance, 667–668, 679

POST, 677

power missing, 678

profile load speed, 675

review questions, 683–685

services not starting, 671

shutdowns, 668–669, 681

system instability, 673–674

time drift, 675–676

USB controller resources, 672–673

Trusted Platform Modules (TPMs)

BitLocker, 536

overview, 175–176

trusted root CAs, 1214

trusted sources

software, 1083–1084

Web browsers, 890

tunneling

SSH, 904

virtual private networks, 909

TWAIN (Technology Without an Interesting Name) drivers, 1118

twisted nematic (TN) technology

description, 689

mobile devices, 1009

portable devices, 966

two-factor authentication, 1082, 1176–1177

Two-way mirror Storage Spaces, 353–354

TXT (text) records, 781

Type-1 hypervisors, 945

Type-2 hypervisors, 945

Type-A USB connectors, 374

Type-B USB connectors, 374

Type-C USB connectors, 1046–1047

type command, 607

type setting for printer paper, 1138

U

UAC. See User Account Control (UAC)

UDP (User Datagram Protocol), 783–784

UEFI Firmware Settings option, 662

UEFI (Unified Extensible Firmware Interface), 161–162

default and optimized settings, 181–182

POST, 180–181

UHS (Ultra High Speed) bus, 406

UIs. See user interfaces (UIs)

Ultimate Boot CD, 1198

Ultra HD monitor resolution, 725

Ultra High Speed (UHS) bus, 406

ultra-wide (80 MHz) channels, 839

unapproved software sources, 1084

unattended Windows installations, 432

unauthorized access

attacks, 1165

mobile applications, 1092–1095

unauthorized camera and microphone activation, 1095–1096

unauthorized location tracking, 1095

unboxing printers and multifunction devices, 1124

unbuffered RAM, 136

UNC (Universal Naming Convention) paths, 823

unexpected behaviors in mobile applications, 1091

unexpected resource use in mobile applications, 1090–1091

Unified Extensible Firmware Interface (UEFI), 161–162

default and optimized settings, 181–182

POST, 180–181

unified Internet e-mail accounts, 901–902

unified threat management (UTM), 1211

Uninstall Updates option, 659, 661

uninstalling

applications, 653–654

mobile applications, 1059

unintended connections to mobile applications, 1091–1092

uninterruptible power supplies (UPSs)

overview, 244–246

rack-mounted, 757

Universal Naming Convention (UNC) paths, 823

universal plug and play (UPnP), 882–883

Universal Product Code (UPC) barcodes, 388–389

Universal Serial Bus Implementers Forum (USB-IF), 371

universal serial bus (USB), 370

bootable drives, 655, 1198

cables and connectors, 374–376, 696–697, 1046–1047

description, 370–371

digital cameras, 396

digitizers, 395

external wireless network adapters, 830

flash memory drives, 404–405

hubs, 376–377

keyboards, 382

locks, 1174

microphones, 401

mobile devices, 1046–1047

motherboards, 202–203

permissions, 173–174

portable devices, 973–974

printers and multifunction device connections, 1123–1124

standards and compatibility, 371–374

thumb drives, 404

troubleshooting, 377–378

video displays, 696–697, 700

unmanaged switches in LAN connections, 795

unofficial software sources, 1084

unpatched systems vulnerabilities, 1170

unprotected systems vulnerabilities, 1170–1171

unshielded twisted pair (UTP)

Ethernet, 745–748

patch panels, 759

solid core vs. stranded core, 755

unsigned device drivers, 214

untrusted software sources, 1083–1084

unwanted notifications from malware, 1189

UPC (Universal Product Code) barcodes, 388–389

Update & Security settings, 465

updated definition files for antivirus programs, 1196

updates

applications, 653–654

drivers, 218–219, 449, 716–717

firmware, 185–186

mobile devices, 1064

rolling back, 661

routers firmware, 884–885

scripts, 641

uninstalling, 659

WAP firmware, 860

Windows installation, 449

upgrade installs, 430–431

upgrades

considerations, 220–221

laptops, 988–991

UPnP (universal plug and play), 882–883

UPSs (uninterruptible power supplies)

overview, 244–246

rack-mounted, 757

upstream USB host controllers, 371

USB. See universal serial bus (USB)

USB controller resource warning, 374, 672–673

USB-IF (Universal Serial Bus Implementers Forum), 371

USB selective suspend, 378

User Account Control (UAC)

account changes, 516

issues, 539–542

levels, 544–546

operation, 542–543

program changes, 546–547

software installation, 565

User Accounts applet, 516

user data files in Windows installation, 449

User Datagram Protocol (UDP), 783–784

user education

about malware, 1194, 1199–1200

mobile application security, 1086–1087

user interfaces (UIs)

command-line, 50–52

description, 32

Linux, 50

macOS, 47–49

mobile devices, 1019

operating systems, 42

Windows, 42–47

user passwords in system setup utility, 167

user profiles, rebuilding, 663–665

User State Migration Tool (USMT), 450

usernames

authentication, 517–519

routers, 881

single sign-on, 423

Windows installation, 443

workgroups, 421–422, 800–801

users and user accounts

asset management, 1223

authentication, 508–510, 516–520

authorization, 520–529

configuring, 511–516

introduction, 507

mobile applications access issues, 1093

review questions, 547–549

security, 1181–1182

synchronization, 1044–1045

Users folder, 56, 810

Users tab in Task Manager, 479–480

USMT (User State Migration Tool), 450

Utilities folder, 60–61

utility protocols functions and ports, 888

UTM (unified threat management), 1211

UTP (unshielded twisted pair)

Ethernet, 745–748

patch panels, 759

solid core vs. stranded core, 755

V

VA (vertical alignment) panels, 689

VA (volt-amps) rating for UPSs, 244–245

validity of licenses, 1239

values

Registry, 460–461

scripts, 643

variables

environment, 646–647

scanners, 1120–1121

scripts, 644

.vbs files, 639

VDI (virtual desktop infrastructure), 955

vendor-specific development models, 1015

vendor-specific stores, 1033

ventilation

CPUs, 115

HVAC systems, 1233–1235

vents cleaning, 680

Verbose event levels in Event Viewer, 491

verifying

backups, 578

device drivers, 216–217

requirements, 654

troubleshooting, 23–24

versions

video display connections, 694

Windows, 420–427

vertical alignment (VA) panels, 689

VESA display mounts, 698–699

VGA (Video Graphics Array)

connectors, 704

monitor resolution, 725

video displays, 694–695

video and video displays

add-on features, 700

adjustments, 698

common features, 694–700

connections, 694–698

display adapters. See display adapters; monitors

flat-panel, 688–691

formats, 402–403

motherboard ports, 203

projectors, 691–694

troubleshooting, 723–724

VESA mounts, 698–699

video-conferencing software, 908

Video Graphics Array (VGA)

connectors, 704

monitor resolution, 725

video displays, 694–695

video mode in monitor resolution, 725

video RAM (VRAM) in display adapters, 703

Video Speed Class of SD cards, 406

video surveillance, 1173

Videos folder, 55

View options in File Explorer, 473–474

View tab in Windows files, 54

viewing angle in monitors, 726–727

views in Event Viewer, 492

virtual assistants, 1020–1021

virtual desktop infrastructure (VDI), 955

virtual local area networks (VLANs), 796–797

virtual machine managers (VMMs), 939

virtual machines (VMs)

applications, 934–935

building, 939–942

creating, 935–938

description, 928

development testing, 934

hardware support and resource requirements, 935–936

installing, 939

names, 941

networks, 937–938

operating system installation, 942–944

purpose, 933–935

RAM, 937

sandboxing, 933–934

storage, 937

virtual memory, 138–142

Virtual Network Computing (VNC), 905

virtual printers, 1115

virtual private networks (VPNs)

mobile devices, 1023–1025

overview, 908–911

VirtualBox, 939–940, 943–944

virtualization

cloud, 945–955

CPU support for, 92

hardware. See hardware virtualization

introduction, 927

review questions, 955–957

VMs. See virtual machines (VMs)

Virus & threat protection tool, 1192

virus shields, 1191, 1196

viruses

antivirus programs, 1077–1078, 1192–1193

description, 1185–1186

polymorphic, 1194

stealth, 1194

vishing attacks, 1167

Visual Basic Script language, 639

Visual Effects tab, 572

VLANs (virtual local area networks), 796–797

VMMs (virtual machine managers), 939

VMs. See virtual machines (VMs)

VNC (Virtual Network Computing), 905

Voice over IP (VoIP)

application protocols, 886

quality issues, 923–924

Web browsers, 903–904

voice recognition, 388

VoIP (Voice over IP)

application protocols, 886

quality issues, 923–924

Web browsers, 903–904

volt-amps (VA) rating for UPSs, 244–245

volt-ohm meters (VOMs) for AC supply tests, 238

voltage

description, 234

portable devices, 983

volumes

creating, 338–341

dynamic disks, 312–313

manipulating, 662

simple, 342–343

spanning, 344–346

VOMs (volt-ohm meters) for AC supply tests, 238

VPNs (virtual private networks)

mobile devices, 1023–1025

overview, 908–911

VRAM (video RAM) in display adapters, 703

vulnerabilities

description, 1162

overview, 1170–1171

W

Wake-on-LAN feature

NICs, 793–794

portable devices, 977

WAN (static wide-area network) IP, 884

WANs (wide area networks)

addresses, 770

description, 765

WAPs. See wireless access points (WAPs)

Warning event levels in Event Viewer, 491

warnings, certificate, 1214

warped characters from laser printers, 1157

warranties in asset management, 1222–1223

watermarks, 1139

wattage

CPUs, 107

formula, 235

power supply requirements, 257–259

WAV sound format, 399

Waze application, 1012

WCS (Windows Color System), 1140

Web

application protocols, 886–888

applications, 949

Web browsers

configuring, 897–899

data browsing, 895–897

description, 736–737, 885–886

extensions and plug-ins, 891–892

installing, 890–891

overview, 889–890

password managers, 892–893

pop-up and ad blockers, 894–895

redirection, 1190

secure connections and sites, 893–894

Web mail, 900–901

Web servers, 736–738

webcams

overview, 396–397

portable devices, 965

Welcome screen, 428

WEP (Wired Equivalent Privacy), 837, 852

whack twenty-four subnets, 773

whaling attacks, 1167

while loops, 645

whitelists for MAC addresses, 1176

Wi-Fi

configuring, 848–856

Internet, 875

LANs, 751

mobile devices, 1033–1037

troubleshooting, 858–862

Wi-Fi 6, 841–842

Wi-Fi analyzers

description, 846

mobile applications, 1087

Wi-Fi calling in mobile devices, 1020

Wi-Fi channels in IEEE 802.11, 839–840

Wi-Fi Protected Access (WPA), 837

Wi-Fi Protected Access 2 (WPA2), 838, 852–854

Wi-Fi Protected Access 3 (WPA3), 838, 852–854

Wi-Fi Protected Setup (WPS), 837

wide (40 MHz) channels, 839

wide area networks (WANs)

addresses, 770

description, 765

wildcards in files, 619–620

Windows Color System (WCS), 1140

Windows Defender, 1192

Windows Defender Antivirus, 1195–1196

Windows Defender Firewall, 1204–1206

Windows Defender Firewall with Advanced Security, 1208–1210

Windows Defender Security Center, 1190–1191

Windows Features dialog box

settings, 571–573

virtual machines, 939

Windows Firewall, 1204–1206

Windows Hardware Compatibility Program, 214

Windows Hello, 386–387

Windows Logs in Event Viewer, 490–491

Windows media creation tool, 655

Windows Memory Diagnostic tool, 149

Windows operating system

autostarting software, 556–557

backups, 580–584

CD-media, 410–411

CLI access, 598–600

component adding and removing, 571–572

Control Panel. See Control Panel

display settings, 707–713

file history, 585

file structures and paths, 52–55

file systems, 318–330

installation, introduction, 419

installation, media sources, 428–430

installation, over networks, 445–447

installation, post-installation tasks, 449–453

installation, process, 433–445

installation, review, 453–455

installation, troubleshooting, 447–448

installation, types, 430–433, 440

installation, versions and editions, 420–427

maintenance scheduling, 555

Microsoft Management Console, 484–493

patch management, 552–553

performance options, 572–575

printer setup, 1130–1137

processes overview, 475

Resource Monitor, 482–484

review questions, 503–505

running programs, 615–616

settings overview, 464–467

software installation, 564–565

software removal, 569–572

System Configuration, 463–464

Task Manager, 475–482

tech utility launch points, 57–60

troubleshooting. See troubleshooting operating systems procedures

user and group configuration, 511–516

user interface, 42–47

Windows 10 Home, 421–423

Windows 10 Pro, 423–426

Windows 10 Pro for Workstations and Windows 10 Enterprise, 426–427

Windows 11, 420–421

workgroups vs. domains, 421–423

Windows Preinstallation Environment, 1198–1199

Windows Recovery Environment (WinRE) tools

anti-malware, 1197–1199

Command Prompt, 661–662

overview, 654–658

Reset this PC, 662–663

Startup Repair, 660–661

Startup Settings, 659

System Image Recovery, 659–660

System Restore, 658–659

UEFI Firmware Settings, 662

Uninstall Updates, 659

Windows Server domains, 421–422, 807–808

Windows Stop errors, 115

Windows Terminal, 598

Windows Tools in Control Panel, 58–59

Windows Update

failures, 1190

patch management, 552–553

WinRE. See Windows Recovery Environment (WinRE) tools

winver command, 626

wiping

hard drives, 451, 637

mobile devices, 1081

wire strippers, 760–761

Wired Equivalent Privacy (WEP), 837, 852

wired networks

installing and configuring, 791–797

portable devices, 971–972

wireless access points (WAPs)

antennas, 844

configuring, 848–852

description, 831

evil twin, 1167

firmware, 860

placement, 836

purpose, 833–835

troubleshooting, 862

wireless cards, replacing, 992–993

Wireless Communications and Public Safety Act, 1022

wireless devices, 998–999

wireless Internet service providers (WISPs), 876

wireless LANs (WLANs). See wireless networks

wireless locators, 846

wireless mesh networks (WMNs), 835

wireless networks

authentication, 837–838

battery usage, 1066–1067

Bluetooth, 846–848, 856–858

components, 829–832

configuring, 848–856, 862

connectivity issues, 860–862

coverage optimization, 843–846

guest, 836–837

hardware, 859

IEEE 802.11-based, 838–843

infrastructure, 833–834

MAC address filtering, 837

review questions, 863–865

security, 835–838, 1215–1216

software, 832–833, 860

troubleshooting, 858–862

Wireless Power Consortium (WPC), 1051

wireless WANs (WWANs), 876

WISPs (wireless Internet service providers), 876

WLANs (wireless LANs). See wireless networks

WMNs (wireless mesh networks), 835

work areas

Ethernet networks, 763–765

structured cabling, 754

workgroups

vs. domains, 421–423

folder access, 804–806

folder sharing, 801–804

introduction, 798–799

usernames and passwords, 800–801

Windows, 443

working directory in CLI, 602

World Wide Web

application protocols, 886–888

applications, 949

worms, 1186

WPA (Wi-Fi Protected Access), 837

WPA2 (Wi-Fi Protected Access 2), 838, 852–854

WPA3 (Wi-Fi Protected Access 3), 838, 852–854

WPC (Wireless Power Consortium), 1051

WPS (Wi-Fi Protected Setup), 837

WQHD monitor resolution, 725

wrappers in video formats, 402–403

Write permission

folders, 522–523

Linux, 528

write stage in CPUs, 92–93

WUXGA monitor resolution, 725

WWANs (wireless WANs), 876

X

X-Rite ColorMunki Display calibrators, 1140

x64 CPUs, 92

x86 CPUs, 92

x86-64 CPUs, 85, 92

Xcode for mobile devices, 1021

xcopy command, 623

XD bit in CPUs, 101

XML Paper Specification (XPS), 1116

XMP (Extreme Memory Profile), 131

XN bit in CPUs, 101

XPS (XML Paper Specification), 1116

XQD format, 407

XSS (cross-site scripting) attacks, 1165

Y

yum command, 633–635

Z

Z shell (zsh), 597

zero-day attacks, 1163

zero insertion force (ZIF) CPU sockets, 106–107

zeroconf feature, 790

ZFS file system, 330

zombies, 1188–1189


Copy
copy

Highlight
highlight

Add Note
note

Get Link
link
table of contents
search
Settings
queue
close x
Preparing for certification?

Take Practice Test
chevron right
