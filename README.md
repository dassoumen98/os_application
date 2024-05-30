# os_application

```py
#wait for a process
import os
pid = os.fork()
if pid ==0:
    os._exit(0)

else:
    pid,status =os.waitpid(pid,0)
    if os.WIFEXITED(status):
        print("child process exited with status:", os.WIFEXITED(status))
    else:
        print("child process terminated abnormality")


```

```py
#zombe process
import multiprocessing
import os
import time

def zombie_process():
    print(f"Child process {os.getpid()} running")
    time.sleep(2)
    print(f"Child process {os.getpid()} exiting")

if __name__ == '__main__':
    p = multiprocessing.Process(target=zombie_process)
    p.start()
    p.join()  # Wait for the child process to finish
    print(f"Parent process {os.getpid()} exiting")
```
```py
#orpahin process
import os
import time
def orphan_process():
  print(f"child process{os.getpid()}running")
  time.sleep(2)
  print(f"child process{os.getpid()}exiting")

if __name__ == '__main__':
  pid = os.fork()
  if pid == 0:#child process
    orphan_process()
  else:
```

```py
#creation of process using fork call
import os
def main():
  pid = os.fork()
  if pid<0:
    print("Child Process creation")
  elif pid == 0:
    print("child process")
  else:
    print("parent process")

main()
```
```py
#find the name of os
import os
print(os.name)
```
```py
#return the group id of currenr process
import os
print(os.getegid())
```

```py
#write down a python code to handel a signal
import signal
import sys
def signal_handler(sigral, frame):
  print('Signal recived, exiting ..... ')
  sys.exit (0)
signal.signal(signal.SIGINT,signal_handler)
print('Running, press Ctrl+c to exit .... ')
```
```py
#write down a python code to block a signal
import signal
import time

# Define a signal handler
def handler(signum, frame):
    print(f"Signal {signum} received")

# Register the signal handler for SIGINT (Ctrl+C)
signal.signal(signal.SIGINT, handler)
signal.siginterrupt(signal.SIGINT, False)

print("Blocking SIGINT...")

while True:
    time.sleep(1)

```
```py
#write down the python code to suspending a signal
import os
import signal

def suspend_process(pid):
    try:
        os.kill(pid, signal.SIGSTOP)
        print(f"Process with PID {pid} suspended")
    except OSError as e:
        print(f"Failed to suspend the process: {e}")

pid = 1234
suspend_process(pid)

```

```py
#UDP
#Server:
#echo server using UDP 
import socket
HOST="192.168.60.138"
PORT=65432
s = socket.socket (socket.AF_INET, socket.SOCK_DGRAM) 
s.bind((HOST, PORT))
print ("UDP server is running")
while True:
    data=s.recvfrom (1024)|
    message=data [0] 
    address=data [1]
    print (message.decode('utf-8')) 
    print (format (address))
    s.sendto (message, address)



#clint
#echo client using UDP 
import socket
HOST="192.168.60.138"
PORT=65432
s = socket.socket (socket.AF_INET, socket.SOCK_DGRAM)
while True:
    d1 = input ("Enter your message")
    s.sendto (d1.encode('utf-8'), (HOST, PORT))
    data= s.recvfrom (1024)
    print (data [0].decode('utf-8'))
```

```py
Socket programming using TCP :

Server:

#echo server

import socket

HOST="192.168.60.141"

PORT=64431

with socket.socket(socket.AF_INET, socket. SOCK STREAM) as s:

s.bind((HOST, PORT))

s.listen()

conn, addr=s.accept()

with conn:

print (f"connected by (addr)")

while True:

data=conn.recv(1024)

if data:

conn.sendall (data)

Client:

#echo client

import socket

HOST="192.168.60.141"

PORT=64431

with socket.socket (socket.AF_INET, socket.SOCK_STREAM) as s:

s.connect ((HOST, PORT))

while True:

dl=input ("Enter your message")

s.sendall (dl.encode ('utf-8'))

data=s.recv(1024)

print (data.decode('utf-8'))
```

```py
# chat server

import socket

HOST = "192.168.60.141"
PORT = 64431

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen()
    print(f"Server listening on {HOST}:{PORT}")
    
    conn, addr = s.accept()
    with conn:
        print(f"Connected by {addr}")
        while True:
            data = conn.recv(1024)
            if not data:
                break
            print("Client:", data.decode("utf-8"))
            reply = input("Enter your reply: ")
            conn.sendall(reply.encode('utf-8'))

# echo client

import socket

HOST = "192.168.60.141"
PORT = 64431

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    print(f"Connected to server at {HOST}:{PORT}")
    
    while True:
        message = input("Enter your message: ")
        s.sendall(message.encode('utf-8'))
        data = s.recv(1024)
        if not data:
            break
        print("Server:", data.decode('utf-8'))


```
