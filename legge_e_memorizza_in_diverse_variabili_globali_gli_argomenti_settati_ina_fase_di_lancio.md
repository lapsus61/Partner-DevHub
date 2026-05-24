---   
title:Legge e memorizza in diverse variabili globali gli argomenti settati ina fase di lancio    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Legge e memorizza in diverse variabili globali gli argomenti settati ina fase di lancio 
Keywords  [STBL][ARGV]

   
   
 rbgset::SUB_SET_ARGV  
 Legge e memorizza in diverse variabili globali gli argomenti settati ina fase di lancio [STBL][ARGV][ARGOMENTI]  
   
 C:\Basis223\VPRO5\vpro5.exe -q -m100000 -tT0 -nT0 -c\\varius\usb\d-zip\rps_ds\configds.bbx g-dmnBKS - null soc:05  
Primo elemento contiene solo l'organizzazione. inserire 'null' nel caso l'installazione non la preveda  
- "o2b_org" Organizzazione  
Il secondo elemento puo' essere composto da diversi argomenti nella forma <mne><:><argomento><;>. I mnemonici sono  
   
Tabella Mne  
   
| Mne | Variabile stbl di destinazione  | Contenuto |  
| ------ | ------------------------------------- | -------------- |   
| soc | ps_argsoc | Codice Socio |  
| usr | ps_argusr | User |  
| pwd | ps_argpwd | Password |  
| gcp | ps_arggcp | Gruppo di capacita' |  
| pgm | ps_runpgm | Programma da eseguire |  
| cfg | ps_argcfg | File di configurazione |  
| log | ps_arglog | Log |  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*
