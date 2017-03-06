#Sellstation Core

##Changelog
##### Revision 1.0.9 - 06/03/2017
 - Sincronización de Journal Local+Remoto
 - Agregado parámetro ignoreBackgroundColors
 - Agregado parámetro debugEnabled
 - Agregado parámetro forzarJournalLocal

## Parámetros de Sellstat.ini
#### Ignore Background Colors  
Obliga al core a ignorar el color de fondo asignado a las ventanas de Sellstation.
```ini
[SELLSTAT]
ignoreBackgroundColors=0|1
```

#### Debug Enabled
Habilita la ventana de Debug cuando en un scriplet se ingresa la instrucción Debug
```ini
[SELLSTAT]
debugEnabled=0|1
```
**Nota:** De ahora en más, si no está habilitado este parámetro, la ventana de debug que siempre se utilizó no aparece (se ignora la instrucción debug en el scriptlet).

#### Forzar Journal Local
Fuerza al core a trabajar solo con el journal local.
```ini
[SELLSTAT]
forzarJournalLocal=0|1
```
**Nota:** Este parámetro fue creado para realizar las pruebas de sincronización de journal para la revisión 1.0.9.


