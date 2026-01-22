# How to setup Docker for Windows  
 
(01.) First we need to setup the windows before installation.
  *   Go to Windows Features  
  *   Then tick WSL(Windows Sub System for Linux) and Virtual Machine Platform
 
(02.) Then we need to restart the machine. 

(03.) Then we need to check whether WSL and VMP is correctly enabled or not. 
      For that,
  *   Go to powershell
  *   To check WSL version ----> wsl --version
  *   To check WSL         ----> wsl --install
  *   To update WSL        ----> wsl --update
  *   WSL config           ----> wsl --set-default-version 2 
  *   To windows version   ----> winver 

(04.) Donwload and install docker desktop.

(05.) Open Docker Desktop.

(06.) Sign in to Docker Hub using docker desktop.

(07.) We should start the docker desktop service in background services.

(08.) Docker Setup successful.
