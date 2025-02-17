import serial
import matplotlib.pyplot as plt
import numpy as np

ser = serial.Serial("COM3", 9600)  # Change to your port
angles = []
distances = []

plt.ion()
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})

while True:
    try:
        data = ser.readline().decode().strip()
        angle, distance = map(int, data.split(","))
        angles.append(np.radians(angle))
        distances.append(distance)

        ax.clear()
        ax.set_ylim(0, 100)  # Adjust according to your range
        ax.scatter(angles, distances, c='red')
        plt.pause(0.01)
    except:
        pass
