# Overview of Mass Storage Structure

**Hard Disk Drive (HDD)**: machanical (magnetic material)

**Nonvolatile Memory Devices (NVM)**: electrical (semiconductor)

## Hard Disk Drives

sector: smallest <mark style="color:blue;">unit of transfer</mark>

### Performance

**transfer rate**: data flow between drive and computer(related to <mark style="color:blue;">rotation speed</mark>)

**random-access time**: seek time + rotaional latency

**effective transfer rates**: random-access time(read) + transfer time(transfer)



## Nonvolatile Memory Devices

e.g., <mark style="color:blue;">NAND flash memory</mark>, DRAM with battery backing, ...

### Form of Flash-Memory-Based NVM

1. solid-state disk(SSD): disk-drive-like container
2. USB Drive
3. surface-mounted onto motherboards: e.g., main storage of smartphones

### Advantage

* more <mark style="color:blue;">reliable</mark>: have no moving parts
* <mark style="color:blue;">faster</mark>: have no seek time and rotational latency
* less <mark style="color:blue;">power</mark>
* more <mark style="color:red;">expensive</mark>
* less <mark style="color:red;">capacity</mark>

<mark style="color:blue;">faster</mark>  **->** connect directly to the system bus (e.g., PCIe)

1. replacement for disk drives
2. new cache tier to optimize performance

### Operations

**read and write** in page (like sector) increment

**erasure** in block (several pages) increment: take much more time

{% hint style="warning" %}
there's no overwrite
{% endhint %}

{% hint style="info" %}
NAND semiconductors <mark style="color:blue;">deteriorate</mark> with every earse cycle, the limitations leads to ameliorating algorithms.

Algorithms are implemented in NVM device controller, and can lead to various <mark style="color:blue;">performance</mark> variations
{% endhint %}

### NAND Flash Controller Algorithms

<mark style="color:blue;">flash translation layer (FTL)</mark>:&#x20;

1. maps which physical pages is valid
2. tracks physical block state (which blocks contain only invalid pages)

#### if SSD is full:

if there's a block containing no valid data

&#x20;   **->** erase and then write

else

&#x20;   **->** **garbage collection** (copy good data to other locations and free up blocks)

&#x20;       **->** **over-provisioning**: set aside pages (20% of the total) as area always <mark style="color:blue;">available for garbage collection</mark> to store good data

**wear leveling**: place data on less-erased blocks so that subsequent erases will happen on those blocks (<mark style="color:blue;">over-provisioning space can help with</mark> wear leveling)

## Volatile Memory

**RAM drive**: created by device drivers by carving out a <mark style="color:blue;">section of the system's DRAM</mark>, acting as <mark style="color:blue;">secondary storage</mark>

<mark style="color:blue;">high speed temporary</mark> storage space&#x20;

&#x20;   **->** file systems are created on them for standard file operations

1. share data easily by writing and reading files
2. Linux creates a temprary root file system at boot time

## Secondary Storage Connection Methods

HDD: e.g., SATA (carried out by <mark style="color:blue;">host-bus adapter</mark>)

NVM: NVM express (<mark style="color:blue;">directly connects</mark> to system PCI bus)

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## Address Mapping

**logical blocks**: map to physical sectors or semiconductor pages (1 to 1)

<mark style="color:blue;">logical block address (LBA)</mark> is easier for algorithms to use than a sector
