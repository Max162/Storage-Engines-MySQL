## Com podem comprovar (Innodb Log Checkpointing):

Amb la comanda ```SHOW ENGINE INNODB STATUS``` comprovarem el Log Checkpointing
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161983732-9831f043-6aaf-4658-a078-c586dd5d2d2e.png">
</p>
<br/>

## LSN (Log Sequence Number)

Trobarem el **LSN** en l'apartat de LOG
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161984369-2a0bdbb3-b413-458d-91f1-34181bb16888.png">
</p>
<br/>

## L'últim LSN actualitzat a disc

L'útlim **LSN** actualitzat és:
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161984940-5ff9e2ea-9b4f-4d2f-8db1-0bf8d374ad14.png">
</p>
<br/>

## Quin és l'últim LSN que se li ha fet Checkpoint

L'últim **LSN** que se li ha fet Checkpoint és:
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161985535-9361503d-bbe9-4fa7-b7e5-e6b437f8fea6.png">
</p>
<br/>

## Proposa un exemple a on es vegi l'ús del redolog


```

```
<p align="center">
 <img src="">
</p>
<br/>

## Com podem mirar el número de pàgines modificades (dirty pages)? I el número total de pàgines?

Trobarem el número de pàgines modificades i el total de pàgines en l'apartat **BUFFER POOL AND MEMORY** al executar la comanda ```SHOW ENGINE INNODB STATUS```
<p align="center">
 <img src="https://user-images.githubusercontent.com/61474788/161986318-3367b369-da58-42ae-898a-f5c5ce1d7b8f.png">
</p>
<br/>
