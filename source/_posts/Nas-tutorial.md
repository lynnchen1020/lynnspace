---
title: Nas-tutorial
date: 2017-08-11 12:10:40
tags: Nas
category: Nas
---

# 外部網路要連進家中 Nas 狀況說明

[基礎說明]
Local Area Network,LAN：區域網路，就是家裡的網路  
Wide Area Network,WAN：廣域網路，就是外面的網路  
Private IP：也常被叫做LAN IP，就是私人IP，諸如192.168.xx.xx,10.0.xx.xx  
Public IP：也常被叫做WAN IP，就是公共IP，例如168.95.1.1  
Port：通訊埠，電腦連線時的通訊窗口，又分為TCP與UDP兩大類。  
<來源: https://www.mobile01.com/topicdetail.php?f=494&t=3758595>

- Nas 連分享器狀態下該怎麼做?
  外部網路要取得 Nas 資料時，分享器會轉發至 Nas 被分配的內部IP，所以需要先透過分享器設定配給 Nas 的 內部虛擬IP 以及要轉接到的 port。
  當你輸入網址時，分享器會將你導至 Nas 被設定的 內部虛擬IP 及 port

- 社區網路的狀況(例如:今網, 群健等)
  由於社區網路的服務就是業者跟中華電信租用網路，再將這個網路用像是分享器的方式，分配給底下申請業者網路服務的用戶，如下列連接圖示意：  
  (中華電信 - 業者分享器 - 家中分享器 - Nas)
  等於連兩次分享器才連接到 Nas, 如果要架站，必須請業者分享器開 port, 家中分享器也要開 port，再去 Nas 設定，請業者開 port 機率低，所以要架站還是直接向電信業者申請獨立的網路吧 (囧)