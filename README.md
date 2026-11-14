# Cloud Folder SDK (EaseFilter Cloud File System)

[![Platform](https://img.shields.io/badge/Platform-Windows-blue.svg)]()
[![Language](https://img.shields.io/badge/Language-C%23%20%7C%20C++%20%7C%20Python%20%7C%20Rust%20%7C%20Java-success.svg)]()
[![License](https://img.shields.io/badge/License-Commercial-orange.svg)]()

The **EaseFilter Cloud File System SDK** enables developers to build seamless cloud folder solutions that bridge the gap between traditional local file systems and infinite cloud storage. By mounting a cloud storage bucket (Amazon S3, Azure Blob, Google Cloud Storage) directly to a local Windows folder, your legacy applications can interact with the cloud exactly as if it were a physical local drive.

![EaseFilter Cloud File System Architecture](https://www.easefilter.com/images/cloud-folder-architecture.jpg)

## 🚀 Key Features

* **Zero-API Integration:** Applications do not need to be rewritten to use REST APIs or specialized cloud SDKs. They continue using standard Windows APIs (`CreateFile`, `ReadFile`, `WriteFile`) seamlessly.

* **Transparent Access:** To the Windows OS, end-users, and applications, the mounted cloud bucket functions exactly like a standard NTFS directory.

* **On-Demand Fetching:** Files are downloaded only when explicitly requested. This saves local disk space and minimizes bandwidth consumption while providing the illusion of massive local storage capacity.

* **Simultaneous Hybrid Access:** Data can be mirrored between the local cache and the cloud repository, allowing continuous synchronization and instant disaster recovery failover.

## 🏗 Architecture

Developing a custom virtual file system from scratch traditionally requires writing a complex Windows kernel-mode driver and navigating I/O Request Packets (IRPs). This SDK abstracts that complexity into two core components communicating together:

| Component | Role | Description | 
| ----- | ----- | ----- | 
| **Kernel-Mode Driver** (`CloudFile.sys`) | System Interception | Intercepts standard file I/O requests at the operating system level, immediately before they reach the local physical file system. | 
| **User-Mode API** (`FilterAPI.dll`) | Configuration & Control | A lightweight library that allows developers to control the kernel driver and define routing/filtering rules using standard programming languages like C#, C++, and C. | 

Because the SDK handles all kernel-level heavy lifting and Microsoft Filter Manager integration, development teams can build enterprise-grade cloud storage solutions entirely in user space.

## 💡 Enterprise Use Cases

* **Painless Infrastructure Migration:** Migrate enterprise data to the cloud without altering application paths or experiencing major downtime. Operations continue mapping to the exact same drive letters, unaware that the data now lives in a remote data center.

* **Hybrid Cloud Gateways:** Keep frequently accessed, latency-sensitive files pinned locally, while pushing cold, archival data to the cloud in the background.

* **Automated Disaster Recovery:** Protect against localized hardware failure, server room outages, or ransomware. With data instantly syncing to the cloud, backup servers can instantly mount the remote folder and resume operations without data loss.

## ☁️ Cloud Folder with Amazon S3

The SDK provides native support for mapping **Amazon S3** buckets directly to local directories, transforming object storage into a fully functional local cloud folder with zero configuration change.

### 🔗 Mapping Amazon S3 to a Local Cloud Folder
Through the SDK, you can map your secure Amazon S3 buckets directly to standard Windows file paths (e.g., `P:\S3CloudFolder`). This completely translates complex Object Storage concepts (buckets, prefixes) into familiar File and Directory structures:
* **Mounting Buckets:** Configure your target bucket with read/write credentials (AWS IAM Keys, Role ARN, or instance profile) to register a standard Windows directory path.
* **On-Demand Hydration:** File listing metadata is fetched instantly, showing large S3 buckets as immediately accessible folders. The content downloads only when a process opens a specific file.
* **Automatic Caching:** Frequently accessed datasets, configurations, or in-use binaries are cached locally, optimizing access times while reducing data retrieval overhead.

### ✨ Seamless S3 Access without APIs
* **Zero API Rework:** Legacy software does not require integration with AWS SDKs or S3-specific REST endpoints. Everything uses standard File I/O.
* **Traditional Windows Operability:** Users and systems can search, edit, back up, or analyze files using local Windows interfaces, scripts (`Powershell`, `CMD`), and native client apps.
* **Multipart Cloud Streaming:** Heavy write operations, data output, or changes locally are seamlessly split and streamed as objects right back into S3 bucket storage without stalling user experiences.

---

## 🏗️ Cloud-Based Disaster Recovery
Cloud-based Disaster Recovery (Cloud DR) takes a very different approach for disaster recovery based on virtualization. EaseFilter Cloud File System automatically integrates the cloud storage into the on-premies storage, it can deliver a fully functional virtual infrastructure ready to take over an outage disrupt primary services. The virtual file is stored in an offsite public cloud where it remains in standby ready for failover. Data synchronization operates in the background to keep data up-to-date. The entire system can be spun up in minutes, saving the organization from costly service interruption.

![Cloud File FOLDER](https://www.easefilter.com/images/cloudFolder.png)

**Active-Active Cluster system.** With the [Cloud File System SDK](https://www.easefilter.com/cloud/cloud-file-system-sdk.htm), you can set up two or more active systems, which the virtual files can be accessed from all the active systems, it can distribute your load balance and support the automated fail over without your interference.

**Zero downtime for the disaster recovery.** With the Cloud File DR solution, in the event of a disaster, you can automatically fail over the local storage to the cloud storage if disaster strikes,you can quickly launch resources to ensure your business continuity. You can leverage for your disaster recovery (DR) processes to significantly minimize the impact on your data, your system, and your overall business operations, your business won't be interrupted. Retrieve back the files from cloud storage is very fast, only the applications requested data will be downloaded.

## EaseFilter File System Filter Driver SDK Reference
| Product Name | Description |
| --- | --- |
| [Cloud File System SDK](https://www.easefilter.com/cloud/cloud-file-system-sdk.htm) | EaseFilter Cloud File System SDK Introduction. |
| [CloudTier Storage Tiering SDK](https://www.easefilter.com/cloud/storage-tiering-sdk.htm) | EaseFilter Storage Tiering Filter Driver SDK Introduction. |
| [File Monitor SDK](https://www.easefilter.com/kb/file-monitor-filter-driver-sdk.htm) | EaseFilter File Monitor Filter Driver SDK Introduction. |
| [File Control SDK](https://www.easefilter.com/kb/file-control-file-security-sdk.htm) | EaseFilter File Control Filter Driver SDK Introduction. |
| [File Encryption SDK](https://www.easefilter.com/kb/transparent-file-encryption-filter-driver-sdk.htm) | EaseFilter Transparent File Encryption Filter Driver SDK Introduction. |
| [Registry Filter SDK](https://www.easefilter.com/kb/registry-filter-drive-sdk.htm) | EaseFilter Registry Filter Driver SDK Introduction. |
| [Process Filter SDK](https://www.easefilter.com/kb/process-filter-driver-sdk.htm) | EaseFilter Process Filter Driver SDK Introduction. |
| [EaseFilter SDK Programming](https://www.easefilter.com/kb/programming.htm) | EaseFilter Filter Driver SDK Programming. |

## EaseFilter SDK Sample Projects
| Sample Project | Description |
| --- | --- |
| [CloudTier Storage Tiering Demo](https://www.easefilter.com/cloud/cloudtier-storage-tiering-demo.htm) | A HSM File System Filter Driver Demo. |
| [CloudTier S3 Tiering Demo](https://www.easefilter.com/cloud/cloudtier-s3-intelligent-tiering-demo.htm) | CloudTier S3 Intelligent Tiering Demo. |
| [Cloud File DR S3 Demo](https://www.easefilter.com/cloud/cloud-file-dr-demo.htm) | Cloud File DR S3 Demo. |
| [Amazon S3 File Explorer Demo](https://www.easefilter.com/cloud/s3-browser-demo.htm) | Amazon S3 File Explorer Demo. |
| [Auto File DRM Encryption](https://www.easefilter.com/kb/auto-file-drm-encryption-tool.htm) | Auto file encryption with DRM data embedded. |
| [Transparent File Encrypt](https://www.easefilter.com/kb/AutoFileEncryption.htm) | Transparent on access file encryption. |
| [Secure File Sharing with DRM](https://www.easefilter.com/kb/DRM_Secure_File_Sharing.htm) | Secure encrypted file sharing with digital rights management. |
| [File Monitor Example](https://www.easefilter.com/kb/file-monitor-demo.htm) | Monitor file system I/O in real time, tracking file changes. |
| [File Protector Example](https://www.easefilter.com/kb/file-protector-demo.htm) | Prevent sensitive files from being accessed by unauthorized users or processes. |
| [FolderLocker Example](https://www.easefilter.com/kb/FolderLocker.htm) | Lock file automatically in a FolderLocker. |
| [Process Monitor](https://www.easefilter.com/kb/Process-Monitor.htm) | Monitor the process creation and termination, block unauthorized process running. |
| [Registry Monitor](https://www.easefilter.com/kb/RegMon.htm) | Monitor the Registry activities, block the modification of the Registry keys. |
| [Secure Sandbox Example](https://www.easefilter.com/kb/Secure-Sandbox.htm) |A secure sandbox example, block the processes accessing the files out of the box. |
| [FileSystemWatcher Example](https://www.easefilter.com/kb/FileSystemWatcher.htm) | File system watcher, logging the file I/O events. |
| [ZeroTrust Example](https://www.easefilter.com/kb/zero-trust-file-access-control-demo.htm) | Zero trust file access control with encryption feature. |

## Filter Driver Reference

* [Understand MiniFilter Driver](https://www.easefilter.com/kb/understand-minifilter.htm)
* [Understand File I/O](https://www.easefilter.com/kb/File_IO.htm)
* [Understand I/O Request Packets(IRPs)](https://www.easefilter.com/kb/understand-irps.htm)
* [Filter Driver Developer Guide](https://www.easefilter.com/kb/DeveloperGuide.htm)
* [MiniFilter Filter Driver Framework](https://www.easefilter.com/kb/minifilter-framework.htm)
* [Isolation Filter Driver](https://www.easefilter.com/kb/Isolation_Filter_Driver.htm)

## License

This repository contains two distinct licensing categories:

1. **Wrapper/Implementation Code (MIT License):** 
   The source code, scripts, and configuration files provided directly in this repository are licensed under the [MIT License](LICENSE). You are free to modify, distribute, and use this specific integration code.

2. **EaseFilter SDK (Commercial License):**
   This project requires the EaseFilter SDK (including its binaries, filter drivers, and core libraries) to function. The EaseFilter SDK is **proprietary commercial software** and is strictly excluded from the MIT License.   
   To use the EaseFilter SDK for commercial purposes or in a production environment, you must obtain a valid commercial license directly from [EaseFilter](https://www.easefilter.com/license.pdf).

## Support
If you have questions or need help, please contact support@easefilter.com 

[Home](https://www.easefilter.com/) | [Solution](https://www.easefilter.com/solutions.htm) | [Download](https://www.easefilter.com/download.htm) | [Demos](https://www.easefilter.com/online-fileio-test.aspx) | [Blog](https://blog.easefilter.com/) | [Programming](https://www.easefilter.com/kb/programming.htm)



