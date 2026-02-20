> [!abstract] What is it? **AWS Storage Extra** = services for **hybrid storage**, **offline data transfer**, **managed file systems**, and **data movement** (on‑prem ↔ AWS, AWS ↔ AWS).

## Snow family overview

**Snow Family** is for moving data when the network is too slow/expensive/unreliable—or when you need edge compute.

- **Snowcone:** Smallest, portable, limited storage + optional compute (edge/field work).
- **Snowball Edge:** Rugged device for TB–PB transfer; can run **EC2 instances / Lambda** at the edge.
- **Snowmobile:** Exabyte-scale transfer in a shipping container (rare, extreme cases).

## Snowball into Glacier architecture

**Goal:** Offline ingest → land in S3 → transition to Glacier for long-term archive.

- **Step 1:** Copy data to **Snowball Edge** on-prem.
- **Step 2:** Ship device to AWS; AWS imports into an **S3 bucket**.
- **Step 3:** Use **S3 Lifecycle rules** to transition objects:
    - **S3 Standard/IA → Glacier Instant/Flexible/Deep Archive** (based on retrieval needs/cost).
- **Key point:** Snowball imports into **S3**, not directly into Glacier—Glacier is reached via **lifecycle transitions**.

## Amazon FSx

**FSx** = fully managed file systems (when you need shared file storage semantics, not object storage).

- **FSx for Windows File Server:** SMB, AD integration, Windows workloads, home directories, lift-and-shift.
- **FSx for Lustre:** High-performance HPC (throughput/IOPS), common for compute + large datasets.
- **FSx for NetApp ONTAP:** NFS/SMB/iSCSI, snapshots/clones, enterprise NAS features.
- **FSx for OpenZFS:** NFS, low-latency, ZFS features (snapshots/clones), Linux/Unix workloads.

> [!note] SAA mental model **EFS** = serverless NFS for Linux.  
> **FSx** = “pick the file system you actually need” (Windows SMB, HPC, ONTAP, ZFS).

## AWS Storage Gateway overview

**Storage Gateway** connects on‑prem apps to AWS storage using a gateway VM/appliance.

- **File Gateway:** Presents **NFS/SMB** on-prem, stores objects in **S3** (with local cache).
- **Volume Gateway:** Presents **iSCSI block volumes** to on‑prem servers.
    - **Cached volumes:** Primary in S3, hot data cached locally.
    - **Stored volumes:** Primary on-prem, async backups to AWS.
- **Tape Gateway:** Virtual tape library for backup apps; stores in S3 and archives to Glacier.

> [!tip] When to use Keep legacy apps/protocols on-prem while using **S3/Glacier** as the durable backend.

## AWS Transfer Family

Managed file transfer **into/out of S3 or EFS** using standard protocols.

- **Protocols:** SFTP, FTPS, FTP
- **Targets:** S3 or EFS
- **Use case:** Partners/vendors/users upload via SFTP → lands directly in S3 (no custom server to manage).

## DataSync overview

**DataSync** = online, automated data transfer service for large-scale moves.

- **Moves data between:** on‑prem ↔ S3/EFS/FSx, and AWS ↔ AWS.
- **Optimized transfer:** parallelism, incremental syncs, scheduling, bandwidth control.
- **Use cases:** migrations, recurring syncs, DR replication, moving NAS data into AWS.

## Storage options comparison

- **S3:** Object storage (durable, cheap, massive scale) — not POSIX file semantics.
- **EFS:** Managed NFS for Linux, shared file system, elastic.
- **FSx:** Managed “specific” file systems (Windows SMB, HPC Lustre, ONTAP, ZFS).
- **Storage Gateway:** Hybrid access (on‑prem protocols backed by AWS storage).
- **Transfer Family:** Managed SFTP/FTPS/FTP endpoints to S3/EFS.
- **DataSync:** High-speed online transfer + scheduled/incremental sync.

<span style="float:left">← [[AWS Global Accelerator]]</span><span style="float:right">[[SQS]] →</span>