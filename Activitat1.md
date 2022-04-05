#

**•	Indica quins són els motors d’emmagatzematge que pots utilitzar (quins estan actius)? Mostra al comanda utilitzada i el resultat d’aquesta.**
<br /><br />
Per saber quins motors d'emmagatzematge estan actius utilitzarem la comanda:
```
SHOW STORAGE ENGINES;
```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161563552-9bd8d06a-64a6-4d05-80b4-f39f6f7c23e5.png">
</p>
<br />


**•	Com puc saber quin és el motor d’emmagatzematge per defecte. Mostra com canviar aquest paràmetre de tal manera que les noves taules que creem a la BD per defecte utilitzin el motor MyISAM?**
<br /><br/>
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

**•	Explica els passos per instal·lar i activar l'ENGINE MyRocks. MyRocks és un motor d'emmagatzematge per MySQL basat en RocksDB (SGBD incrustat de tipus clau-valor).
Aquest tipus d’emmagatzematge està optimitzat per ser molt eficient en les escriptures amb lectures acceptables.**
<br /><br />
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
 <img src="![image](https://user-images.githubusercontent.com/61474788/161705565-13c3cec2-e453-4f7b-b239-22896fd88fa2.png)">
</p>
<br />


**•	Importa la BD Sakila com a taules MyISAM. Fes els canvis necessaris per importar la BD Sakila perquè totes les taules siguin de tipus MyISAM. 
Mira quins són els fitxers físics que ha creat, quan ocupen i quines són les seves extensions.
Mostra'n una captura de pantalla i indica què conté cada fitxer.
Un cop fet això torna a deixar el motor InnoDB per defecte.**
<br /><br />

A l'hora d'importar la BD Sakila i fer que totes les taules siguin de tipus MyISAM, haurem de canviar en totes les taules el valor **ENGINE** per ```ENGINE=MyISAM```

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161706052-834daf94-3608-4949-a498-53f08baf8b89.png">
</p>
<br />

Tots els fitxers que es generen a l'hora d'importar la BD es troben en la ruta ```/var/lib/mysql/salika```. Aquests fitxers pessen tots molts **pocs MB** i tenen les extensions **.frm**, **.TRN**, **.MYD** y **MYI**.

Cada extensió conté diferent informació relacionada amb la BD
**• .frm** contenen informació relacionada amb el format i l'estructura de la BD
**• .TRN** són copies de seguretat que s'utilitzen per restaurar la BD i per retrocedir a qualsevol estat anterior de la BD
**• .MYD** contenen informació de bases de dades i taules
**• .MDI** emmagatzemen els índexs de taules MyISAM

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

**•	A partir de MySQL apareixen els schemas de metadades i informació guardats amb InnoDB.
Busca informació d'aquests schemas. Indica quin és l'objectiu de cadascun d'ells i posa'n un exemple d'ús.**
<br /><br />
```

```
<p align="center">
 <img src="">
</p>
<br />


**•	Posa un exemple que produeix un DEADLOCK i mostra-ho al professor.**
<br /><br />
```

```
<p align="center">
 <img src="">
</p>
<br />

