# FT800 Calibrate with Arduino FTImpl

``` 
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
```
По умолчанию там уже может быть записаны результаты неверной калибровки. Тогда надо собрать проект с обратным условием.


## Загрузка и вывод изображения - Load and resize image FT800 board EVE
```              
FTImpl.Begin(FT_BITMAPS);
FTImpl.Cmd_LoadIdentity(); //далее будет происходить трансформация изображения
FTImpl.Cmd_Scale(65536*1.27, 65536*1.29); //Увеличиваем X в 1.27 раза, у в 1.29
FTImpl.Cmd_SetMatrix(); //Применяем к изображению
FTImpl.Vertex2ii(10, 10 ,r, 0);	
FTImpl.RestoreContext(); // !
FTImpl.End();  

```
