---
title:  "python batch 작업 asyncio로 성능개선시키기"
search: false
categories: 
  - Python
  - asyncio
last_modified_at: 2018-08-06T01:00:00+09:00
---

# Asyncio로 Batch작업 성능 개선 시키기

### 배치작업을 처리하는데 시간이 지연됨
-> aws sqs쪽으로 data를 쌓는 시간이 오래 걸리는 거였음
-> 비동기 처리로 후딱 끝내버리면 좋겠다!

### 먼저 나의 거대한 메세지를 담아줄 그릇이 되는가 자네 sqs?$$
-> 저희 메시지는 순서가 보장될 필요가 없기 때문에 standard queue로 되어 있군요. 어차피 조금만 쓰다가 안쓸 녀석인데 대충 읽고 넘어가겠습니다.
-> 오 Unlimited랍니다.. (씨익) 괜히 걱정되는 마음에 적은 TPS로 시작해서 조금씩 올려가며 괴롭혀 보도록 하겠습니다.  이친구랑 놀 날도 얼마 남았지 않았기 때문에 최대한 즐기다가 가야하지 않겠습니까(?)

### request를 asyncio로 보내고 싶었지만..
-> aws boto library는 비동기를 지원하는 라이브러리가 아닙니다.