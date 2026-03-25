# PROJET_PFE_PORTEUR

## Description

Ce projet permet de contrôler une nacelle de largage composée de plusieurs modules (grabbers) pilotés par servos.

Le système repose sur :

- Raspberry Pi Zero 2 W : contrôle (Python)
- Raspberry Pi Pico : pilotage des servos et des entrées/sorties

La communication entre les deux cartes se fait via une liaison série UART.

---

## Matériel nécessaire

- Raspberry Pi Zero 2 W
- Raspberry Pi Pico
- Carte PCB du projet
- Servomoteurs (x4)
- LEDs (NeoPixel)
- Câbles Dupont

---

## Câblage UART

| Raspberry Pi | PCB | Pico |
|-------------|----|------|
| Pin 8 (TX)  | RX | GP1 |
| Pin 10 (RX) | TX | GP0 |
| 5V          | VCC | VCC |
| GND         | GND | GND |

Important : TX ↔ RX (croisé)

---

## Installation

### 1. Mise à jour système

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install python3 python3-pip python3-venv git -y
```

### 2. Cloner le projet

```bash
git clone https://github.com/bageffray/PROJET_PFE_PORTEUR.git
cd PROJET_PFE_PORTEUR
```

### 3. Environnement Python 

```bash
python3 -m venv .venv
source .venv/bin/activate
```
### 4. Installer les dépendances

```bash
pip install djitellopy pyserial
```

### 5. Activer UART

```bash
sudo raspi-config
```
Interface Options → Serial Port
Login shell → NO
Serial port → YES
```bash
sudo reboot
```
### 6. Firmware Pico
Ouvrir le fichier .ino dans Arduino IDE
Installer les librairies :
    - Adafruit NeoPixel
    - Servo
Flasher le Pico

## Utilisation
### 1. Lancer le programme

```bash
cd firmware/nacelle
source ../../.venv/bin/activate
python nacelle_control.py
``` 

### 2. Commandes
#### Commandes globales
force_open
force_close
cycle_force
#### Commandes par module
open 1
close 1
load 1
launch 1
#### Commandes générales
help
status_req
reset_req
