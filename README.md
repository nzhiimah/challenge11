# Challenge 11 : SMB NSE Enumeration

### Objective :
- To enumerate SMB information and discover user accounts using Nmap NSE scripts.

### Target Information :
| Item      | Value          |
| --------- | -------------- |
| Target IP | 192.168.83.129 |
| Service   | SMB            |
| Port      | 445            |

### Tools Used :
- Nmap
- NSE Script (smb-enum-users)

### Steps:
1. Verify SMB Port

Command :
```
nmap -p 139,445 192.168.83.129
```

Result :
<img width="643" height="261" alt="Screenshot 2026-05-09 232941" src="https://github.com/user-attachments/assets/458c7e08-382c-40ee-a230-7eed10693bba" />
<br>

Explanation :
- Port 445 was open.
- Indicates SMB service is running on the target machine.
---
2. SMB OS Discovery

Command :
```
nmap --script smb-os-discovery -p445 192.168.83.129
```
Result :
<img width="643" height="335" alt="Screenshot 2026-05-09 233021" src="https://github.com/user-attachments/assets/3432db5b-76d7-4c03-996f-bb183fbaf4f8" />
<br>

Findings :
| Information | Details |
|---|---|
| Operating System | Unix/Linux |
| SMB Software | Samba 3.0.20 |
| Computer Name | metasploitable |
| Service | SMB |

Explanation :
- The SMB OS Discovery script identified the operating system and SMB software running on the target machine.
- This information helps attackers understand the target environment before attempting further attacks.

---
3. Enumerate SMB Users

Command :
```
nmap --script smb-enum-users -p445 192.168.83.129
```
<img width="573" height="169" alt="Screenshot 2026-05-09 233321" src="https://github.com/user-attachments/assets/65a6f4d8-ec3b-4b15-b545-ae43bdc01e55" />

<br>

<img width="631" height="567" alt="Screenshot 2026-05-09 234204" src="https://github.com/user-attachments/assets/c55d1d26-65c4-4045-b407-d83e3cfd3cc4" />
<img width="540" height="553" alt="Screenshot 2026-05-09 234249" src="https://github.com/user-attachments/assets/b7e280e9-b20f-4c4e-85e9-ad8d1b4d342c" />
<img width="558" height="505" alt="Screenshot 2026-05-09 234307" src="https://github.com/user-attachments/assets/06208074-c849-4070-a127-bfc219c617a5" />
<br>

Result Summary :
| Username | Status   | Notes                         |
| -------- | -------- | ----------------------------- |
| msfadmin | Active   | Normal user account           |
| user     | Active   | Normal user account           |
| root     | Disabled | System administrator account  |
| mysql    | Disabled | MySQL service account         |
| postgres | Disabled | PostgreSQL administrator      |
| tomcat55 | Disabled | Apache Tomcat service account |

Findings :
- Multiple user accounts were successfully enumerated through SMB.
- Service accounts and administrator-related accounts were exposed.

Conclusion :
SMB enumeration successfully identified several user accounts and service-related accounts on the target machine.
