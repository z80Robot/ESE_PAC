# PAC - Pana Amusement Cartridge  

Es un cartucho de expansión compatible con el "Pana Amusement Cartridge" para MSX lanzado por Panasonic. El original utilizaba SRAM, pero este modelo emplea FRAM que no requiere bateria para mantener los datos en la memoria.

![ケース無し](./PCB/Image1.jpg)  

参考資料(対応ソフト情報など）：  
https://ja.wikipedia.org/wiki/パナアミューズメントカートリッジ  
カセットは、Boothおよび一部ショップにて販売予定です。  
https://ifc.booth.pm/items/3479171  

## ■ Mapa de memoria

Especificación idéntica a la del cartucho Pana Amusement.

| Page (8kB)    | Switching address                  | Initial Setting                     |
| ------------- | ---------------------------------- | ----------------------------------- |
| 4000h ~ 5FFDh | 5FFEh = 4Dh / 5FFFh = 69h (Enable) | 5FFEh = 00h / 5FFFh = 00h (Disable) |

## ■ Control de la FRAM
Para cambiar al modo de escritura, escribe los valores 4Dh en la dirección 5FFEh y 69h en la dirección 5FFFh. Esto convertirá el rango de direcciones 4000h-5FFDh en un área de RAM.

No existe un método específico para identificar si el PAC está implementado en el slot. Cambia de slot y verifica si se ha activado escribiendo los valores 4Dh en 5FFEh y 69h en 5FFFh, luego intenta escribir datos en el rango de direcciones 4000h ~ 5FFDh para confirmarlo. Ten cuidado de no dañar los datos originalmente escritos en esta área al implementar el código.

※ En el programa de lectura y escritura, esta operación se ejecuta mediante la función chkPacInSlot(). 

## ■ Programa de lectura/escritura
Se incluyen los programas pacread y pacwrite para realizar operaciones de lectura y escritura en la RAM del PAC. Inserta el cartucho en cualquiera de los slots y ejecuta los siguientes comandos para realizar una copia de seguridad de los datos de la RAM y restaurarlos. 
Además, si tienes un FM-PAC, también puedes usar la utilidad call fmpac para este propósito.

● Lectura
`>pacread.com [Archivo de salida]`  
● Escritura
`>pacwrite.com [Archivo de entrada]`  
● Programa de prueba (no es estable)
`>pactest.com`  

El código fuente puede compilarse con z88dk. Las opciones de compilación son las siguientes:  
`zcc +msx -create-app -subtype=msxdos -lmsxbios  main.c -o xxxx.com`  
  
  
## ■ 頒布基板について
回路図およびガーバファイルが必要な場合はPCBのフォルダーを参考にしてください。  
<img src="./PCB/Schematic/esePAC.png" width=800>  
  
## ■ CPLDについて
CPLD Xillix XC9536XLの設計データはRTLのフォルダーを参照してください。  
  
## ■ カードリッジシェルについて
RGRさんのTransparent Cartridge Shell for MSX Konami-styleに合う様に設計しています。  
https://retrogamerestore.com/store/msx_cart_shell/  
https://ifc.booth.pm/items/3240279  
輸入と製造都合で若干の小傷がある場合があります。あらかじめご了承ください。  
  
頒布基板はASCII仕様のいくつかのシェルタイプに対応していますが、  
すべてのタイプには対応していません。ご了承ください。  
  
![ケース入り](./PCB/Image3.jpg)


