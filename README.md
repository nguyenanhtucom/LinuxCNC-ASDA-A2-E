# Build siitool from source 
  
  $ git clone https://github.com/synapticon/siitool.git
  
  $ make
  
  $ sudo make install

# Write EEPROM for ASDA-A2-E
  
  nat@linuxcnc:~/siitool/delta$sudo ethercat -p0 sii_write Delta-asda.bin
  
  nat@linuxcnc:~/siitool/delta$sudo ethercat rescan
  
  nat@linuxcnc:~/siitool/delta$sudo ethercat slave

# Config ASDA-A2-E Driver
  
  Use ASDA_soft write parameter from file ASDA-A2-E Servo_Ethercat.par   
  
# Create file asda_a2_e.hal

  loadusr ethercat debug 1
  
  loadrt threads name1=master period1=1000000
  
  loadusr lcec_conf ethercat-conf.xml
  
  loadrt lcec
  
  addf lcec.read-all master
  
  addf lcec.write-all master
  
  start
  
  loadusr ethercat debug 0
  
  loadusr halshow my.halshow
  
  loadusr sim_pin lcec.0.3A1.srv-enable-volt lcec.0.3A1.srv-enable lcec.0.3A1.srv-switch-on lcec.0.3A1.srv-vel-cmd 

# Exec file asda_a2_e.hal
  
  $halrun -I asda_a2_e.hal
  
 # Run LinuxCNC GUI
  
  $linuxcnc swm-fm45a.ini
  
  Open file GCode gcode.ngc
  
