<p align="center">
  <img src="https://github.com/danielneil/Shark/blob/main/shark/files/shark_ui_patches/logofullsize.png?raw=true">
</p>

# Shark Doc 

Documentaiton for Shark, an algorithmic trading platform

## Quick Start Instructions 

<details>
<summary>System Requirements</summary>
<br>
  
| Operating System | CPU  | RAM | DISK |
| ------------- | ------------- | ------------- | ------------- |
| Rocky Linux 8+         | 4 CPU   | 8 GB |80 GB  |
  
</details>


## Setup

<details>
<summary>System Installation</summary>
<br>
  
1. Prepare a vanilla Rocky Linux (server instance) with VirtualBox ([help](https://kifarunix.com/install-rocky-linux-8-on-virtualbox/)).

2. Install epel - open a terminal, and run:
  ```
yum install epel-release -y
```
  
3. Install ansible - open a terminal, and run:
  ```
yum install ansible -y
```

4. Install git - open a terminal, and run:
  ```
yum install git -y
```

5. Open a terminal, and run:
```
git clone https://github.com/danielneil/Shark.git && cd Shark && ./build.sh
```
6. Navigate to http://shark-server/shark (web credentials are shark/shark) - it will take a few minutes to populate with data.
</details>

## Sample Configuration
```
TPD
```

## Sample Backtests
* [Moving Averages](https://github.com/danielneil/Shark-Config/blob/master/backtests/files/backtests/moving_averages.py).
* [BBands](https://github.com/danielneil/Shark-Config/blob/master/backtests/files/backtests/BBands.py).
* [RSI2](https://github.com/danielneil/Shark-Config/blob/master/backtests/files/backtests/rsi2.py).
