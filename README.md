[![LTspice](https://img.shields.io/badge/LTspice-%238B0000.svg?style=for-the-badge&logoColor=white)](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)
[![NGSpice](https://img.shields.io/badge/NGSpice-%234070B0.svg?style=for-the-badge&logoColor=white)](http://ngspice.sourceforge.net/)

# Precision Rectifier and Peak Detector Circuit for AC Voltage using LT Spice
Design and simulate an Op-Amp based circuit that can compute the RMS &amp; peak value of a given sinusoidal signal. Here we basically have to design 2 blocks each, a peak detector circuit and a Non-Inverting Amplifier with gain equal to '0.707', for the peak & RMS values respectively.

## Peak Detector Circuit
A peak detector circuit is used to find the peak amplitude in a rapidly changing waveform. Peak detector -s are generally used in sound measuring applications to find the maximum level of sound in a particular area or place, to help determine the maximum loudness level in that place. Like this, freak detector Circuits have a multitude of applications.

For a basic peak detector circuit, we don't even need any complex electronics components. A simple heak detector cirunt can be built by using a diode and a capacitor.

![image](https://github.com/user-attachments/assets/009bc826-2d23-4b0d-b8d2-120199dad66b)

**Basic Circuit Diagram of a Peak Detector**

A positive peak detector captures the most positive point of the input signal and a negative peak detector Captures the most negative point of the input signal. Ideally, the output of the peak detector circuit tracks or follows the input Voltage until the extreme point is reached, but holds that Value as the input decreases.

## Methodology
This circuit captures the peak value of the input Voltage (IN). When IN is positive, D2 is reverse biased, D1 is forward biased and no current flows in the feedback resistor R2. The output Voltage (OUT) therefore tracks the input Voltage (IN) because the outer feedback loof drives the inputs of A1 to a virtual short (V+ = V-). The output Voltage tracks the Voltage on Capacitor C1 because A2 is configured as a Voltage follower. C is charged to this Voltage by the output current of A1 through the D1. R1 prevents the A1 from exceeding its short curent output Current and isolates A1 from the capacitance of C, which prevents ringing or even oscillations. This state holds as long as the input Voltage is positive and increasing

![image](https://github.com/user-attachments/assets/0133d833-4e56-480d-947b-94a04e6c2198)

**An Improved version of the Peak Detector Circuit**

This figure of the circut changes state when the input Voltage decreases. D1 is reverse biased when the input voltage decreases because the output of A1 (anode of D1) drops below the cathode Voltage of D1, which is equal to the previous peak Voltage stored on C. The outer feedback loop is broken in this state and the output of 01 attempts to snah to the negative rail Voltage. D2 is the forward biased component in this case and provides local feedback to A1, which clamps the annode of D1 at one diode drop below the input Voltage. The hold state is maintained until the input voltage overcomes the capacitor voltage, which is equal to the output Voltage. The D2 clamp reduces the transition time from the hold state back to the Tracking State.

![Screenshot (216)](https://github.com/user-attachments/assets/e8705c2f-aedc-41d1-a503-de001f45bb9a)

**Circuit Simulation of an improved form of Peak Detector Circuit in LT Spice**

Speed, is the major limitation of this circuit. The output Voltage cannot be changed any faster than C Can be charged. The speed at which C is charged is limited by the short circuit output current of A1, the forward Voltage drop of D1, the communication Commutation speed of D1 and the exponential rise due to the time Constant formed by R & C.

## Design Calculations
- Time Constant of R1C1 = 0.25 x Time Period
- C = V(peak)/ Vr x f x R = 0.25 x 20 ms = 5ms
  
  We have taken a 1uF Capacitor with a 10K resistor
  Therefore, Time Constant = 1e-6 x 10 x 1000 = 10 ms
- For a Non - Inverting Amplifier Circuit, the values of R3 and R4 will be as follows for gain **0.707**
- Av = ( 1 + R4/R3) = 0.707 , Therefore R3 = 1k & R4 = 1k-0.707k = 0.292k
- In the LT Spice Model, 3 LM741/NS Op-Amps are used and 2 BAT54 Schottky Diodes are used

## Results 
- **Input Voltage = 1 sin(100πt)**
- **Peak Value of Voltage = 1V**

  This is achieved 5 ms after the start of Voltage Flow due to RC time constant.
- **RMS Value = 0.707 V**  

![Screenshot (217)](https://github.com/user-attachments/assets/4a547808-1867-49bd-b8f4-67f530a75db5)

**Output Voltage Waveforms of the Circuit on LT Spice**

![Screenshot (213)](https://github.com/user-attachments/assets/76943222-3278-44b1-9e63-075cf92123ee)

**Frequency Characteristics of the circuit**

## Conclusion

1) A peak detector circuit is used to identify the maximum / peak value in the cvicuit and is used to hold that peak nalue until a peak nolue largeur than the previous one is detected.
2) In this circut, a BAT54 schottky diode is used instead of the regular 2N7000 or 1N914 disde, due to its low turn -voltage, fast recovery time and low loss of energy at ligh frequencies, increasing the overall effrerincy of the circuit.
3) There is a slight delay in peak detection, due to a limitation of speed, the output cannot change faster than the charging time of RC circuit.
4) The use of a clamp circuit can be made too, in which the output/input peak will be clamped using a clamped capacitor.
5) Peak Detector Circuits find applications in signal processing systems, where it is required to detect the peak of a signal. The design of a demodulator for amplitude-modulated(AM signals) are a major application.
