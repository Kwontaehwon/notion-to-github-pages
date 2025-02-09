---
title: UDP
subtitle: 
categories: 
tags: 
date: 2023-10-10 10:49:42 +0000
last_modified_at: 2023-10-10 10:49:42 +0000
---

> User Datagram Protocol
> 

<aside>
💡 UDP는 Segment가 유실될 수 있고 순서를 보장하지 않는다.

</aside>

## 특징

- No Connection Establishment
    - No handshake → TCP 보다 더 빠르다
- Simple
    - Connection State가 없다.
- Small header size
- No Congestion Control

스트리밍, DNS, HTTP/3, SNMP에서 사용함.

게임서버는 UDP와 TCP를 같이 사용.

만약 UDP를 사용하며 Reliable Transfer가 필요하다면(ex : HTTP/3) Application Layer에서 Congestion Control 등을 직접 개발한다.

## 구조

![Untitled](/assets/images/UDP/Untitled.png)

- dest port # : Demultiplexing 에 사용됨
- **checksum** : Error Detection에 사용
- length : Header + Payload를 모두 포함한 길이

## UDP Checksum

> 데이터가 변형되지 않았는지 확인하는 방법
> 

### Sender

1. IP주소와 UDP header와 데이터(payload)를 16비트 단위로 쪼갠 뒤 모두 더한다.
2. 가장 큰 자리에 Wrap around(올림값)이 있다면 이를 가장 작은 자리에 더해준다.
3. 1의 보수를 취한 뒤 그 값을 checksum 값에 저장한다.

### Receiver

수신한 값으로 Sender가 Checksum을 만들 때 방법으로 값을 구한다.

→ 그 값이 저장된 Checksum 값과 다르다면 오류이다.

### 완벽하지 않음

![Untitled](/assets/images/UDP/Untitled%201.png)

<aside>
💡 **checksum 값이 같아도 오류가 발생할 수 있다.**

</aside>