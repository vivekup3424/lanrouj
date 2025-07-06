---
tags:
  - database-design
  - system-design
  - database
---
**### Objectives for database
1. Fast reads
2. Fast writes
3. Persistent data


### Things that we can use for data storage
1. Hard Disk Drive
	1. results in slower reads
	2. since data is read from a spindle hence they are best for sequential operations

for a naive database implementation, use a list, that way you would be doing read/write operations in
O(n) time.

a slightly better implementatio would be to make use of append only logs, this means that for a update on a field we are not going to search for the field inside our database,
rather we will just create a new entry for that data-field with updated information.
This thing is very useful in the case when we are writing more than we are reading.

a more better implementation would be make use of a hashmap to store the data (with a hash associate to it)
so that it can be accessed in constant time quickly by calculating the hash, and checking whether there exists any data present in
our database for the hash-value.

However this becomes a problem as soon as we have large amount of data, so that we have started writing that data on the disk.

But Indexes can make reading times much faster
Pro - faster reads
Con - Slower writes(only use indexes if you need them, do not create index for evey field)

There are several types of index implementations

1. Hash indexes
	1. Keep an in memory hash table of key mapped to the memory location of where the data exists
	 ![[Pasted image 20250702164101.png|200]]
	 1. Easier to implement and very fast if the data is inside the memory
	 2. But all of the keys must fit in memory, bad for range queries
2. SST Table/LSTM trees
	1. Read about [[Memtable]]
3. B Trees