---
tags:
  - git
---

# 🧠 Understanding Git Clone: Objects and Deltas

When running `git clone`, Git transfers a **history of changes**, not just files. This involves:

- **Objects**: Core building blocks of Git history.
- **Deltas**: Efficient compression using differences between objects.

---

## 📦 What Are Git Objects?

Git stores data as objects in the `.git/objects/` directory.

| Object Type | Description                                         |
| ----------- | --------------------------------------------------- |
| **Blob**    | File content (no filename/path)                     |
| **Tree**    | Directory (contains paths to blobs/trees)           |
| **Commit**  | Snapshot + metadata (author, message, parent, etc.) |
| **Tag**     | Named pointer to another object (e.g., a commit)    |

A single commit might refer to **many objects** (files, directories, etc.).

---

## 🌀 What Are Deltas?

To save space and bandwidth, Git uses **delta compression**:

- Stores **full objects** for some files.
- Stores **deltas** (changes) for others:
  > Example: If one line changes in a large file, Git stores only that change (delta), not a new full copy.

---

## 🧳 [[Packfiles]]

When cloning, Git transfers data in a **packfile**:
- Contains compressed objects and deltas.
- Optimized for minimal size and fast transfer.
- Unpacked and resolved locally on your machine.

---

## 🖥️ Example Output Explained

```

Cloning into 'keus-iot-cloud'...  
remote: Enumerating objects: 7315, done.  
remote: Counting objects: 100% (203/203), done.  
remote: Compressing objects: 100% (114/114), done.  
remote: Total 7315 (delta 103), reused 90 (delta 89), pack-reused 7112  
Receiving objects: 100% (7315/7315), 24.83 MiB | 6.06 MiB/s, done.  
Resolving deltas: 100% (4395/4395), done.

```

### Breakdown:

| Line | Meaning |
|------|---------|
| `Enumerating objects: 7315` | Git found 7315 objects to send (blobs, trees, commits, etc.) |
| `Counting objects: 203`     | These are the objects being newly packed |
| `Compressing objects: 114`  | These 114 are being compressed |
| `delta 103`                 | 103 objects are stored as deltas (differences) |
| `pack-reused 7112`          | 7112 objects reused from an existing server-side packfile |
| `Receiving objects`         | Your machine received all objects |
| `Resolving deltas`          | Your Git client reconstructed full objects from deltas |

---

## ✅ Summary

| Concept | Description |
|--------|-------------|
| **Object** | A core unit in Git: blob, tree, commit, or tag |
| **Delta** | A compressed difference between two objects |
| **Packfile** | A bundle of compressed objects and deltas |
| **Enumerating** | Git finding what to send |
| **Compressing** | Making objects smaller for transfer |
| **Resolving deltas** | Reconstructing full files locally |

---

## 🛒 Analogy

Imagine Git like a store cashier:

- You (the producer) give **receipts** (objects) with **serial numbers** (IDs).
- If you retry a transaction, Git can say **"Already got this!"** (detect duplicate).
- But if you leave and return (new session), Git **forgets the earlier serials** — just like a new cashier.

---

## 🔍 Want to Go Deeper?

- [ ] Explore `.git/objects/` manually
- [ ] Inspect a `.pack` file with `git verify-pack`
- [ ] Try `git cat-file` to decode objects
- [ ] Learn how Git generates and stores deltas internally
