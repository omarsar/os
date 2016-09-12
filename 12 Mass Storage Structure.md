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
    + Improve in Performance via Parallelism - Data stripping or bit level stripping (consist of splitting the bits of each byte across multiple disks); every disk participates in every access, so the number of accesses that can be processed per second is about the same as on a single disk, but each access can read eight times as many data in the same time as on a single disk; block-level stripping (in blocks); this increases throughput

- Mirroring provides high reliability, but it is expensive. Stripping provides high data transfer rate, but it does not improve reliability.


- Raid Levels - different levels to provide redundancy at lower cost by using disk stripping combined with "parity" bits
    + RAID level 0 - disk arrays with stripping but no redundancy
    + RAID level 1 - disk mirroring
    + RAID level 2 - uses ECC to detect corrupted data; data is stored in disk using stripping; further disk then hold error-correction bits; if one disk fail the remaining bytes stored in the other disks and the associated error-correction bits can be read from other disks to reconstruct the damaged data; three disk overhead
    + RAID level 3 - one disk overhead, less disk require; parity bits of sectors are computed and compared to  to see if data has been lost of corrupted; uses bit stripping
    + RAID level 4 - uses block stripping; one parity disk
    + RAID level 5 - data and parity bits are distributed among disks; a parity block cannot store parity for blocks in the same disk, because a disk failure would result in loss of data as well as of parity, and hence loss would not be recoverable; avoid overuse of a single parity disk
    + RAId level 6 - almost like level 5 but also uses redundancy to guard against multiple disk failures; error correcting code is used;
    + RAID level 0 + 1 and 1 + 0 - 
        * RAID 0 + 1 combines the idea of RAID level 0 and RAID level 1 to increase performance and reliability; it also requires more disks; if a single disk fails then one entire strip is lost; disks are stripped then mirrored;  
        * RAID level 1 + 0 - first disks are mirrored then stripped; if one disk fails then other mirror is still available for restoring.
        
