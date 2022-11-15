## File Sharing Protocol Comparison

### NFS (Network File System)
<ins>Pros:</ins>
<br />
- This protocol is efficient and particularly performant for read and writes of small files. This is most likely due to less overhead on each transaction between client and server. We see this carry on in regards to systems that scan large NFS export directories where the transactional efficiencies add up and provide a tangible difference in mount traversal.

- NFS supports file locking in which the client can choose to "lock" the file so that no other process or client can intercept.

- Easier to setup and uses Linux rights.

<ins>Cons:</ins>
<br />
- The security options are not reliable with its inherently insecure RPC communication. It is best used when all IP's in a local subnet are whitelisted and ensuring the the file share is not accessible over the public network.

- Authentication is only done based on whitelisted IP addresses. This makes it difficult when trying to seperate different users permissions/ access rights on a single machine. 

- Not natively supported on windows, still needs to be manually enabled within windows optional features unlike Samba.

### Samba/CIFS (Common Internet File System)
<ins>Pros:</ins>
<br />
- Better in a full windows enviroment with the use of a domain controller in which client credentials are authorised access.

- User based authorisation. User/Pass combo is required for autorisation and can limit RWX permissions.

- File transfer is known to be secure and reliable.

- Allows for printers to be shared.

<ins>Cons:</ins>
<br />
- Inefficient "chatty" communication between the client and the server. Results in extra overhead dwindling time to transfer for small files and increasing latency.





