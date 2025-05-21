---
tags:
  - git
---

# 🧰 Git Cat-File — Low-Level Object Inspector

`git cat-file` is a powerful plumbing command that lets you **inspect Git objects** directly by their SHA-1 hash.

---

## 📌 Syntax

```bash
git cat-file <option> <object>
````

Where:

- `<option>` specifies the action (`-t`, `-s`, `-p`, etc.)
    
- `<object>` is the SHA-1 hash (or any ref, like `HEAD`, `HEAD^{tree}`, etc.)
    

---

## 🧪 Common Options

|Option|Description|
|---|---|
|`-t`|Show the object **type** (blob, tree, commit, tag)|
|`-s`|Show the object **size** (in bytes)|
|`-p`|Pretty-print the **content** of the object|
|`-e`|Check if the object **exists** (no output, returns 0 or 1)|
|`--batch`|Read many object IDs from stdin and dump info|
|`--batch-check`|Same as above but only type and size (fast lookup)|

---

## 📦 Object Types

|Type|Description|
|---|---|
|`blob`|File contents (raw text or binary)|
|`tree`|Directory listing (points to blobs/trees)|
|`commit`|Commit metadata and pointer to tree|
|`tag`|Annotated tag (points to other objects)|

---

## 📋 Examples

### 🔍 1. Show the Type of an Object

```bash
git cat-file -t <sha>
```

> Example:

```bash
git cat-file -t HEAD^{tree}
# Output: tree
```

---

### 📐 2. Show the Size of an Object

```bash
git cat-file -s <sha>
```

> Example:

```bash
git cat-file -s HEAD
# Output: e.g., 256
```

---

### 📖 3. Pretty Print Object Content

```bash
git cat-file -p <sha>
```

> Works for **commits**, **trees**, **blobs**, and **tags**.

#### 🔎 Commit:

```bash
git cat-file -p HEAD
```

#### 📂 Tree:

```bash
git cat-file -p HEAD^{tree}
```

#### 📄 Blob:

```bash
git ls-tree HEAD
# Find a blob hash, then:
git cat-file -p <blob-hash>
```

---

### 🧯 4. Check Object Existence

```bash
git cat-file -e <sha>
```

> Returns `0` (success) if object exists, no output.

---

## 🔁 Batch Mode

Efficient when working with many objects.

### Example:

```bash
echo HEAD | git cat-file --batch
```

> Outputs type, size, and raw content of the object.

---

## 🧠 Why Use `git cat-file`?

- Inspect what Git _really stores_
    
- Debug plumbing-level issues
    
- Understand how objects are connected (e.g., commit → tree → blobs)
    
- Explore Git internals manually
    

---

## 📦 Related Commands

- `git hash-object`: Compute or store a blob from a file.
    
- `git ls-tree`: View tree structure (directory contents).
    
- `git rev-parse`: Resolve refs to hashes.
    

---

## 🧪 Try It Yourself

```bash
# Create a file
echo "hello world" > hello.txt

# Add to git and get blob hash
git add hello.txt
git hash-object hello.txt
# => abc123...

# Inspect with cat-file
git cat-file -t abc123...     # => blob
git cat-file -s abc123...     # => file size
git cat-file -p abc123...     # => hello world
```

---

## 🔍 See Also

- [Git Internals Book](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain)
    
- `man git-cat-file`
    