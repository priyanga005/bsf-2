import numpy as np
import scipy.signal as signal
import matplotlib.pyplot as plt

# Define filter specifications
fs = 1000  # Sampling frequency in Hz
f0 = 50    # Center frequency of the band-stop filter in Hz
bw = 10    # Bandwidth (stopband width) in Hz

# Normalize the frequencies (as a fraction of the Nyquist frequency)
nyquist = 0.5 * fs
low = (f0 - bw / 2) / nyquist
high = (f0 + bw / 2) / nyquist

# Design a Butterworth band-stop filter
order = 4  # Order of the filter
b, a = signal.butter(order, [low, high], btype='bandstop')

# Frequency response
w, h = signal.freqz(b, a, fs=fs)

# Plot the frequency response
plt.figure()
plt.plot(w, 20 * np.log10(abs(h)), 'b')
plt.title('Butterworth Band-Stop Filter Frequency Response')
plt.xlabel('Frequency [Hz]')
plt.ylabel('Amplitude [dB]')
plt.grid()
plt.show()
