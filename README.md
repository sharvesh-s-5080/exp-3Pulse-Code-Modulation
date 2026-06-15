# Pulse-Code-Modulation
## Aim:
Write a simple Python program for the modulation and demodulation of PCM, and DM.
## Tools required:
Google Colab
## Program:
### puls code modulation (PCM):
```
import numpy as np, matplotlib.pyplot as plt
t = np.linspace(0,0.05,500,False)
m = np.sin(2*np.pi*100*t)
c = np.sign(np.sin(2*np.pi*200*t))
q = np.round(m/0.125)*0.125
for i,s in enumerate([m,c,q,q],1):
    plt.subplot(4,1,i)
    plt.plot(t,s) if i!=3 else plt.step(t,q)
    plt.grid()
plt.show()()
```
## Output Waveform:
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ebd04736-7291-48dd-a352-b9f7cc37c461" />

## Delta Modulation(DM):
```
import numpy as np, matplotlib.pyplot as plt
from scipy.signal import *
t=np.arange(0,1,1/10000)
m=np.sin(20*np.pi*t)
p=0;e=[]
for s in m:
    e+=[s>p]; p+=0.1 if s>p else -0.1
dm=np.cumsum([0.1 if b else -0.1 for b in e])
y=filtfilt(*butter(4,20/5000,'low'),dm)
for i,s in enumerate([m,dm,y],1):
    plt.subplot(3,1,i)
    plt.plot(t,s) if i!=2 else plt.step(t,s)
plt.show()
```
## output:
<img width="500" height="590" alt="image" src="https://github.com/user-attachments/assets/d68fc8b4-1350-4986-969b-01b7e32f0ef5" />


## Results:
The analog signal was successfully encoded and reconstructed using PCM and DM techniques in Python, verifying their working principles..

