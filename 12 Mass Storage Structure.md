## Chapter 1.2: System Structures

- Bus connects the drive to the computer

- Host controller (end of bus) allows for transferring of commands (via messages) to the disk controller (built inside the drive).

- Disk controllers usually have a built-in cache.

- SSD - have no moving parts, no latency, consume less power; expensive, less capacity, shorter life span; directly connected to the system bus (PCI); 

- magnetic tapes - slower access time than magnetic disks and main memory; these types of tapes are mainly used for backups; 

- Disk scheduling:
    + **FCFS** - problem with request on heads far apart
    + **Shortest-seek-time-first (SSTF) algorithm** - takes care of the requests close to the head (with least seek time); a form of SJF algorithm and may lead to starvation of some requests
    + **SCAN scheduling** - scan back and fort and service requests as they are being scanned; avoid starvation
    + **Circular Scan (C-SCAN) scheduling** - scan back and fort but only service requests one way
    + **LOOK Scheduling** - only scans until meeting the last request on one end and then moves back.

- Disk Management:
    + Low-level formatting - fills the disk with a special data structure for each sector; includes partitioning disk into cylinders and logical formatting (creation of a file-system)
    + Boot Block - stores bootstrap program which initializes all aspects of the system, from cPU registers to devise controllers and the contents of main memory, and then starts the operating system; a disk that has boot partition is called a boot disk or system disk; master boot record (MBR) contains boot code and partition table.
    + Bad Blocks - bad block are search for so as to make unusable; these are usually replaced with a spare; to ensure optimization the replacement sector is chosen with the cylinder

- Virtual memory is a feature of an operating system (OS) that allows a computer to compensate for shortages of physical memory by temporarily transferring pages of data from random access memory (RAM) to disk storage.

- swap space - moving process information (code and data segments) from main memory -- because of critical low point -- to a swap space location on disk

- swap space can be located on the file system or the raw partitions; the trade-off is between the convenience of allocations and management in the file system and the performance of swapping in raw partitions.

- Redundancy arrays of independent disks (RAID) - setting up disk in parallel to improve performance (higher data-transfer rate) and reliability; 
    + Improving reliability via Redundancy -
        * Mirroring - a logical disk consists of two physical disks and every write is carried out on both disks (mirrored volume); rate of failure is reduced because there is a low probability that both disks will fail at the same time (this also depends on the time it take to repair a disk);
        * 

