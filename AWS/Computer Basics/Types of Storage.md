# Storage Types

[Source](https://aws.amazon.com/what-is/block-storage/)

> [!note] Block Storage
> In block storage, data are stored in a fixed-sized blocks. When one part of the data is modified, only the corresponding block gets changed. 
> 
> Block storage has high performance for data retrieving and accessing, is platform-independent, is scalable, is efficient for updating large files, and is amenable to granular control. Developers can specify which block to store the data to optimize retrieving speed.
> 
> Use cases include: **storage area networks**, **containerized applications**, **transactional workloads**, and **VM Machines**. It is primarily useful for structured database storage, VM file system volumes, and high volumes of read and write loads.

^ecdca8

> [!note] Instance Storage
> An [instance store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) provides temporary block-level storage for your instance. This storage is located on disks that are **physically attached** to the host computer.
> 
> Instance store is ideal for *temporary storage* of information that changes frequently, such as buffers, caches, scratch data, and other temporary content. It's also useful for data that's *replicated across a fleet of instances*, such as a load-balanced pool of web servers.
> 
> An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available vary by instance type.

^f4da18

> [!note] Object Storage
> Object storage is used for storing unstructured data, such as text, videos, and audios. Each **object** is tagged with a unique **identifier** and contains **metadata** that describes the underlying content.
> 
> When an object is modified, the entire object is updated, compared to block storage where only the affected block is updated.

^77504f

> [!note] File Storage
> 
> File storage stores data in a hierarchical structure of files and folders. In network environments, file-based storage often uses [network-attached storage (NAS)](https://aws.amazon.com/what-is/nas/) technology. NAS allows users to access network storage data in similar ways to a local hard drive. File storage is user-friendly and allows users to manage file-sharing control.

