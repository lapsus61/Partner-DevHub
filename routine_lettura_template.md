---   
title:Routine lettura template    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Routine lettura template 
Keywords  [smd_tmp[[TMP][FAST][SIMPLE]

   
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
VERSIONE RIDOTTA   
 call "smd_tmp::simple","keytmp","rectmp","keytfil"  
 >Enter  
 keytmp  key della template interessata  
 >Out   
 rectmp  template dimensionata  
 keytfil  key tfil del file collegato  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
VERSIONE ESTESA   
 call "smd_tmp","keytmp","rectemp","descrizione","tiporecord","pgmlink","Mnemonico","keytfil","null1","null2"  
 >Enter  
 keytmp  key della template interessata  
 >Out   
 rectmp  template dimensionata  
 descrizione Descrizione  
 tiporecord  Valore tipo record  
 pgmlink  Programma di gestione   
 Mnemonico Variabile mnemonica  
 keytfil  key tfil del file collegato  
   
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:22 in ambiente Oblivion/ECHO*
