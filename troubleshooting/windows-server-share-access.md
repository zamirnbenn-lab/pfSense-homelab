# Windows Server Shared Folder Access Issue

## Problem

After moving Windows Server 2025 to 'SERVER-LAN', I tried accessing the 'IT-shared' folder from the Windows 11 client using the new server IP '192.168.20.10'.

The connection returned False when tested with 'Test-Path', even though Windows 11 could reach the server over port 445.

## Resolution

I checked the shared folders on Windows Server using 'Get-SmbShare' and found that 'IT-shared' was missing from the list.

I then checked 'C:\Shares\IT' and confirmed that the folder still existed and that the 'LAB\IT' security group still had Modify permissions.

I recreated the 'IT-shared' network share without changing the existing NTFS permissions.

After recreating the share, I tested access again from Windows 11 using 'Test-Path'.

The IT account was able to access 'IT-shared', while access to 'Marketing-shared' was denied.
