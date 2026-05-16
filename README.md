# Pulse-Code-Modulation
## Aim:
Write a simple Python program for the modulation and demodulation of PCM, and DM.
## Tools required:
Google Colab
## Program:
### puls code modulation (PCM):
```
#PCM
import numpy as np
import matplotlib.pyplot as plt

fs, f, d, q = 10000, 100, 0.05, 16

t = np.linspace(0, d, int(fs*d), endpoint=False)
m = np.sin(2*np.pi*f*t)
c = np.sign(np.sin(2*np.pi*200*t))

step = (m.max()-m.min())/q
qm = np.round(m/step)*step
pcm = ((qm-qm.min())/step).astype(int)

titles = ["Message Signal (Analog)",
          "Clock Signal (Increased Frequency)",
          "PCM Modulated Signal (Quantized)",
          "PCM Demodulation Signal"]

signals = [m, c, qm, qm]
colors = ['b', 'g', 'r', 'purple']

plt.figure(figsize=(12,10))

for i in range(4):
    plt.subplot(4,1,i+1)
    
    if i == 2:
        plt.step(t, signals[i], color=colors[i])
    else:
        plt.plot(t, signals[i], color=colors[i],
                 linestyle='--' if i==3 else '-')
    
    plt.title(titles[i])
    plt.xlabel("Time [s]")
    plt.ylabel("Amplitude")
    plt.grid()

plt.tight_layout()
plt.show()
```
## Output Waveform:
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ebd04736-7291-48dd-a352-b9f7cc37c461" />

## Delta Modulation(DM):
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs, f, T, d = 10000, 10, 1, 0.1

t = np.arange(0, T, 1/fs)
m = np.sin(2*np.pi*f*t)

e, dm, p = [], [0], 0

for s in m:
    b = 1 if s > p else 0
    e.append(b)
    p += d if b else -d
    dm.append(p)

x = [0]
for b in e:
    x.append(x[-1] + d if b else x[-1] - d)

b, a = butter(4, 20/(0.5*fs), 'low')
y = filtfilt(b, a, x)

titles = ['Original Signal',
          'Delta Modulated Signal',
          'Demodulated & Filtered Signal']

signals = [m, dm[:-1], y[:-1]]

plt.figure(figsize=(12,6))

for i in range(3):
    plt.subplot(3,1,i+1)
    
    if i == 1:
        plt.step(t, signals[i], where='mid')
    else:
        plt.plot(t, signals[i],
                 linestyle='dotted' if i==2 else '-' ,color='r')
    
    plt.legend([titles[i]])
    plt.grid()

plt.tight_layout()
plt.show()

```
## output:
<img width="500" height="590" alt="image" src="https://github.com/user-attachments/assets/d68fc8b4-1350-4986-969b-01b7e32f0ef5" />


## Results:
The analog signal was successfully encoded and reconstructed using PCM and DM techniques in Python, verifying their working principles..

