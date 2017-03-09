# Sellstation Core

## Tabla de contenidos
1. Changelog
2. Sellstation.log
3. Parámetros de Sellstat.ini
4. Sincronización de Journals

## 1. Changelog
##### Revision 1.0.9 - 06/03/2017
 - Sincronización de Journal Local+Remoto
 - Agregado parámetro ignoreBackgroundColors
 - Agregado parámetro debugEnabled
 - Agregado parámetro forzarJournalLocal
 - Limpieza general de logs antiguos

## 2. Sellstation.log
Es el log del core que contiene todo tipo de información referente al mismo. Es creado la primera vez que abrimos Sellstation, y en caso de que sea mayor a 5mb, se copia a un archivo historico y se limpia.  
Se encuentra estructurado de la siguiente forma:  
>20170306-154743 [INF] SELLSTATION Application Start  
>YYYYMMDD-HHMMss [Tipo] Información

#### Tipos de Log
- **Info [INF]: ** Mensajes informativos.
- **Warning [WAR]: ** Mensajes de alerta.
- **Error [ERR]: ** Mensajes de error graves (importante para analizar crashes).
- **Window [WND]: ** Eventos de los dialogos.
- **Journal [JOU]: ** Eventos de journal.
- **Scriplet [SCP]: ** Mientras está activado escribe cada instrucción que corre en el log (**cuidado**, genera mucha cantidad de log y hace que Sellstation funcione mas lento).
- **Dialogs [DLG]: ** Eventos de apertura + cierre de diálogos.
- **DDs Read [DDR]: ** Eventos de lectura en DDs.
- **DDs Write [DDW]: ** Eventos de escritura en DDs.
- **Device [DVC]: ** Eventos de dispositivos.
- **Journal Sync [JSC]: ** Eventos de sincronización de journal.

**Nota:** Los diferentes tipos de logs son habilitados y deshabilitados a medida que sea necesario utilizarlos. Por default se encuentran habilitados INF,WAR,ERR y JSC.

#### Habilitar tipos de log por diálogos
Existe la posibilidad de habilitar uno de los tipos de log para un dialogo y los dialogos a los que llame el dialogo seleccionado. Esta herramienta se puede utilizar para **monitorear el comportamiento** del core.  
**No necesita reiniciar Sellstation** para habilitar/deshabilitar, aunque debe asignarse antes de abrir el dialogo.
Esto se logra de la siguiente forma:
```ini
[Logger]
DIALOGO=TIPO1,TIPO2,TIPO3
TL0431=SCP,DDW,DVC
```
**Nota: **Para investigar un crash, podemos utilizar el log de SCP para poder ver el último comando que corrio el core.  
**Nota 2: **Dependiendo de cuantos logs sean habilitados, Sellstation puede funcionar mas lento (la lentitud solo es notable para el log SCP).

#### Información importante que encontramos en el Log

- Inicio + Cierre de la aplicación
>20170306-154743 [INF] SELLSTATION Application Start  
>20170306-154743 [INF] Sellstation no cerro correctamente.  
>20170306-164235 [INF] SELLSTATION Exiting...

- Versión + Revisión del Core
>20170306-152120 [INF] Version 3.5.0 Rev 1.0.8k [RELEASE]  
>20170306-152120 [INF] Version 3.5.0 Rev 1.0.9dev [DEBUG]

- Estados del Logger
>20170306-154743 [INF] Logger [INF] enabled  
>20170306-154743 [INF] Logger [SCP] disabled

- SUIT Actual
>20170306-154743 [INF] Loading suit **C:\SSCAJA**

- Usuario, OpNum, Acceso
>20170306-154747 [INF] Teller **B035460** OpNum **103** Access **249**

- Utilización de aplicaciónes externas
>20170306-174032 [INF] WinExec: C:\Sellstat\SellStationSyncService\SincronizadorDeImagenes.exe

- Parámetros de Sellstat.ini habilitados
>20170306-153745 [INF] Parametro "HostSimMode" habilitado.
>20170306-153745 [INF] Parametro "ignoreBackgroundColors" habilitado.  
>20170306-153745 [INF] Debug para dialogos habilitado.  
>20170306-153746 [INF] Forzando a utilizar journal local.

- Exceptions
>20170307-104051 [INF] Exception MFC-DoCommand(Clearfield (dd[TEMP.AcctType[0]]))

## 3. Parámetros de Sellstat.ini
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

## 3. Sincronización de Journals
#### Problematica
Sellstation actualmente abre en caso de ser posible, un journal **local** y uno **remoto** ubicado en el **servidor F**. En el caso de no poder conectarse al servidor, trabaja solo con el journal local, de manera transparente para el usuario.  
Se daba la problemática que, cuando se **perdía conexión** con el servidor F, Sellstation continuaba su funcionamiento normalmente, con la diferencia de que **solo escribía journal localmente**. Cuando se reestablecia la conexión, se volvia a escribir en ambos, **sin hacer ningún tipo de copia o sincronización**, dejando operaciónes solo en el journal local. Cuando se volvia a abrir Sellstation, el journal local era reemplazado por el remoto (por comparación de fechas), **perdiendo las operaciónes** que estaban escritas solo en el journal local.

#### Solución
1000
837035
universal assistance
0800-222-8565