# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### Server Program:
```
import socket

s = socket.socket()
s.bind(("localhost", 8000))
s.listen(1)

print("Server waiting for client...")

c, addr = s.accept()
print("Client connected!")

while True:
    data = c.recv(1024).decode()

    if data == "exit":
        break

    print("Received:", data)

    c.send("ACK".encode())
    print("ACK sent")

c.close()
s.close()
```
### Client Program:
```

import socket

s = socket.socket()
s.connect(("localhost", 8000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = []

for i in range(n):
    data = input("Enter data for frame " + str(i + 1) + ": ")
    frames.append(data)

i = 0

while i < n:
    print("\nSending frames:")

    for j in range(i, min(i + w, n)):
        print("Sending:", frames[j])
        s.send(frames[j].encode())

        ack = s.recv(1024).decode()
        print("Received:", ack)

    i = i + w

s.send("exit".encode())
s.close()

```
## OUPUT:
<img width="1907" height="1020" alt="Screenshot 2026-11-02 141445" src="https://github.com/user-attachments/assets/401a2417-7706-4213-a75a-ecd67edbb3ae" />

<img width="941" height="597" alt="Screenshot 2026-11-02 141513" src="https://github.com/user-attachments/assets/58f4b327-fb66-45a6-aeb4-65be7cf3c01c" />



## RESULT:
Thus, python program to perform stop and wait protocol was successfully executed
