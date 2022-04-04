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
<br /><br />
Per saber quin és el motor d'emmagatzematge per defecte ens haurem de fixar en el valor **Support** de la consulta anterior.

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161565089-13b787ef-b673-4384-860a-41620b70f2ed.png">
</p>

Per fer que les noves taules que creem a la BD per defecte utilitzin el motor MyISAM afegirem la següent línia perquè a cada inici de sessió es cargui el motor MyISAM per defecte.
```
default-storage-engine=MyISAM
```
També serveix executar la comanda **SET DEFAULT_STORAGE_ENGINE=MyISAM** pero quan tanquem la sessió MyISAM deixarà de ser el motor per defecte.

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161568687-2be849d8-c9e9-4ae0-9b1f-f5d4d2982bea.png">
</p>
<br />


**•	Explica els passos per instal·lar i activar l'ENGINE MyRocks. MyRocks és un motor d'emmagatzematge per MySQL basat en RocksDB (SGBD incrustat de tipus clau-valor).
Aquest tipus d’emmagatzematge està optimitzat per ser molt eficient en les escriptures amb lectures acceptables.**
<br /><br />
```

```
<p align="center">
 <img src="">
</p>
<br />


**•	Importa la BD Sakila com a taules MyISAM. Fes els canvis necessaris per importar la BD Sakila perquè totes les taules siguin de tipus MyISAM. 
Mira quins són els fitxers físics que ha creat, quan ocupen i quines són les seves extensions.
Mostra'n una captura de pantalla i indica què conté cada fitxer.
Un cop fet això torna a deixar el motor InnoDB per defecte.**
<br /><br />
```

```
<p align="center">
 <img src="">
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

