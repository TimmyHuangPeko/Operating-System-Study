# 11-2 HDD Scheduling

1. minimize <mark style="color:blue;">access time</mark> (seek time + rotational latency)
2. maximize <mark style="color:blue;">bandwidth</mark> (total number of bytes transferred / total time)

<mark style="color:blue;">multiprogramming</mark> system

&#x20;   **->** device queue has several <mark style="color:blue;">pending requests</mark>

&#x20;   **->** <mark style="color:blue;">queue ordering</mark>/disk scheduling (avoid head seeks)

goal of disk scheduling:

* **fairness**
* **timeliness**
* **optimizations**

{% hint style="info" %}
assume that increasing LBAs mean increasing physical addresses
{% endhint %}

## FCFS Scheduling

first-come, first-served (FIFO)

* fair
* not fastest

## SCAN Scheduling

1. begin with one direction
2. move toward the end
3. reverse the direction and move toward the other end

(service requests as it reaches each cylinder)

* heavy load on the disk
* less likely to cause starvation

{% hint style="info" %}
when reaching one end of the disk, the heaviest density of requests may be at the other end, why not go there first?

&#x20;   **->** C-SCAN Scheduling
{% endhint %}

## C-SCAN Scheduling

variant of SCAN: treat cylinders as a <mark style="color:blue;">circular</mark> list

* heavy load on the disk
* less likely to cause starvation
* more <mark style="color:blue;">uniform wait time</mark>

## Selection of a Disk-Scheduling Algorithm

for any particular list of requests, there might be an optimal order of retrieval, but the <mark style="color:blue;">computation needed to find the optimal schedule</mark> may not justify the savings over <mark style="color:blue;">SCAN</mark>

### Deadline Scheduler

1. two read queues and two write queue, one sorted by LBA and the other by FCFS
2. after each batch of I/O requests sent, check if there're requests in FCFS queues being expired
3. if so, the LBA containing the requests is selected for the next batch of I/O

{% hint style="info" %}
1. reads are given priority since processes are more likely to block on read
2. all I/O requests are sent in a batch in LBA ordered queue
{% endhint %}
