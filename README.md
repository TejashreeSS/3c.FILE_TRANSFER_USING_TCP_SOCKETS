# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
### Server
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)

print("Server listening...")

while True:
    conn, addr = s.accept()
    print("Connected by", addr)

    data = conn.recv(1024)
    print('Server received:', repr(data))

    filename = 'mytext.txt'  # file to send
    f = open(filename, 'rb')
    l = f.read(1024)
    while l:
        conn.send(l)
        print('Sent 1024 bytes')
        l = f.read(1024)
    f.close()

    print('Done sending')
    conn.send('Thank you for connecting'.encode())
    conn.close()
```
### Client
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000

s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file.txt', 'wb') as f:
    while True:
        print('Receiving data...')
        data = s.recv(1024)
        print('Data =', data)
        if not data:
            break
        f.write(data)

print('Successfully received the file')
s.close()
print('Connection closed')

```
## OUPUT
<img width="1871" height="1026" alt="image" src="https://github.com/user-attachments/assets/1e411f37-d831-4e92-ae77-d8312f2d56b1" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
