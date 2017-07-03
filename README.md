# Planificación - ReanEmu 2.4.3 - The Burning Crusade

La planificación y organización del equipo de desarrollo es la primera
línea ante un proyecto que está en constante cambio e involucra el esfuerzo
de muchas personas. Se ha establecido una metodología basada en hitos
o milestones para dividir e identificar las grandes áreas de desarrollo
con el objetivo de mantener un proyecto legible y que brinde trazabilidad
con un mínimo de esfuerzo.

## Organización del trabajo


### Milestones

-El repositorio no puede ser un desorden por lo que se fijarán metas concretas en 7 MILESTONES:

|   Milestone   | Description |
| ------------- | ----------- |
| Milestone 0.0 | -- Características principales y adicionales para el
 emulador
| Milestone 1.0 | -- Jugabilidad en general, adecuaciones de código
vario en mapascomportamiento de bgs, arenas, players-units-pets y mejoras.
| Milestone 2.0 | -- Mejoras en Instances y dungeons, escencialmente
para darles funcionalidad y detalles para tenerlas lo mas cercano a
blizzlike, solucion de bugs relativos a las mismas, implementacion de
} nuevas scripts.
| Milestone 3.0 | -- Arreglos a Spells, sobre todo para estabilidad
del pve y del pvp dentro de los reinos.
| Milestone 4.0 | -- Arreglos en quests, y cadenas de misión, esto
incluye scripts en c++ y SmartAI.
| Milestone 5.0 | -- Traducciones, e inclusión de varios dentro de
tablas y strings del emulador, ya sea en c++ o en sqls.
| Milestone 6.0 | -- Arreglos en eventos de mundo, logros y varios,
con SAI, c++ y sql para items, criaturas, spells, etc.Que no encajen
en las demas milestones.
| Milestone 7.0 | -- Código custom, utilitario y caracteristicas
interesantes varias.

### Descripción Milestones

Dentro de cada milestone hay una subdivision que ha de respetarse adicionalmente al
criterio unificado de que debe ir dentro de cada numeracion y como debe hacerse, es por
ello que detallaremos esta parte:

== Milestone2.0: ==

- Raids -
- Dungeons -

== Milestone3.0: ==

3.1 - Druid
3.2 - Hunter
3.3 - Mage
3.4 - Paladin
3.5 - Priest
3.6 - Rogue
3.7 - Shaman
3.8 - Warlock
3.9 - Warrior
3.10 - Trinkets
3.11 - Special

== Milestone4.0: ==

4.0 - Misiones de clases
4.1 - Especiales: acá van misiones especiales que no estén asociada a una zona en específico
4.2 - Kalimdor y Reinos del Este
4.3 - Terrallende


### Commits

Cada COMMIT se escribirá por cada una de los cambios mínimos que hagan referentes al mismo
milestone-tema y se clasificarán también con una estructura para que asemeje a un solo 
tópico en concreto:

MilestoneNumero Nombre: Descripción
--------------- ------- -----------
"2.X Instance: Boss texto, ids o sql"   -> 2.20.15 TheOculus: Eregos some tweaks
"3.X Clase: Texto e ID"                 -> 3.51 DK: Raise ally (61999)
"4.X Zona: Quest texto script ID o sql" -> 4.8.36 Tundra Boreal: Fix for quest Drake Hunt
"7.X Custom: texto explicativo"         -> 7.11 Custom: Gs Command implementation

Los nombres de archivos que describan los cambios en sql, serán sin espacios, 
solo guiones bajos son aceptados y se ajustarán a la cronología en la carpeta /reanemu, 
ya sea en mangos, characters o realm de acuerdo a lo que corresponda cada query o grupo en 
concreto asi:

año_mes_dia_numero mayor a 100_carpeta_texto_explicativo.sql
----------- ------------------ ------- -------------------------------
2011_09_01_100_world_wintergrasp_turrets.sql
2012_07_14_100_characters_history.sql
2009_01_26_100_auth_premium.sql

Ojo, siempre igual a cien, para diferenciarlos de cualquier otro sql, incluyendo los de tc.

Para el CHANGELOG también hemos de añadir esta información de manera que siempre tengamos 
documentado algun cambio por fecha y quien lo hizo, de este modo si se depreca o se lo 
vuelve a incluir en la branch principal, no se pierda y no haya informacion variante 
durante el proceso de desarrollo, y se hará así:

MilestoneNumero - Fecha: NombreFeature: Descripcion por Autor
---- --------- --------- -----------------------
0.19 - 19/04/2012: SOAP server information commands por Eilo
1.3  - 05/10/2011: Join LFG channel without being on a city por Opcode187
2.2.89 - 06/08/2012: ICC: TheLichKing temp fix to height issues by Jildor
3.71 - 18/07/2012: Shaman: Grounding totem (8177) also absorbs polymorph effect por Vincent-Michael
4.9.8  - 04/10/2012: Howling Fjord: Scare the guano out of them! por Muzashi

Otra cosa que hay que tomar en cuenta es el hecho de que si algo es de código de otra 
persona  o equipo de personas en concreto hay que mencionarlo, y si nosotros hacemos 
algo de lo que no haya referencias previas, añadir el copyright de cada uno individualmente 
y el de ReanEmu,  sobre todo si en una script se le ha hecho mejoras notables y de peso.

 * Copyright (C) 2008-2012 cMANGOS <https://github.com/cmangos/>
 * Copyright (C) 2010-2012 WoWRean <http://www.wowrean.es/>
 * Copyright (C) 2009-2012 Eilo <https://github.com/eilo/>



### Workflow

Nos basaremos en el juego que nos dan las branches para organizar adecuadamente el 
desarrollo y en las pull requests, cuando sea necesario, provenientes de los forks 
privados del equipo. 

Siempre habrá 2 branchs fijas en el repositorio: Compilado y Dev.


### Branch Compilado

Compilado es considerada un retail. Aquí estarán todos los commits que se hayan seleccionado 
para entrar en producción. Será una branch que se tocará sólo cuando se va a actualizar 
producción siguiendo este proceso: 

1. Se hace el reset necesario para poder actualizar la revisión base, elegida en función 
   de estos tres parámetros: 

              | usabilidad | <---> | estabilidad | <---> | jugabilidad |

2. Se hace reset a esa rev de tc.

3. Se aplican los parches de los commits seleccionados de Rean y serán aplicados 1 a 1 
   siguiendo el orden de las milestones prefijadas.

4. Finalmente, se indicará el uptime medio alcanzado con la última rev así como el número
   de pjs.

De esta manera tendremos una branch siempre limpia y organizada de manera que sea fácil 
consultar todo lo que contiene actualmente producción.



### Branch Dev

La branch dev será donde el equipo de desarrollo trabajará de forma oficial. Aquí se 
pushearan todos los commits que posteriormente entrarán a formar parte de Master. 

Esta branch debe estar lo más limpia posible, evitando  reverts y typos innecesarios. 
Además esta branch siempre debe ser funcional para los testeos lo que significa que debe 
ser compilable todo el tiempo. 

Esencialmente es una branch de trabajo donde se irá progresando en el desarrollo del 
emulador a lo largo del tiempo entre cada actualización.



### Forks y Otras Branchs

Los forks se usarán como cada uno quiera. Su principal función será la de hacer pull 
request de una determinada feature/commit para que así los demás miembros del equipo de 
desarrollo puedan opinar sobre éste y si es necesario hacer las correcciones pertinentes 
antes de ser mergeado a dev.

Si es necesario se pueden crear branchs para desarrollar determinadas features o que aún 
están demasiado verdes como para entrar a producción. Por ej. se podría crear una branch 
para contener los mmaps y según Venugh lo vaya desarrollando ir haciendo merge y testeando.



### Consideraciones a tener en cuenta

1. Siempre se commiteará cada acción con un commit individual por mas pequeño que sea. Dado 
   que en algún momento se necesita revertir, por que no funcione bien o porque tc lo arreglase
   en algún momento.

2. Se mantendrá el codestyling de espacios en blanco con espaciadora, nunca con tabs en el 
   código o el emulador pierde condescendencia y también porque tc mantiene estas reglas 
   básicas para coding.

3. Siempre se comunicara al resto de devs que es lo que se esta haciendo y se tendrá claro 
   siempre los repos que a cada uno se le ha asignado. Si algún commit tiene referencia a 
   alguno de los repos de otro dev, es imprescindible comunicarlo.

4. Se depreca el cherry pick por razones de conflictos anteriores, y se lo permitirá únicamente
   con un commit contemporáneo, es decir que no supere 1 día atrás de la revisión punta (head) 
   que tengamos nosotros.


El proceso en general se lograra hacer mas llevadero y sobre todo nos ayudara para alcanzar
esta meta inmensa como equipo de desarrollo de ReanEmu.


Saludos
Staff Developers WoWRean

