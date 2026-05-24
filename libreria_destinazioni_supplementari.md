---   
title:Libreria destinazioni supplementari    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria destinazioni supplementari 
Keywords  [SIC][IS][CTR][DEST]

--  
  
## Primo contatore libero  
 call "omiiis::SUB_NEW_CTR_IS"  
  
## Accesso esterno alla gestione  
 dim gb__arg$:"key:c(5),gest_is:c(1)"  
 gb__arg.key$=str(num(sendmsg(gb__sysgui,1015,20,0,$$)):"00000")  
 gb__arg.gest_is$="Y"  
 call "g-rpgana",gb__arg$  
  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
