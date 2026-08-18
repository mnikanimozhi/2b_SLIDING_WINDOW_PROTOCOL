# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

## server2b.py:
```
import socket

s = socket.socket()

s.bind(('localhost', 8000))
s.listen(1)

print("Waiting for connection...")

conn, addr = s.accept()
print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data
    conn.send(ack.encode())

conn.close()
s.close()
```

## client2b.py:
```
import socket

s = socket.socket()

s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = list(range(1, n + 1))

i = 0

while i < n:
    send_frames = frames[i:i + w]

    msg = " ".join(map(str, send_frames))

    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()

    print("Received:", ack)

    i += w

s.close()
```

## OUPUT
## server2b.py

<img width="1190" height="146" alt="Screenshot 2026-08-18 142142" src="https://github.com/user-attachments/assets/3c8521f7-c2c5-4187-a018-5c74a3791572" />

## client2b.py

<img width="565" height="157" alt="Screenshot 2026-08-18 142126" src="https://github.com/user-attachments/assets/df5c406d-8ce4-4149-b940-f902e40571d1" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
