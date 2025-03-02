---
title: "Minecraft Pomodoro"
---

python

```
import argparse
import socket
from time import sleep
from datetime import datetime
import subprocess
# POMODORO = 25
# REST = 5
POMODORO = 1
REST = 1

SUNSET = 12000
DAY_START = 24000

def main():
    HOST = "localhost"
    PORT = 25575
    PASSWORD = "***"

    while True:

        # sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # sock.connect((HOST, PORT))

        try:
            # Log in
            # result = login(sock, PASSWORD)
            # if not result:
            #     print("Incorrect rcon password")
            #     return

            tick = get_tick()
            request = f"time set {tick}"
            # request = "time query"
            print(f"send {request}")
            # response = command_no_response(sock, request)
            subprocess.check_call(f'mcrcon -s -p {PASSWORD} "{request}"', shell=True)
            sleep(1)
        finally:
            # sock.close()
            pass

def get_tick():
    now = datetime.now()
    minute = (now.minute + now.second / 60) % (POMODORO + REST)

    if minute <= POMODORO:
        tick = minute * SUNSET / POMODORO
    else:
        m = minute - POMODORO
        tick = SUNSET + (DAY_START - SUNSET) * m / REST
    return int(tick)


if __name__ == '__main__':
    main()

```

