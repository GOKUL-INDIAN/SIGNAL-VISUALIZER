# SIGNAL-VISUALIZER
Signal Visualizer is a compact, portable signal analysis device featuring a protected front-end attenuator, high-speed ADC for precise waveform capture, and an ATmega328 processing core. It includes a full-color display, intelligent battery management, onboard USB reprogramming, and an all-SMD design for enhanced portability and reliability.

# BLOCK DIAGRAM
Overall, the design consist of a front end, which includes an attenuator accompanied by a signal
conditioner. Then follows the ADC part which samples the analog input. The next part is the
heart of the design, the controller of the arduino (ATMEGA 328), which processes the sampled
data. Next is the TFT screen which displays the processed output from the controller. In
addition to that a power supply unit consisting of adequate circuitry to provide specific power
to different components in the device is also employed.
# ATTENUATOR
Theattenuator block is the main part of the front end design of the scope. The attenuator section
consists of mainly two parts. They are :
• Thecompensated attenuator ladder
• Analog multiplexer
The compensated attenuator ladder : This is the voltage attenuating section and it attenuates
wide span of random input signal voltages to a safe operational voltage range to our device. It is
equipped with frequency compensated potential divider arrangement so as to cop up with wide
range of frequency inputs without distortion. The desired range of input voltage is between 0v
to 10v
Analog multiplexer : This is an IC to select which analog input has to be given for processing
by digital switching.
Frequency compensated potential divider circuit :
Basically a frequency compensated potential divider is a 2 port RC network providing a fixed
voltage division ratio over a wide frequency range. In this arrangement capacitors are added
parallel to each resistors. It reduces the parasitic capacitance of the resistors which is highly
active at high frequencies. At low frequencies the resistors act as the voltage divider but at high
frequencies capacitors act as the voltage divider circuit
Atypical potential divider circuit with frequency compensation is given below :
Analog multiplexer:It is used to select required input attenuated signal. It is a wideband 4 to 1 analog multiplexer.
It is controlled by a 2 bit binary input. The schematic model for multiplexer is shown below 

# SIGNAL CONDITIONER
This section provides a high input impedance and low output impedance in the circuit. That
is, the signal after attenuation has already been a bit power lost and to increase the power of
the signal, this section is used. This section avoids the loading effect which can be caused by
feeding the signal to the ADC chip. An operational amplifier with unity gain configuration is
implemented for satisfying the above condition. This section also provide a DC shift facility
inorder to move the signal up or down.
This section also provides a protection against high voltage input, because the supply voltage
for the op amp is only 3 volts, so if in case an input of greater volts is applied then the op amp
could only provide a maximum of 3 volts , thus keeping the associating circuits safe and sound.
The operational amplifier used in the conditioner design is NJM4565.The specifications are :
High gain, wide bandwidth (4 MHz), slew rate (4V/us), capable of driving 20 V peak to peak
into 400 ohms loads.
# ANALOG TO DIGITAL CONVERTER
Arduino has the provision to directly accept analog input and process it. But the sampling rate
of arduino is very low. Lower sampling rate will result in a very unpleasant output signal in the
display, thus reducing the efiiciency of the scope. As a solution to this problem, an additional
ADC chip having very high sampling rate is used. The chip used here is TLC 5510 (whose
datasheet specifications are given at the end). The chip is capable of sampling the signal at a
rate of 10Msps to 15 Msps. The full scale voltage input is restricted to 2V.
The completed circuit diagram for this section is given below:
After implementing the above circuit diagram the following specifications have been obtained:
• Highsampling rate ranging up to 15 MSPS.
• 8bit parallel data out, which can be connected to microcontroller pins.
• 2Vfull scale input voltage.
• Single power supply operation
After sampling the conditioned input signal, it is now time to process and display it on the
screen.
# PROCESSING UNIT(ATMEGA 328P)
The processor chip, Atmega 328 acts as the core computing part of this device. It accepts the
input from the ADC and stores it temporarily for processing. The processor also drives the final
output TFT display screen. It also controls the input multiplexer operations. To comment about
the specifications, it has :
• 8bit AVRRISCbased microcontroller
• 32bit program flash memory
• 2KBSRAM
• Total 32 pins (8 analog pins and 14 digital pins)
The figure of SMD package used is shown below:
The detailed circuit diagram with all the specific connections are depicted below:
As seen in the circuit, no complex components are needed to use the controller chip. A set of
resistors and capacitors are needed to wire up the circuit. External crystal is added to provide
the clock pulses for the operation of the processor (16MHz). The controller is programmable
using a USB serial interface IC which is provided in the device. The 8 pins are configured
as input , to receive the input from the ADC chip (8 bit serial communication). Two pins are
provided for the digitally controlled switching of the multiplexer.
# POWER SUPPLY
This is definitely one of the most delicate and important section for the entire design. This
section produce different voltages for each parts. All the necessary voltages are generated from
the Lithium-ion cell. It makes the device portable.
Mainly the power supply section consist of three parts:
• Boost converter
• 555charge pump
• 3vregulator
Boost converter, provides a stable 5 volt supply for arduino and ADC. 555 charge pump circuit
provides the negative power supply for signal conditioner. The 3 volt regulator is used to gen
erate voltage (3.3 volts) for display. The boost converter is realized using the DC-DC converter
IC MT3608. It is a constant frequency 6-pin SOT23 current mode step-up converter intended
for small low power applications. This IC switches at 1.2MHz and allows the use of tiny, low
cost capacitors and inductors 2mm or less in height. Internal soft start results in small inrush
current and extends battery life.
Using 555 as a charge pump is a cheap and easy solution for doubling tripling or inverting the
supply voltage. Charge pump can be used in a non-synchronous rectifier when in low dropant
mode to cause a high output ripple with a light load.
All components used are SMD variants, in order to reduce the size considerably. The 3.3 volt
is generated by the IC HT7130 which is a low drop out linear regulator.
# BATTERY MANAGEMENT 
The power house of the entire device is the lithium ion cell (3.7V). The cell is capable of
providing necessary power but it is very dangerous to handle. The reason for that is lithium
ion batteries may even explode if the handling is careless and improper. The cell must be taken
special care to avoid shorting at any cost. The design includes a protection circuit to cancel
the after effect of short circuit incidents and also an over voltage protection. This system also
includes an intelligent battery charging system to keep battery in good condition. Full charge
indicator is also included to safely remove from charging at the riht time. Apart from that an
auto cut-off facility is also added to the management system.
The circuit mainly consist of three ICs. TP4056 , DW01A , S8205.
The TP 4056 IC is a complete constant current / constant voltage linear charger for single cell
lithium ion batteries. Its SOP package and low external component count makes it ideally suited
for portable applications. It also can work within USB and wall adaptors. No blocking diode is
required due to the internal PMOSFET architecture and have prevent to negative charge current
circuit. Thermal feedback regulates the charge current to limit the die temperature during high
power operation or high temperature operation.
DW01A is a battery protection IC designed to protect lithium ion battery from damage or
degrading the life time due to overcharge over discharge or over current events. The ultra small
package and less required external components make it ideal to use in any circuit combinations
S8205A is a MOSFET IC which contain two MOSFETS. Each mosfet is controlled by the
DW01IC. It is act as a switch to disconnect the battery when the IC detect deep discharge and
over charge. The internal reverse diode bypass the current to the cell for charging.
The detailed circuit diagram for the above mentioned battery management unit is shown below:
# USB INTERFACE
USB interface is provided a provision for firmware updation. It helps to connect the processor
with the computer, which enables the user for proper updation and even slight program mod
ifications. This section consist of only a single chip with minimum external components as
shown below:
The CH340 is a serial to USB chip used to implement the USB interfacing facility. It is a
USBbusconverter chip and it can realize USB convert to serial interface, USB convert to IrDA
interface or USB convert to printer interface.
In serial interface mode, CH340 supplies common MODEM liaison signal used to enlarge
asynchronous serial interface of computer or upgrade the common serial device to USB bus
directly:
# DISPLAY
The display used is a 2.8 inch TFT (Thin Film Transistor) display. It has a 240 x 320 pixel
resolution. It is a full color LCD display. This module is built in with IL19341V IC. It supports
8/16 bits 8080– series parallel MCU interface. It is a portrait mode LCD module.
# ADC CLOCK CIRCUIT
The clock circuit is the most important circuit for any microprocessor based working devices.
It provide the timing sequence for the efficient working of the circuit. Here the clock circuit
is made by using a combination of NOT gate IC and a crystal. The NOT gate IC used is
the common digital IC 7414 which has a total of six Schmitt triggered NOT ICs. The circuit
diagram for the production of 16 MHz clock signal is shown below:
# PROGRAM FLOW
• Specified packages to drive the TFT screen is imported
• Required output pins for implementing serial communication with TFT is defined.
• Anarray of data matching with total pixel matrix size of the TFT screen is pre- defined.
• Input pins to read the digital inputs from the ADC chip is allocated.
• Thearray is filled with digital inputs using the iterative function, for( ).
• Thestored data given to the TFT
• Search for input contorl signals via switches
• Repeat the whole process

# FULL CIRCUIT DIAGRAM
# ACHIEVED SPECIFICATIONS AND OUTCOME
• Bandwidth up to 1MHz
• Support all types of waveform
• Input signal voltage range up to 10V
• Highinput impedance 0.5 M
• Highsampling rate 10 M Samples/second
• Highsignal to noise ratio
• 8-bit resolution

