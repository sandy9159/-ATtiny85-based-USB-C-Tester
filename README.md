# ATtiny85-based-USB-C-Tester

designe credit to : - https://oshwlab.com/wagiminator/attiny85-usb-c-tester

![image](https://user-images.githubusercontent.com/19898602/159016797-cd10cd7e-3c65-4f68-a068-8c34d8b91b72.png)



Simple USB-C Power Delivery Tester based on ATtiny25/45/85 and INA219. 

The device measures 

> voltage

> current

> power 

> energy capacity

and displays the values on an OLED screen. You can switch between different screens by pressing the SET button.


# Circuit diagram 

![image](https://user-images.githubusercontent.com/19898602/159018437-68980ed4-dceb-4ad0-8b68-59e58a632e87.png)

![image](https://user-images.githubusercontent.com/19898602/159020151-eefe0284-c947-4c7b-8fc4-2eaefce2c2e7.png)

![image](https://user-images.githubusercontent.com/19898602/159019338-53ee50e2-93df-4f16-abfb-72b0e38e0e72.png)

![image](https://user-images.githubusercontent.com/19898602/159019776-c7b7086e-d09c-4b1c-a112-c8c0b91b417c.png)


![image](https://user-images.githubusercontent.com/19898602/159020608-3df3cf5c-dc08-4fdb-a4f4-1c0d40e3af0f.png)


If you guys want to order the PCB please downlod the gerber file from here

[USB_C_Tester_gerber_v1.0b.zip](https://github.com/sandy9159/ATtiny85-based-USB-C-Tester/files/8305138/USB_C_Tester_gerber_v1.0b.zip)

I always prefer [JLCPCB.com](https://jlcpcb.com/IAT) for my PCB needs, [JLCPCB.com](https://jlcpcb.com/IAT) have best deals for their customers
$2 for 1-4 Layer PCBs, free SMT assembly monthly.

![image](https://user-images.githubusercontent.com/19898602/159014034-3c9a50c3-61c3-40d2-836d-9cadc2317d33.png)


SMT Assembly service of [JLCPCB.com](https://jlcpcb.com/IAT) is cherry on top now get your PCB fully assembled and save your time and money
Select components for your PCB from there Parts Library of 200k+ in-stock components
they are offering $27 valued New User coupon  & $24 SMT coupons every month
$8.00 setup fee, and $0.0017  per joint

Now no need to order components separately for you PCB and get free from stress of soldering them on PCB just try PCB SMT assembly service and get you PCB with components pre assembled and ready for the project


👉 Try PCBA service of JLCPCB.com/PCW and save your time and money, get PCB ready for project, 200K+ components in library of JLCPCB.com/PCW as well as 3rd party         parts to choose from. 
    Assembly will support 10M+ parts from Digikey, mouser
    
👉 $27 valued New User coupons 

👉 $24 SMT coupons every month


For more detials & offers please visit [JLCPCB.com](https://jlcpcb.com/IAT)


[Click here to visit JLCPCB.com](https://jlcpcb.com/IAT)



# Hardware 

USB Connectors

The device is equipped with a USB-C receptacle (PCB version a) or plug (PCB version b) for the input and a USB-C receptacle for the output, 

so that it can be plugged between the power supply and the consumer. 

CC1 and CC2 communication channels are passed through so that supply and consumer can negotiate the bus power.

![image](https://user-images.githubusercontent.com/19898602/159016917-4de07d64-41ed-47f8-95fd-6e8792ebde74.png)


![image](https://user-images.githubusercontent.com/19898602/159016926-9b2f37e6-62f6-4f97-99eb-37341168666f.png)




# Voltage and Current Measurement

An INA219 is used to measure voltage and current. The INA219 is a current shunt and power monitor with an I²C-compatible interface. 

The device monitors both shunt voltage drop and bus supply voltage, with programmable conversion times and filtering.

A programmable calibration value, combined with an internal multiplier, enables direct readouts of current in amperes. 

The selected shunt resistance of 8mΩ enables both a very small influence on the circuit and a measurement with a resolution of 1mA. 

For an accurate measurement, a shunt resistor with a low tolerance (1% or better) should be selected.

# User Interface

The user interface utilizes two buttons and a 128x64 pixels OLED display. 

An ATtiny24/45/85 microcontroller handles the user interface as well as the calculation and display of the values.


![image](https://user-images.githubusercontent.com/19898602/159017028-36dee7ae-f4b8-48d1-8698-cbf36043d394.png)



# Software

Basic Principle

The INA219 continuously measures current and voltage and transmits the values to the ATtiny via I²C. 
From this, the ATtiny calculates the other values and displays them on the OLED screen.

I²C OLED Implementation

The I²C protocol implementation is based on a crude bitbanging method. 
It was specifically designed for the limited resources of ATtiny10 and ATtiny13, but it works with some other AVRs (including the ATtiny25/45/85) as well. 
The functions for the OLED are adapted to the SSD1306 OLED module, but they can easily be modified to be used for other modules.
In order to save resources, only the basic functionalities which are needed for this application are implemented. 
For a detailed information on the working principle of the I²C OLED implementation visit TinyOLEDdemo.

Accuracy of Time and Capacity Determination

The internal oscillator of the ATtiny is used to determine energy and capacity. 
The accuracy of the internal oscillator is +/-10% with the factory calibration. 
This can be improved to +/-2% or better by manual calibration. 
The calibration value determined in this way can be set in the source code.

# Compiling and Uploading

Since there is no ICSP header on the board, you have to program the ATtiny either before soldering using an SOP adapter, or after soldering using an EEPROM clip. The AVR Programmer Adapter can help with this.

If using the Arduino IDE

> Make sure you have installed ATtinyCore.

> Go to Tools -> Board -> ATtinyCore and select ATtiny25/45/85 (No bootloader).

> Go to Tools and choose the following board options:

> Chip: ATtiny25 or 45 or 85 (depending on your chip)

> Clock: 1 MHz (internal)

> B.O.D.Level: B.O.D. enabled (2.7V)

> Leave the rest at the default settings

> Connect your programmer to your PC and to the ATtiny.

> Go to Tools -> Programmer and select your ISP programmer (e.g. USBasp).

> Go to Tools -> Burn Bootloader to burn the fuses.

> Open USB_C_Tester sketch and click Upload.

If using the precompiled hex-file

> Make sure you have installed avrdude.

> Connect your programmer to your PC and to the ATtiny.

> Open a terminal.

> Navigate to the folder with the hex-file.

> Execute the following command (if necessary replace "usbasp" with the programmer you use):

```
avrdude -c usbasp -p t85 -U lfuse:w:0x62:m -U hfuse:w:0xd5:m -U efuse:w:0xff:m -U flash:w:usb_c_tester.hex

```

# Operating Instructions

1. Connect the device between a power supply and a consumer. Due to the internal structure of the USB-C cables, it may be necessary to change the orientation of one of the cable plugs if you are using the 2-receptacle version of the device.
 
2. Use the SET button to switch between the different screens.

3. Use the RESET button to reset all values.

![image](https://user-images.githubusercontent.com/19898602/159017719-1d222ae5-c187-4c2c-bdc8-27ad2cae952b.png)


![image](https://user-images.githubusercontent.com/19898602/159017737-8144668d-5a0c-4680-9797-31b65013ec5f.png)


# Characteristics

Parameter	Value

Voltage	5V - 20V

Current	max 5A

Voltage Measurement Resolution	4mV

Current Measurement Resolution	1mA

