Intel HEX format is a object file format used to program that presents binary data in ASCII format.
It is used to program microcontrollers, EPROM / FLASH memories etc. 

Data is written in hexadecimal format and each row contains 6 fields:
<ul>
  <li>Start code- one ASCII character `:`</li>  
  <li>Byte count- 2 hex digits- specifies a number of bytes in data section</li>  
  <li>Address- 4 hex digits- begining of 16bit memory address offset</li>  
  <li>Record type - 2hex digits </li>
  <li>Data</li>
  <li>Checksum</li>
</ul>
File example:
![[intelhex.png]]