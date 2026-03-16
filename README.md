# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
server.py
```

import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```

client.py
```

import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## OUTPUT
server.py
<img width="692" height="221" alt="image" src="https://github.com/user-attachments/assets/3dc37216-2980-49f0-bae7-93ec80dc839d" />

client.py
<img width="999" height="594" alt="image" src="https://github.com/user-attachments/assets/0b19246b-0565-42fa-bb2f-d7ec7f7bd389" />

<img width="730" height="222" alt="image" src="https://github.com/user-attachments/assets/1c28d012-e7d6-4b46-a975-d842ec1ad47d" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
