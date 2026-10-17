# CMPG325-2026-145-41865073
Amohelang Electronics Repairs and Sales - Network Project

## Student
Thabiso Tharaka - 41865073

## Phase 1 Files
- IP addressing plan.pdf
- cmpg 325 client requirements.pdf
- Amohelang Electronics Repairs and Sales physical...

## Phase 2 Final Submission

- cmpg325-2026-pkt.pkt - Final Packet Tracer file (write memory done, tested with ping after reopen)
- router0-config.txt - Router running-config
- switch0-config.txt - Switch running-config
- [testing evidence.pdf](testing%20evidence.pdf) - Screenshots and explanations of the DHCP tests

## Assigned Feature: DHCP

Router0 is the DHCP server, with one scoped pool per VLAN on 192.168.61.0/24:

| VLAN | Department | Pool | Network | Gateway |
|------|------------|------|---------|---------|
| 10 | Sales | SALES | 192.168.61.0/26 | 192.168.61.1 |
| 20 | Repairs | REPAIRS | 192.168.61.64/26 | 192.168.61.65 |
| 30 | Admin | ADMIN | 192.168.61.128/26 | 192.168.61.129 |
| 50 | Shared printer zone | PRINTER_ZONE | 192.168.61.224/27 | static printer 192.168.61.231 |

Inter-VLAN routing uses Router-on-a-Stick. ACL ADMIN_NO_PRINTER_ZONE keeps the Admin VLAN out of the printer zone, while Sales and Repairs can print (change request CR8).

## How to test

1. Open cmpg325-2026-pkt.pkt in Packet Tracer
2. Open sales-PC1 -> Desktop -> Command Prompt
3. Run ipconfig /all - should show an address in 192.168.61.0/26 from DHCP server 192.168.61.1
4. ping 192.168.61.67 - should get Reply (Sales to Repairs)
5. ping 192.168.61.231 - should get Reply (Sales to shared printer)
6. On Admin-PC1, ping 192.168.61.231 - should be blocked (ACL)
