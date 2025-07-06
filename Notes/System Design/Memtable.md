### ✍️ Write Operation Flow

- Writes go to the **memtable** (in-memory) — this is **fast**.

- Once the memtable exceeds a **predefined memory threshold**, it is:
    
    - **Flushed to disk** as an **SSTable** (Sorted String Table).
        
    - This SSTable is **immutable** — it cannot be modified once written.
        
- After flushing:
    
    - A **new memtable** is created for subsequent writes.
        
    - **Updates** or **deletes** to previous data are logged in the **new memtable**, not by modifying the old SSTable.
        

---

### 🔎 Read Operation Flow

1. **Check in current memtable.**
    
2. If not found:
    
    - Check **recently created SSTables** in **reverse creation order** (most recent first).
        
    - Stop when:
        
        - The record is found, or
            
        - All sources are exhausted.
            
3. SSTables are **sorted**, enabling **binary search**, making lookups faster.
    

---

### Memtable Implementation Options

Memtables can be implemented using different data structures:

- `Red-Black Tree`
    
- `SkipList`
    
- `HashSkipList`
    
- `HashLinkList`
