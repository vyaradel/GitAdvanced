# Git


## What is Git and how did it all start?
- [Linux kernel & BitKeeper](https://en.wikipedia.org/wiki/BitKeeper)
- Tables turn in April 2005
- Git is being born on the concepts of: Distributed Version Control, Snapshots, Branching & Merging, Data Integrity
<br>

![image](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExMXdybTcwNDltZGhwaHZrb3dxaGUwZmh4d2c0NmE4OTIxanJ2Z3I0bSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/du3J3cXyzhj75IOgvA/giphy.gif)


<br>

### Okay, but still, what is Git?
- Merkle Directed Acyclic Graph (Merkle Tree + DAG) <br>
(actually the repo is)
(Git is VCS)

#### And a Merkle Tree: <br>
Also known as a hash tree, is a data structure used in computer science and cryptography to efficiently and securely verify the integrity of data. It is a binary tree where each leaf node contains a hash of a block of data, and each non-leaf node contains a hash of its child nodes. This structure allows for quick and reliable verification of data integrity and consistency <br>
<br>
![image](https://media.github.ibm.com/user/467971/files/1b1bbfdf-9441-487b-9911-014f1d88f63e)

#### And a DAG: <br>
A DAG is a graph that flows in one direction, where no element can be a child of itself. So most of us are familiar with LinkedLists, trees, and even graphs. A DAG is very similar to the first two, and an implementation of the third
<br>
![image](https://media.github.ibm.com/user/467971/files/055d9002-1ef8-4cb1-9a67-2b8a85a28e37)

Core characteristics: 
- Hash
- Binary Tree Structure
- Efficient Verification
- Immutability
<br>


#### Is this a data structures presentation or are we going back to Git?
That's right! Let's get serious!
 
Git Structure: 
<br>
![image](https://media.github.ibm.com/user/467971/files/4e08d426-de0b-43f0-b1f6-6ad6e8aa4e07)

<br>

## .git
- initialized by ``git init`` and basically everything you need to perform version control, when you clone the git repo in your file system, you clone the .git object, contains: <br>
- 
#### Four sub-directories:
- hooks/ : example scripts
- info/ : exclude file for ignored patterns
- objects/ : all "objects" (there are 4 types f objects)
- refs/ : pointers to commit objects

#### Four files:
- HEAD : the current branch
- config : configuration options
- description
- index : staging area

and other stuff....
<br>
<br>
![image](https://media.github.ibm.com/user/467971/files/85a2a997-8852-458b-aad3-c299fdd175ac)

<br>
<br>

## Types of objects

Let's give credit to our dear SHA-1 algoritm real quick: <br>
SHA-1 or Secure Hash Algorithm 1 is a cryptographic algorithm which takes an input and produces a 160-bit (20-byte) hash value. This hash value is known as a message digest and this is a core component in the way Git stores, locates, encrypts data. Due to security concerns with SHA-1, Git has been working on transitioning to a more secure hash function (SHA-256)

### What does SHA do for us?
- Object Identification
- Immutability
- Deduplication
- Data Integrity

![image](https://media.github.ibm.com/user/467971/files/aa1e3a44-cc5f-4438-b470-2092455d86ec)
![image](https://media.github.ibm.com/user/467971/files/1f7cddda-e37f-4b3e-a787-02d33f23d10c)

<br>
<br>
#### Why are we saying all this? 
Well, because the names of the objects in Git are all SHA-1 hashes.
You can use the ``git cat-file -t`` command to view the type of each SHA-1. As well, the ``git cat-file -p`` command to view the contents and simple data structure of each object. The ``git cat-file`` command is an underlying core command of Git 
<br>

### Blob Objects <br>
They are used to store the contents of a single file. The file is typically a binary data file that does not contain any other file information, such as the file name and other metadata

### Tree Objects <br>
They are the directory structures of the corresponding file systems. They contain subdirectories (trees), file lists (blobs), file types, and some permission models for data files

Let's see the following example:
<br>
![image](https://media.github.ibm.com/user/467971/files/3d318fc2-f8f8-441b-9b9a-c05474eb6675)
<br>
<br>
Where:
![image](https://media.github.ibm.com/user/467971/files/a4e2614c-0a8e-47f0-b6ad-81adf423dc9e)


### Commit Objects <br>
They are the collection of all the files that are modified currently, and they are similar to the "transactions" that contain a series of operations. A commit object is a snapshot of a collection of modified files. With a commit operation, the modified files will be committed to the local repository. During a versioning process, you can use commit objects to retrieve the contents that are modified each time. These objects are the cornerstone of versioning
<br>
<br>

Now let't run the ``git cat-file -t`` and command 
<br>
<br>
![image](https://media.github.ibm.com/user/467971/files/9a8b5f2d-0d1c-4017-b8f5-69e9e66ce9a6)
<br>
![image](https://media.github.ibm.com/user/467971/files/91047d56-6d67-4b86-b79b-74afc4cd8b3d)
<br>
<br>
<br>

### Tag Objects <br>
A tag is a "fixed branch." Once you have added a tag, the content represented by the tag will be permanently immutable because the tag is only associated with the last commit object in the version library at the time when the tag was added <br>
If you use a branch, the content will continuously change due to continuous commits because the last commit that the branch points to will continuously change. Therefore, the release of general applications or software versions typically uses tags
<br>
Git supports two types of tags: <br>

#### 1. Lightweight

Creation Method: <br>
``git tag tagName`` <br>
When you create a tag with this method, Git will directly point to a commit object instead of creating a real underlying tag object. At this point, the git cat-file -t tagName command will return a commit.
<br>

![image](https://media.github.ibm.com/user/467971/files/7966dd14-8cf5-42bb-a8aa-20e04e846668)
<br>
<br>

#### 2. Annotated <br>
Creation Method:<br>
``git tag -a tagName -m''`` <br>
When you create a tag with this method, Git will create an underlying tag object that contains related commit information and additional information, such as the tagger. At this time, if you run the ``git cat-file -t tagname`` command, a tag will be returned.
<br>

![image](https://media.github.ibm.com/user/467971/files/678016bf-2c40-4a47-846d-40c4f4dbbc79)
<br>
<br>
<br>
![image](https://media.github.ibm.com/user/467971/files/9a60ed23-185d-414f-ad79-40b04c025c83)
<br>
<br>

## Git's uniqueness 
Things that make Git better than other VSC: <br>
- Storage Models                                               
- Indexing
- Retrieval Models                                             
- Query Algorithm
- Pack Files  
<br>

Imagine your project files are lined up on a timeline.
Each time you save a new version, the system records only the changes (deltas) made since the last version.
This is like keeping track of every single change made to each file over time.
Git takes a different approach by treating each version (commit) as a complete snapshot of your entire project.
Instead of recording just the changes, Git saves the state of every file in the project.
However, to save space, if a file hasn't changed between versions, Git doesn't store the file again. It simply points to the already stored file.
<br>
<br>

![image](https://media.github.ibm.com/user/467971/files/c24d701c-8ecf-48a5-b0cf-cd80f7c3e988)











