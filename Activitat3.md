### Partint de l'esquema anterior configura el Percona Server perquè cada taula generi el seu propi tablespace en una carpeta anomenada tspaces (aquesta pot estar situada a on vulgueu).
### Indica quins són els canvis de configuració que has realitzat.

En primer lloc pararem el servei mysqld amb la comanda ```systemctl stop mysqld``` i seguidament documentarem la variable ```innodb_file_per_table=0``` en l'arxiu ```my.cnf``` per activar el **innodb_file_per_table**.

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161958324-f1c70d7a-7dfc-40fd-8b0b-4eccca08e99b.png">
</p>
<br/>

A continuació crearem el directori **tspaces** amb els seus respectius permisos d'usuari i grup al usuari mysql i copiarem el contingut de la ruta ```/var/liv/mysql``` dins del nou directori ```/tspaces```

```
-- Creació del directori i assiganció dels permisos
sudo mkdir /tspaces
sudo chown -R mysql:mysql /tspaces
sudo chmod 751 /tspaces

-- Copia del directori /var/lib/mysql (o el /discs-mysql pequè tenen el mateix) al /tspaces
sudo cp -R -p /var/lib/mysql/* /tspaces
```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161953376-41651389-ce9d-47c5-88d8-b6b2248d3058.png">
</p>
<br/>

Modificarem l'arxiu ```my.cnf``` indicant la ruta del directori **/tspaces** en els paràmetres **datadir** i **socket**
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161954233-75c8bd66-5c07-4058-b702-d71e52d9c683.png">
</p>
<br/>

Abans de tornar a iniciar el servei mysqld, executarem les següents comandes per aplicar la seguretat necessaria al nou directori /tspaces
```
semanage fcontext -a -t mysqld_db_t "/discs-mysql(/.*)?"
restorecon -R /discs-mysql
```
<br/>

Per finalitzar tornarem a iniciar el servei mysql amb la comanda ```systemctl start mysqld``` i seguidament comprovarem que el **datadir** ha canviat a **tspaces**
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161959026-37d0091a-c95c-4134-ba00-8d09adc68b0f.png">
</p>
<br/>
