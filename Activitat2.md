### Desactiva l’opció que ve per defecte de innodb_file_per_table

Per desactivar l'opció que ve per defecte de innodb_file_per_table haurem de afegir la línia ```innodb_file_per_table=O``` en l'arxiu ```/etc/my.cnf``` i seguidament reiniciarem el servei amb ```systemctl restart mysqld```.

Una altra opció seria executar la comanda ```SET GLOBAL innodb_file_per_table=0``` però al reiniciar el sistema aquesta opció es tornaria a activar.
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161768985-a8d674f0-cf42-423d-b0de-a4f326a0a29b.png">
</p>
<br/>

Per comprovar que està desactivada executarem la comanda ```SHOW GLOBAL VARIABLES LIKE 'INNODB_FILE_PER_TABLE'```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161769940-852eef31-cec6-4527-90d7-24282b8de7ea.png">
</p>
<br/>



### Importa la BD Sakila com a taules InnoDB. 

Importarem la BD Sakila des de el Workbench indicant que el **ENGINE** de totes les taules és igual a **ENGINE=InnoDB**

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161771136-de055ea0-e05a-431b-9c2e-937d262e9df9.png">
</p>
<br/>

### Quin/quins són els fitxers de dades? A on es troben i quin és la seva mida?

Al haver desactvar el **innodb_file_per_table**, totes les dades de les taules InnoDB, les metadates InnoDB, els buffers amb els canvis, els buffers de doble escriptura i els logs pasan a estar guardats en un arxiu InnoDB ```ibdata1``` en la ruta ```/var/lib/mysql/ibdata1```.

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161774000-9b427f5e-3a78-4c3e-a97e-910fb64ae430.png">
</p>
<br/>


Si no haguéssim desactivat el **innodb_file_per_table**, tota la infromació que es troba en l'arxiu ```/var/lib/mysql/ibdata1``` es trobarien dins de ```var/lib/mysql/sakila``` en arxius .ibd.

Com observem, en la imatge de la esquerra trobem la carpeta de **sakila** importada amb la opció **innodb_file_per_table** deshactivada, i la de la dreta amb l'opció activada. Podem diferenciar que els arxius .ibd no es troben en la imatge de la dreta perquè al importat la BD amb l'opció activada aquests arxius passen a estar dins de ```ibdata1```

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161775496-2a6d23f2-a28e-41be-a028-e1a6ea82b2f6.png">ㅤㅤㅤ
 <img src="https://user-images.githubusercontent.com/61474788/161775547-b7d985e4-065f-49dd-8fc7-5faedfdd6f69.png">
</p>





### Canvia la configuració del MySQL per:
   - **Canviar la localització dels fitxers del tablespace de sistema per defecte a /discs-mysql/**
   - **Tinguem dos fitxers corresponents al tablespace de sistema.**
   - **Tots dos han de tenir la mateixa mida inicial (10MB)**
   - **El tablespace ha de créixer de 5MB en 5MB.**
   - **Situa aquests fitxers (de manera relativa a la localització per defecte) en una nova localització simulant el següent**
   - **/discs-mysql/disk1/primer fitxer de dades → simularà un disc dur**
   - **/discs-mysql/disk2/segon fitxer de dades → simularà un segon disc dur.**

  <br/>
  
   En primer lloc, per poder canviar la configuració haurem d'aturar el sereii mysqld amb la comanda ```systemctl stop mysqld```
   

   Un cop aturat el servei, crearem el directori **/discs-mysql/** amb la comanda ```sudo mkdir /discs-mysql```.
   
   Quan tinguem creada la carpeta, li assignarem el permisos corresponents com a propietari mysql de grup i usuari amb les comandes: <br/>
   ```
   sudo chown -R mysql:mysql /discs-mysql
   sudo chmod 750 /discs-mysql/
   ```
   
   Copiarem tots els arxius de **/var/lib/mysql** en el directori **/discs-mysql**
   ```sudo cp -R -p /var/lib/mysql/* /discs-mysql```
   
   
   Modificarem l'arxiu ```my.cnf``` indicant la ruta del directori **/discs-mysql** en els paràmetres **datadir** i **socket**
   <p align="center">
    <img src="https://user-images.githubusercontent.com/61474788/161793203-76a56561-e95d-498c-ade0-9a773c146213.png">
   </p>
   <br/>
   
   Abans de tornar a iniciar el servei mysqld, executarem les següents comandes per aplicar la seguretat necessaria al nou directori **/discs-mysql**
   ```
   semanage fcontext -a -t mysqld_db_t "/discs-mysql(/.*)?"
   restorecon -R /discs-mysql
   ```
   
   Per acabar, reiniciarem el servei mysqld amb la comanda ```systemctl start mysqld``` i comprovarem que el datadir ha canviat a **/discs-mysql**
   <p align="center">
    <img src="https://user-images.githubusercontent.com/61474788/161792955-b08a5ae4-6f82-455f-ab0c-ad765221dc4a.png">
   </p>
   <br/>
   
   <br/>
   Seguidament tornarem a apagar el servei mysql amb la comanda ```systemctl stop mysql``` i crearem l'estructura dels direcotris dels discosamb les següents comandes<br/>
   
   ```
   -- Creació dels directoris
   sudo mkdir /discs-mysql/disk1
   sudo mkdir /discs-mysql/disk2
   
   -- Assignació dels permisos corresponents
   sudo chown -R mysql:mysql /discs-mysql/disk1
   sudo chown -R mysql:mysql /discs-mysql/disk2
   sudo chmod 751 /discs-mysql/disk1
   sudo chmod 751 /discs-mysql/disk2
   
   ```

<p align="center">
 <img src="">
</p>
<br/>

