# wireshark-tutorial

- [Wireshark によるパケット解析講座 1: Wiresharkの表示列をカスタマイズする](https://unit42.paloaltonetworks.jp/unit42-customizing-wireshark-changing-column-display/)
  - Column Preferences > Source Port: Src port (unresolved) 
  - Column Preferences > Destination Port: Dest port (unresolved)  
  - Align Left
  - View > Time Display Format > UTC Date and Time of Day 
  - View > Time Display Format > Seconds
  - http.request フィルタ
    - Hypertext Transfer Protocol > Host を右クリック Apply as Column
  - ssl.handshake.type == 1 フィルタ
    - Secure Sockets Layer もしくは Transport Layer Security > Handshake Protocol: Client Hello > Extension: server_name > Server Name Indication extension > Server Name > Server Name: を右クリック Apply as Column
  - http.request or ssl.handshake.type == 1 フィルタ
