### Crea un tablespace anomenat 'ts1' situat a /discs-mysql/disc1/ i col·loca les taules actor, address i category de la BD Sakila.

Crearem un nou tablespace indicant el seu **ENGINE** com a **InnoDB** i indicant la ruta on guardara els arxius en ```/discs-mysql/disk1/ts1.ibd```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161962966-31b77269-005d-4640-9322-05aa1f2d7faa.png">
</p>
<br/>

Comprovarem que el tablespace s'ha creat correctament si s'ha creat un arxiu **ts1.ibd** en la ruta ```/discs-mysql/disk1/```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161964764-9a94af13-a5dd-4245-a20a-4c2d204dea20.png">
</p>
<br/>


### Crea un altre tablespace anomenat 'ts2' situat a /discs-mysql/disc2/ i col·loca-hi la resta de taules.

Crearem un nou tablespace indicant el seu **ENGINE** com a **InnoDB** i indicant la ruta on guardara els arxius en ```/discs-mysql/disk2/ts2.ibd```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161965481-71b4620c-4fcb-466b-9e7f-8da20bdf2444.png">
</p>
<br/>

Comprovarem que el tablespace s'ha creat correctament si s'ha creat un arxiu **ts2.ibd** en la ruta ```/discs-mysql/disk2/```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161965801-30580483-9657-4a71-bee4-171fd0260452.png">
</p>
<br/>


### Comprova que pots realitzar operacions DML a les taules dels dos tablespaces.

Comprovarem que podem realitzar operacions DML en el tablespace de ```ts1```.
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161967223-ee280c71-e84b-4152-81ac-5874d1241f72.png">
 <img src="https://user-images.githubusercontent.com/61474788/161967295-0593e93a-bbb0-42b4-a1f4-fb0384c344a7.png">
</p>
<br/>

Comprovarem que podem realitzar operacions DML en el tablespace de ```ts2```.
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161968050-f6035c93-ef8d-47ec-a76e-36dd63c6ad1d.png">
 <img src="https://user-images.githubusercontent.com/61474788/161968087-26a47ab3-6c21-4d68-97c9-28339b31b7f4.png">
</p>
<br/>


