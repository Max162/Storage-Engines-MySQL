## Documenta i posa exemple de com utilitzar ENGINE MyRocks. Crea una Base de dades amb 2 o 3 taules i inserta-hi contingut ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤCal documentar els passos que has hagut de realitzar per preparar l'exemple: configuracions, instruccions DML, DDL, etc....


En primer lloc comprovarem que tenim instal·lat el motor MyRocks
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/162014265-e0dac4d9-0632-4e5f-a946-e50b6f8b5691.png">
</p>
<br/>

Seguidament crearem una base de dades amb dues taules amb dos registres cada una

<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/162015218-312cdd0e-4cae-4d97-8477-cd6e015c6681.png">
</p>
<br/>

## A quin directori es guarden els fitxers de dades? Fes un llistat de a on són els fitxers i què ocupen.

Els fitxers es guardaran en la ruta ```/var/lib/mysql/db_rocks``` i estaran en format **.frm**.
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/162015938-c8612d50-f361-4f2c-bf79-18bc9607707a.png">
</p>
<br/>

## Quina és la compressió per defecte que utilitza per les taules? Com ho faries per canviar-lo. Per exemple utilitza Zlib o ZSTD o sense compressió


Per saber la compressió que que utilitzen els taules per defecte executarem la comanda:

```SELECT * FROM information_schema.rocksdb_cf_options WHERE option_type LIKE '%compression%' AND cf_name='default'```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/162017197-bd0a2221-0dca-4166-8fa4-fb20d7eee841.png">
</p>
<br/>
