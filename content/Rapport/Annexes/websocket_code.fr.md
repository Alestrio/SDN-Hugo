---
title: "2. Code mises à jour automatique"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

```py
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.bind(('', 514))

async def listen(websocket, path):
    print("Start listening..")
    REGEX = # regex pour conertir le log en évenement
    while True:
        print('listening...')
        data = s.recv(4048)
        data = data.decode('utf-8')
        print(data)
        matches = re.search(REGEX, data)
        if matches:
            ...
            await websocket.broadcast(json.dumps(onu_info))
            #server.send_message_to_all(json.dumps(onu_info))
        else:
            await websocket.broadcast(json.dumps({"message": "No matches found"}))


async def main():
    print("Running.")
    async with websockets.serve("0.0.0.0", 6969):
        await asyncio.Future()  # run forever

asyncio.run(main())
asyncio.run(listen())
```

Code réalisé en collaboration avec le groupe de projet AC-Vision.