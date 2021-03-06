---
title: Fsutil behavior
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: "IT Pro"
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b

---
# Fsutil behavior

>Applies To: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Queries or sets NTFS volume behavior, which includes:

-   The creation of 8.3 character-length file names

-   Extended character use in 8.3 character-length short file names on NTFS volumes

-   The updating of the Last Access Time stamp when directories are listed on NTFS volumes

-   The frequency with which quota events are written to the system log and to NTFS paged pool and NTFS non-paged pool memory cache levels

-   The size of the master file table zone (MFT Zone)

-   Silent deletion of data when the system encounters corruption on an NTFS volume.

-   File-delete notification (also known as trim or unmap)

For examples of how to use this command, see [Examples](#BKMK_examples).

## Syntax

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<VolumePath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <Value> | [<VolumePath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <Frequency> | symlinkevaluation <SymbolicLinkType> | disabledeletenotify {1|0}}
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|query|Queries the file system behavior parameters.|
|set|Changes the file system behavior parameters.|
|allowextchar {1&#124;0}|Allows (**1**) or disallows (**0**) characters from the extended character set (including diacritic characters) to be used in 8.3 character-length short file names on NTFS volumes.<br /><br />You must restart your computer for this parameter to take effect.|
|Bugcheckoncorrupt {1&#124;0}|Allows (**1**) or disallows (**0**) generation of a bug check when there is corruption on an NTFS volume. This feature can be used to prevent NTFS from silently deleting data when used with the Self-Healing NTFS feature.<br /><br />You must restart your computer for this parameter to take effect.<br /><br />This parameter applies to:  Windows Server 2008 R2  and  Windows 7 .|
|disable8dot3 [<VolumePath>] {1&#124;0}|Disables (**1**) or enables (**0**) the creation of 8.3 character-length file names on FAT- and NTFS-formatted volumes. Optionally, prefix with the *VolumePath* specified as a drive name followed by a colon or GUID.|
|disablecompression {1&#124;0}|Disables **(1)** or enables **(0)** NTFS compression.<br /><br />You must restart your computer for this parameter to take effect.|
|disablecompressionlimit {1&#124;0}| Disables **(1)** or enables **(0)** NTFS compression limit on NTFS volume. When a compressed file reaches a certain level of fragmentation, rather than failing to extend the file, NTFS stops compressing additional extents of the file. This was done to allow compressed files to be larger than they normally would be. Setting this value to TRUE disables this feature which limits the size of compressed files on the system. We do not recommend disabling this feature.<br /><br />You must restart your computer for this parameter to take effect.|
|disableencryption {1&#124;0}|Disables **(1)** or enables **(0)** the encryption of folders and files on NTFS volumes.<br /><br />You must restart your computer for this parameter to take effect.|
|disablefilemetadataoptimization {1&#124;0}|Disables **(1)** or enables **(0)** file metadata optimization. NTFS has a limit on how many extents a given file can have. Compressed and spares files can become very fragmented. By default, NTFS periodically compacts its internal metadata structures to allow for more fragmented files. Setting this value to TRUE disables this internal optimization. We do not recommend disabling this feature.<br /><br />You must restart your computer for this parameter to take effect.|
|disablelastaccess {1&#124;0}|Disables (**1**) or enables (**0**) updates to the Last Access Time stamp on each directory when directories are listed on an NTFS volume.<br /><br />You must restart your computer for this parameter to take effect.|
|disablespotcorruptionhandling {1&#124;0}|Disables **(1)** or enables **(0)** spot corruption handling. One of the new features introduced in Windows 8 and Windows Server 2012 is a new high availability form of CHKDSK. This feature allows system administrators to run CHKDSK to analyze the state of a volume without taking it offline. We do not recommend disabling this feature.<br /><br />You must restart your computer for this parameter to take effect.|
|disabletxf {1&#124;0}|Disables **(1)** or enables **(0)** txf on the specified NTFS volume. TxF is an NTFS feature that provides transaction like semantics to file system operations. TxF is presently deprected though the functionality is still available. We do not recommend disabling this feature on the C: volume.<br /><br />You must restart your computer for this parameter to take effect.|
|disablewriteautotiering {1&#124;0}|Disables ReFS v2 auto tiering logic for tiered volumes.<br /><br />You must restart your computer for this parameter to take effect.|
|encryptpagingfile {1&#124;0}|Encrypts (**1**) or does not encrypt (**0**) the memory paging file in the Windows operating system.<br /><br />You must restart your computer for this parameter to take effect.|
|mftzone <Value>|Sets the size of the MFT Zone, and is expressed as a multiple of 200MB units. Set *Value* to a number from **1** (default is 200 MB) to **4** (maximum is 800 MB).<br /><br />You must restart your computer for this parameter to take effect.|
|memoryusage <Value>|Configures the internal cache levels of NTFS paged-pool memory and NTFS nonpaged-pool memory. Set to **1** or **2**. When set to **1** (the default), NTFS uses the default amount of paged-pool memory. When set to **2**, NTFS increases the size of its lookaside lists and memory thresholds. (A lookaside list is a pool of fixed-size memory buffers that the kernel and device drivers create as private memory caches for file system operations, such as reading a file.)<br /><br />You must restart your computer for this parameter to take effect.|
|quotanotify <Frequency>|Configures how frequently NTFS quota violations are reported in the system log. Valid values for are in the range 0 – 4294967295. The default frequency is 3600 seconds (one hour).<br /><br />You must restart your computer for this parameter to take effect.|
|symlinkevaluation <SymbolicLinkType>|Controls the kind of symbolic links that can be created on a computer. Valid choices are:<br /><br />1.  Local to local symbolic links, L2L:{0&#124;1}<br />2.  Local to remote symbolic links, L2R:{0&#124;1}<br />3.  Remote to local symbolic links, R2R:{0&#124;1}<br />4.  Remote to remote symbolic links, R2L:{0&#124;1}|
|DisableDeleteNotify|Disables \(**1**\) or enables \(**0**\) delete notifications. Delete notification \(also known as trim or unmap\) is a feature that notifies the underlying storage device of clusters that have been freed due to a file delete operation. In addition:<br /><br />-   For systems using ReFS v2, trim is disabled by default. Applies to Windows Server 2016.<br />-	For systems using ReFS v1, trim is enabled by default. Applies to Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.<br />-	For systems using NTFS, trim is enabled by default unless an administrator disables it.<br />-	If your hard disk drive or SAN reports that it does not support trim, then your hard disk drive and SANs do not get trim notifications.<br />-   Enabling or disabling does not require a restart.<br />-   Trim is effective when the next unmap command is issued.<br />-   Existing inflight IO are not impacted by the registry change.<br />-   Does not require any service restart when you enable or disable trim.<br /><br />This parameter was introduced in Windows Server 2008 R2 and Windows 7. | 

## Remarks

-   The MFT Zone is a reserved area that enables the master file table (MFT) to expand as needed to prevent MFT fragmentation. If the average file size on the volume is 2 KB or less, it can be beneficial to set the **mftzone** value to 2. If the average file size on the volume is 1 KB or less, it can be beneficial to set the **mftzone** value to 4.

-   When **disable8dot3** is set to **0**, every time you create a file with a long file name, NTFS creates a second file entry that has an 8.3 character-length file name. When NTFS creates files in a directory, it must look up the 8.3 character-length file names that are associated with the long file names. This parameter updates the **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** registry key.

-   The **allowextchar** parameter updates the **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** registry key.

-   The **disablelastaccess** parameter reduces the impact of logging updates to the Last Access Time stamp on files and directories. Disabling the **Last Access Time** feature improves the speed of file and directory access. This parameter updates the **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** registry key.

    Notes:

    -   File-based **Last Access Time** queries are accurate even if all on-disk values are not current. NTFS returns the correct value on queries because the accurate value is stored in memory.

    -   One hour is the maximum amount of time that NTFS defers updating **Last Access Time** on disk. If NTFS updates other file attributes such as **Last Modify Time**, and a **Last Access Time** update is pending, NTFS updates **Last Access Time** with the other updates without additional performance impact.

    -   The **disablelastaccess** parameter can affect programs such as Backup and Remote Storage that rely on this feature.

-   Increasing physical memory does not always increase the amount of paged pool memory available to NTFS. Setting **memoryusage** to **2** raises the limit of paged pool memory. This might improve performance if your system is opening and closing many files in the same file set and is not already using large amounts of system memory for other applications or for cache memory. If your computer is already using large amounts of system memory for other applications or for cache memory, increasing the limit of NTFS paged and non-paged pool memory reduces the available pool memory for other processes. This might reduce overall system performance. This parameter updates the **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** registry key.

-   The value specified in the **mftzone** parameter is an approximation of the initial size of the MFT plus the MFT Zone on a new volume, and it is set at mount time for each file system. As space on the volume is used, NTFS adjusts the space reserved for future MFT growth. If the MFT Zone is already large, the full MFT Zone size is not reserved again. Because the MFT Zone is based on the contiguous range past the end of the MFT, it shrinks as the space is used.

    The file system does not determine the new MFT Zone location until the current MFT Zone is completely used. Note that this never occurs on a typical system.

-   Some devices may experience performance degradation when the delete notification feature is turned on. In this case, use the **disabledeletenotify** option to turn off the notification feature.

### <a name="BKMK_examples"></a>Examples
To query for the disable 8dot3 name behavior for a disk volume specified with the GUID, {928842df-5a01-11de-a85c-806e6f6e6963}, type:

```
fsutil behavior query disable8dot3 Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

You can also query the 8dot3 name behavior by using the **8dot3name** subcommand.

To query the system to see if TRIM is enabled or not, type:

```
fsutil behavior query DisableDeleteNotify
```
This yields an output similar to this:

    NTFS DisableDeleteNotify = 1
    ReFS DisableDeleteNotify is not currently set

To override the default behavior for TRIM \(disabledeletenotify\) for ReFS v2, type:

```
fsutil behavior set DisableDeleteNotify ReFS 0
```

To override the default behavior for TRIM \(disabledeletenotify\) for NTFS and ReFS v1, type:
```
fsutil behavior set DisableDeleteNotify 1
```

#### Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Fsutil 8dot3name](Fsutil-8dot3name.md)


