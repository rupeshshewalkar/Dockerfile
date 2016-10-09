

### Docker uses union filesystem
Docker uses union filesystems to store images. This means that each image is made of a base image plus a collection of diffs that adds the required changes. Each diff represents an additional layer of an image. This has a
direct impact on how your write your Dockerfile and use the various directives.



### Docker architect has two main features, which provides isolation and resource management in docker.

**cgroup [control group]:** 

cgroup is built into kernel space. It primary responsibility is provide the resource usage isolation [cpu,memory,disk and network]. cgroup provides the guaranteed resource to any application or set of application. This can modify the resource allocation on the fly.cgroup also monitor the resource allocation.

	docker stats <container id> /*this command will show the resource usages*/

	CONTAINER           CPU %               MEM USAGE/LIMIT     MEM %                 NET I/O
	a21ac26f720f        0.00%               5.345 MB/2.088 GB           0.26%               7.236 kB/1.055 kB
 
 
**Cgroups involve resource metering and limiting:**

    memory
    CPU
    block I/O
    network



**Namespace:** 

Namespace provide the isolation view. This basically provides the process virtualization. A few set of kernel name space is mentioned below

      mnt [mount points, file system]
      pid [process]
      net [network]
      ipc [inter process communication]
      uts [hostname]
      user[UIDS

**In short:**

Cgroups = limits how much you can use;

namespaces = limits what you can see (and therefore use)