
### **Indica quins són els motors d’emmagatzematge que pots utilitzar (quins estan actius)? Mostra al comanda utilitzada i el resultat d’aquesta.**
Per saber quins motors d'emmagatzematge estan actius utilitzarem la comanda:
```
SHOW STORAGE ENGINES;
```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161563552-9bd8d06a-64a6-4d05-80b4-f39f6f7c23e5.png">
</p>
<br />


### **Com puc saber quin és el motor d’emmagatzematge per defecte. Mostra com canviar aquest paràmetre de tal manera que les noves taules que creem a la BD per defecte utilitzin el motor MyISAM?**
Per saber quin és el motor d'emmagatzematge per defecte ens haurem de fixar en el valor **Support** de la consulta anterior.

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161565089-13b787ef-b673-4384-860a-41620b70f2ed.png">
</p>

Per fer que les noves taules que creem a la BD per defecte utilitzin el motor MyISAM afegirem la següent línia en l'arxiu ```/etc/my.cnf``` perquè a cada inici de sessió es carregui el motor MyISAM per defecte.<br/>
També serveix executar la comanda segona comanda en el mysql però quan tanquem la sessió MyISAM deixarà de ser el motor per defecte.
```
mycnf ➜ default-storage-engine=MyISAM

mysql ➜ SET DEFAULT_STORAGE_ENGINE=MyISAM
```

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161568687-2be849d8-c9e9-4ae0-9b1f-f5d4d2982bea.png">
</p>
<br />

Comprovarem que el motor per defecte és MyISAM amb la comanda **SHOW ENGINE**

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161704805-623c0cae-6c91-46bc-bf0e-04fe639dbc98.png">
</p>
<br />

### **Explica els passos per instal·lar i activar l'ENGINE MyRocks. MyRocks és un motor d'emmagatzematge per MySQL basat en RocksDB (SGBD incrustat de tipus clau-valor). Aquest tipus d’emmagatzematge està optimitzat per ser molt eficient en les escriptures amb lectures acceptables.**

En primer lloc instal·larem el paquet del MyRocks
```
sudo yum install Percona-Server-rocksdb-57
```

Un cop instal·lat el paquet, l'activarem amb la següent comanda indicant el nostre usuari i password
```
ps-admin --enable-rocksdb -u max -pP@ssw0rd
```

Comprovarem que s'ha instal·lat correctament el MyRocks al veure que s'ha creat el seu storage engine
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161705565-13c3cec2-e453-4f7b-b239-22896fd88fa2.png">
</p>
<br />


### Importa la BD Sakila com a taules MyISAM. Fes els canvis necessaris per importar la BD Sakila perquè totes les taules siguin de tipus MyISAM. Mira quins són els fitxers físics que ha creat, quan ocupen i quines són les seves extensions. Mostra'n una captura de pantalla i indica què conté cada fitxer. Un cop fet això torna a deixar el motor InnoDB per defecte.

A l'hora d'importar la BD Sakila i fer que totes les taules siguin de tipus MyISAM, haurem de canviar en totes les taules el valor **ENGINE** per ```ENGINE=MyISAM```

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161706052-834daf94-3608-4949-a498-53f08baf8b89.png">
</p>
<br/>

Tots els fitxers que es generen a l'hora d'importar la BD es troben en la ruta ```/var/lib/mysql/salika```. Aquests fitxers pessen tots molts **pocs MB** i tenen les extensions **.frm**, **.TRN**, **.MYD** y **MYI**.

Cada extensió conté diferent informació relacionada amb la BD<br/>
   - **.frm** contenen informació relacionada amb el format i l'estructura de la BD<br/>
   - **.TRN** són copies de seguretat que s'utilitzen per restaurar la BD i per retrocedir a qualsevol estat anterior de la BD<br/>
   - **.MYD** contenen informació de bases de dades i taules<br/>
   - **.MDI** emmagatzemen els índexs de taules MyISAM<br/>

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161708942-789457fb-c6cb-4339-93b4-544a236a2827.png">
</p>
<br />

Per deixar un altre cop el motor InnoDB per defecta descomentarem la línia **default-storage-engine** afegida anteriorment i reiniciariem el servei ```systemctl restart mysqld```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161712287-42da356b-15f7-49bc-8ee3-fa5d504a0412.png">
</p>
<br />

Tornaríem a tenir el motor InnoDB per defecte
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161712595-24ce2310-32ea-46fd-b941-cce864395aed.png">
</p>
<br />

### **A partir de MySQL apareixen els schemas de metadades i informació guardats amb InnoDB. Busca informació d'aquests schemas. Indica quin és l'objectiu de cadascun d'ells i posa'n un exemple d'ús.**
L'esquema que ens proporciona una fomra d'accedir a les metadades de les bases de dades és el  ```INFORMATION_SCHEMA```, una BD que ve incorporada amb el MySQL, la qual ens permet extreure i consultar metadades sobre els objectes d'esquema administrats per InnoDB utilitzant les taules del sistema del ```INFORMATION_SCHEMA```.

Per consultar les taules executarem del ```INFORMATION_SCHEMA``` executarem:
```
mysql> SHOW TABLES FROM INFORMATION_SCHEMA LIKE 'INNODB_SYS%';
+--------------------------------------------+
| Tables_in_information_schema (INNODB_SYS%) |
+--------------------------------------------+
| INNODB_SYS_DATAFILES                       |
| INNODB_SYS_TABLESTATS                      |
| INNODB_SYS_FOREIGN                         |
| INNODB_SYS_COLUMNS                         |
| INNODB_SYS_INDEXES                         |
| INNODB_SYS_FIELDS                          |
| INNODB_SYS_TABLESPACES                     |
| INNODB_SYS_FOREIGN_COLS                    |
| INNODB_SYS_TABLES                          |
+--------------------------------------------+
```

L'objectiu de cada una d'aquestes taules és:<br/>
   - **```INNODB_SYS_DATAFILES```** facilita informació de la ruta de l'arxiu de dades per espais tant de tables generals com d'arxiu per taula de InnoDB<br/>
   - **```INNODB_SYS_TABLESTATS```** facilita informació del estat de baix nivell sobre les taules InnoDB que es deriva de les estructures de dades de memòria<br/>
   - **```INNODB_SYS_FOREIGN```** facilita metadades sobre les claus externes en definides en les taules de InnoDB<br/>
   - **```INNODB_SYS_COLUMNS```** facilita metadades sobre les columnes de la taula InnoDB<br/>
   - **```INNODB_SYS_INDEXES```** facilita metadades sobre els índexs de InnoDB<br/>
   - **```INNODB_SYS_FIELDS```** facilita metadades sobre les columnes clau dels índexs de InnoDB<br/>
   - **```INNODB_SYS_TABLESPACES```** facilita metadades tant sobre l'arxiu per taula com d'espai de taules generals de InnoDB<br/>
   - **```INNODB_SYS_FOREIGN_COLS```** facilita metadades sobre les columnes de claus externes que es definiexen en les taules InnoDB<br/>
   - **```INNODB_SYS_TABLES```** facilita metadades sobre les taules InnoDB<br/>

**Exemples d'us:**<br />
No he realitzat exemples de totes les maneres d'accedir a les metadades utilitzant les taules del ```INFORMATION_SCHEMA``` perquè les consultes són ben bé iguals i només canvia el nom de la taula del ```INFORMATION_SCHEMA```.<br />

Executarem la següent comanda per obtenir les metadades de la taula **film_text** de la BD de sakila i aquesta ens donarà informació a nivell de bits sobre el format de la taula, les caraterístiques d'emmagatzematge, el ID, etc...
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161720650-59e20e65-8745-435f-8169-1d49530ccfef.png">
</p>
<br/>

Seguidament, amb la següent consulta, obtindrem les metadades de les columnes de la mateixa taula anterior a través del seu ID i aquesta ens proporcionara informació concreta de cada columna, com la posició ordinal de cada columna, el seu tipus, el codi del conjunt de caràcters, etc...
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161720769-7f8bc77a-3fde-47a9-9d94-861661c71156.png">
</p>
<br/>

En la <a href="https://dev.mysql.com/doc/refman/5.7/en/innodb-information-schema-system-tables.html">documentació oficial de InnoDB INFORMATION_SCHEMA System Tables</a> trobarem exemples de tot tipus
<br /><br/>

### **Posa un exemple que produeix un DEADLOCK i mostra-ho al professor.**
Seguint la documentació oficial del InnoDB DEADLOCK, trobem el següent exemple que explica clarament el seu funcionament.

En primer lloc, el client A, crearà una taula amb una taula i seguidament iniciarà una transacció d'un SELECT.
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161723476-2ca58998-253f-43f0-94b4-80dce15e0353.png">
</p>
<br />

A continuació, el client B, obre una transacció i intenta eliminar la fila de la taula on el client A també esta realitzant una transacció
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161725587-931cb701-14e7-4ae3-8de2-656e2fdcf39a.png">
</p>
<br />

Com observem, es produeix un error perquè el client B vol realitzar una transacció sobre unes dades que ja estàn sota una transacció del client A. Aixó es fa perquè no hi hagi inconsistencia en les dades, ja que si dos clients estuguessin consultant i modificant dades al mateix temps, podríen estar canviant modificar dades que en aquell mateix moment necessita un altre client. D'aquesta forma amb el DEADLOCK, si un client obre una transacció, cap altre client podrà ralitzar transaccions sobre una taula que ja tingui una transacció activa.
