---   
title:rbgioe    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# rbgioe 
Keywords  [PGM:rbgioe]

sysgui,key,template,canale,record in out,ES$,blk,eco(id+lunghezza)  
es$ in out 0=Inesistente 1=Esiste  
blk 0=read 1=extract  
p41=template  
CALL "Rbgioe",GB__SYSGUI,FLD$,"p41",C[4],TD$,ES$,BLK,"0000000"  
#######################################################################################################  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:11 in ambiente Oblivion/ECHO*
