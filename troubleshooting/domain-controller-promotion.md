# Domain Controller Promotion Issue

## Problem

While promoting Windows Server 2025 to a domain controller, the prerequisites check failed because the built-in Administrator account did not have a password set.

## Resolution

I opened Command Prompt as administrator and set a password for the built-in Administrator account using:

net user Administrator 'password'

After setting the password, I reran the prerequisites check and was able to continue the domain controller promotion.
