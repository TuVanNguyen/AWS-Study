# OSI Model

### What?
* stands for Open Systems Interconnection (OSI) Model
* conceptual framework which describes function of a network 
* model to enable different apps, computer systems, and networks to communicate to each other[^1]

| Layer | Purpose | Scope |
|-------|---------|-------|
| 7: Application | convert computer-readable network data to user-readable responses and vice versa | what end users see, http, web browsers, email clients (SMTP) |
| 6: Presentation | makes sure data is in usable format | encryption, compression, data translation, ssh | 
| 5: Session | maintains connections and sessions; starts and stops connections between 2 devices on the network |
| 4: Transport | transmit end-to-end data between 2 devices on the network| TCP, UDP |
| 3: Network | logically routing network packets based on IP address, for devices connecting across different networks | IP, DNS lookup |
| 2: Data Link | physically transmit data based on MAC addresses, for devices on the same network |
| 1: Physical | transmit bits and bytes over physical devices | routers, USB cables |

| Subcategories | Layers | Description |
|---------------|--------|-------------|
| Software Layers | 7, 6, 5 | all transmissions are between software apps e.g OS, web browsers, email clients |
| Transport Layer | 4 | handles all data communication between networks and systems |
| Hardware Layers | 3, 2, 1 | data moves through physical components of the network as it's processed |

### Email Example

| Layer | What's happening |
|-------|------------------|
| 7 | User types up an email, then click send button. Application layer sends email to presentation layer via SMTP |
| 6 | email data is compressed and encrypted and sent to session layer |
| 5 | start and maintains an SMTP session and sends data to transport layer |
| 4 | divide data into packets using TCP |
| 3 | encapsulate the packets into IP packets which contain source and destination IP addresses, then route them to email server using IP address |
| 2 | frames each packet with MAC addresses to handle delivery between routers as they make their way to the email server |
| 1 | email becomes electrical signals (cable), light pulses (fiber optic), or radio waves (wifi) to travel from source network infrastructure to destination network infrastructure | 



## Footnotes

[^1]: [https://www.ibm.com/think/topics/osi-model](https://www.ibm.com/think/topics/osi-model)