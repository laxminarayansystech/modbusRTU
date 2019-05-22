# modbusRTU
This tutorial shows how to communicate with a PLC device from your C# or python application through modbus RTU

# Required Tools
- C# application
1. Visual Studio installed
2. Download *EasyModbusTCP/UDP/RTU .NET* from here(https://sourceforge.net/projects/easymodbustcp/) extract and copy *EasyModbus.dll* to a prefered directory.
3. In your visual studio c# application, add *EasyModbus.dll* to the solution. If you have created any application yet, created a console application or download my source code from here.
  * At the solution explorer, right click on *References*
  * click *Add Reference* > click *Browse* to locate *EasyModbus.dll* > Click *Add and check it* > click *ok* 
4. Download and install *Free virtual serial ports*(https://freevirtualserialports.com/). This will help to create a virtual pair of serial ports <COM1-COM2> for communication tesing. **IF YOU HAVE A PHYSICAL PLC DEVICE THIS STEP MAY NOT BE NECESSARY**
5. Download & install *Modbus PLC Simulator*(http://www.plcsimulator.org/) **IF YOU HAVE A PHYSICAL PLC DEVICE THIS STEP MAY NOT BE NECESSARY**
6. Run the *Modbus PLC Simulator* from the *prot bar* change the protocol to *MODBUS RS-232*
7. Run the *Free virtual serial ports* and create a pair of virtual ports <COM1-COM2>
  * C# application will connect to *COM1*
  * *Modbus PLC Simulator* will connect to the other end of the pair, that's *COM2*
8. Code snippet 
~~~~
ModbusClient modbusClient = new ModbusClient("COM1"); // Connection object using COM1 port
modbusClient.Connect();
modbusClient.WriteMultipleRegisters(49, new int[10] { 112, 12, 3, 4, 53, 6, 27, 80, 9, 1 }); // write values to multiple registers
modbusClient.WriteMultipleCoils(29, new bool[10] { true, true, true, true, true, true, true, true, true, true, }); // write values to multiple coils
  
  //Reads & display Discrete Inputs from coil #5, #6, #7
Console.WriteLine("Value of Coil #5-7.................." + coils5_6_7[0].ToString() + " " + coils5_6_7[1].ToString() + " " + coils5_6_7[2].ToString());
 //Reads Registers #50-59
int idx = 0;
foreach (var k in regRange)
  {
    Console.WriteLine("Holding Regs {0} = ..................{1}", 50 + idx,  regRange[idx].ToString());
    idx++;
  }
~~~~
9. Compile & run the c# application. Check the *Modbus PLC Simulator* for written values, Check your application console for read values

# python application
- With python installed, at the terminal run *pip install pymodbus* to install modbus python api
