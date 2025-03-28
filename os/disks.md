# Disks
## Disk scheduling algorithms
Done by the operating systems to schedule I/O requests arriving for the disk

* **Seek Time**  is the time taken to locate the disk arm to a specified track where the data is to be read or write
* **Rotational Latency**  is the time taken by the desired sector of disk to rotate into a position so that it can access the read/write heads
* **Transfer Time**  is the time to transfer the data. It depends on the rotating speed of the disk and number of bytes to be transferred

**Disk Access Time** is the sum of the previous ones

**Disk Response Time** is the average of time spent by a request waiting to perform its I/O operation
### FCFS (First Come – First Service)
The requests are addressed in the order they arrive in the disk queue
| Advantages | Disadvantages |
|--|--|
| Every request gets a fair chance | Does not try to optimize seek time |
| No indefinite postponement | May not provide the best possible service |

### SSTF (Shortest Seek Time First)
Requests having shortest seek time are executed first
So, the seek time of every request is calculated in advance in the queue and then they are scheduled according to their calculated seek time
| Advantages | Disadvantages |
|--|--|
| High throughput | Long waiting time for requests for locations just visited by disk arm |
| Low variance of response time |  |
| Average response time |  |
### SCAN
The disk arm again scans the path that has been scanned, after reversing its direction
May be possible that too many requests are waiting at the other end or there may be zero or few requests pending at the scanned area
| Advantages | Disadvantages |
|--|--|
| High throughput | Long waiting time for requests for locations just visited by disk arm |
| Low variance of response time |  |
| Average response time |  |
#### CSAN (Circular SCAN)
The disk arm moves in a circular fashion
| Advantages | Disadvantages |
|--|--|
| Provides more uniform wait time compared to SCAN |  |
### LOOK
Similar to SCAN
The arm of the disk stops moving inwards (or outwards) when no more request in that direction exists
#### CLOOK
### RSS
### LIFO
### N-STEP SCAN
### FSCAN
## RAID (Redundant Array of Inexpensive Disks)
**SoftRaid**, operációs rendszer nyújtja
**HardRaid**, valamely külső vezérlőegység

Több lemezt fog össze, és egy logikai egységként látja az operációs rendszer

### RAID 0 (Striping)
Nem redundáns
Több lemez logikai összefűzésével egy meghajtót kapunk
A lemezkapacitások összege adja az új meghajtó kapacitását
A logikai meghajtó blokkjait szétrakja a lemezekre (striping), ezáltal egy fájl írása több lemezre kerül
Gyorsabb I/O műveletek
Nincs meghibásodás elleni védelem
### RAID 1 (Mirroring)
Két független lemezből készít egy logikai egységet.
Minden adatot párhuzamosan kiír mindkét lemezre
Tároló kapacítás felére csökken
Drága
Mindkét lemez egyszerre történő meghibásodása okoz adatvesztést
### RAID 1+0, RAID 0+1
RAID 1+0: Tükrös diszkekből vonjunk össze többet
RAID 0+1: Raid 0 összevont lemezcsoportból vegyünk kettőt
A vezérlők gyakran nyújtják egyiket, másikat, mivel így is, úgy is tükrözés van, azaz drága, így ritkán használt
### RAID 2
Adatbitek mellett hibajavító biteket is tartalmaz
### RAID 3
Elég egy plusz „paritásdiszk”, n+1 diszk, Σ n a kapacitás
### RAID 4
RAID0 kiegészítése paritásdiszkkel
### RAID 5
Nincs paritásdiszk, ez el van osztva a tömb összes elemére (stripe set)
Adatok is elosztva kerülnek tárolásra
Intenzív CPU igény (vezérlő CPU!!!)
Redundáns tárolás, 1 lemez meghibásodása nem okoz adatvesztést
N lemez RAID 5 tömbben(N>=3), n-1 lemez méretű logikai meghajtót adű
### RAID 6
A RAID 5 paritásblokkhoz, hibajavító kód kerül tárolásra.(+1 diszk)
Még intenzívebb CPU igény
Két diszk egyidejű kiesése sem okoz adatvesztést!
Relatív drága
N diszk RAID 6-os tömbjének kapacitása, N-2 diszk kapacitással azonos
Elvileg általánosítható a módszer
### Összegzés
Leggyakrabb a RAID 1,5
Hot-Swap(forró csere) RAID vezérlő: működés közben a meghibásodott lemezt egyszerűen kicseréljük
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjEyNjE4MDFdfQ==
-->