# FT800 Calibrate with Arduino FTImpl

<code>
if((EEPROM.read(0) != 0x7C)){
        FTImpl.DLStart();
        FTImpl.Cmd_Calibrate(0);
        FTImpl.Finish();
        for (int i = 0; i < 24; i++)
          EEPROM.write(1 + i, FTImpl.Read32(REG_TOUCH_TRANSFORM_A + i));
    EEPROM.write(0, 0x7c);  // is written!	
 }else{
 
  for (int i = 0; i < 24; i++)
      FTImpl.Write32(REG_TOUCH_TRANSFORM_A + i, EEPROM.read(1 + i));
      
 }
 </code>
