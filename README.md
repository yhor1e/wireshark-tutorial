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

- [Wireshark によるパケット解析講座 2: 脅威インテリジェンス調査に役立つフィルタリング設定](https://unit42.paloaltonetworks.jp/using-wireshark-display-filter-expressions/)
  - > 表示フィルタの背景色が赤いとき､入力した式はまだそのままでは利用できない状態です。この色が緑に変われば、入力内容は式として利用でき、正しく動作します。表示フィルタの背景色が黄色の場合、式は受け入れられていても、おそらく意図したとおりには動作しません。
  - `==`, `eq`
  - `&&`, `and`
  - `||`, `or`
  - !(ip.addr eq 192.168.10.1)
  - > SSDP(Simple Service Discovery Protocol)が生成しているもので､SSDPはプラグ アンド プレイ デバイス検出に使用されているプロトコル
  - > 一般的なwebトラフィックとは関連しないものなので､表示されてほしくありません｡
    - (http.request or ssl.handshake.type == 1) and !(udp.port eq 1900)
    - (http.request or ssl.handshake.type == 1) and !(ssdp)
  - > 感染したホストが、オフラインのサーバーやTCP接続を拒否するサーバーに接続を試みていた可能性もあるのです。こうした接続試行の様子は、フィルタに「tcp.flags eq 0x0002」を追加してTCP SYNセグメントを含めれば表示することができます。
    - (http.request or ssl.handshake.type == 1 or tcp.flags eq 0x0002) and !(udp.port eq 1900)
  - > 
    - (http.request or ssl.handshake.type == 1 or tcp.flags eq 0x0002 or dns) and !(udp.port eq 1900)
  - DNS で名前解決をしてその後 SYN をしている様子がわかる。
  - ftp フィルタ
    - ログインしている様子、ファイルをダウンロードしている様子がわかる。
  - > Wiresharkの表示フィルタでは大文字と小文字が区別されることに注意してください。
    - smtp contains "From: "
    - > 表示されているフレームのいずれかひとつを選択して右クリックし､表示されたコンテキストメニューで[追跡]､[TCP ストリーム]の順にクリックします｡これでそのフレームに関連するSMTP通信の内容が表示される
  - (http.request or tls.handshake.type == 1) and !(udp.port eq 1900)
    - ssl is deprecated
  - (http.request or tls.handshake.type == 1 or tcp.flags eq 0x0002) and !(udp.port eq 1900)
  - (http.request or tls.handshake.type == 1 or tcp.flags eq 0x0002 or dns) and !(udp.port eq 1900)
- [Wireshark によるパケット解析講座 3: ホストとユーザーを特定する](https://unit42.paloaltonetworks.jp/using-wireshark-identifying-hosts-and-users/)

  
