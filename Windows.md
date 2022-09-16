# Windows Setup

Requires Windows 11, WSL2 enabled.

1. Install Docker Desktop, enable WSL2, start docker desktop
2. Install Visual Studio Code 
3. Create a file `docker-compose.yml` like below: 

```
version: '3'
services:
  noetic-desktop-full:
    image: osrf/ros:noetic-desktop-full
    volumes: 
      - ../:/workspace:cached
      - /tmp/.X11-unix:/tmp/.X11-unix
      - /mnt/wslg:/mnt/wslg
      - /usr/lib/wsl:/usr/lib/wsl
      
    devices: 
      - /dev/dxg:/dev/dxg

    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
    
    environment: 
      - DISPLAY=:0
      - WAYLAND_DISPLAY
      - XDG_RUNTIME_DIR
      - PULSE_SERVER
    
    command: /bin/sh -c "while sleep 1000; do :; done"
```

4. Place it in your dev directory, open VS Code, run Ctr-Shift-P and select "Remote Containers: Open Folder In Container"
5. Choose make container from `docker-compose.yml`
