---   
title:Restituisce il valore contenuto in una cella MNE    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Restituisce il valore contenuto in una cella MNE 
Keywords  [GRIGLIA]

   
 10/12/2025  
 Utilizzare smdVmgd::SUB_GET_ROWCOL  
 piu' completa e con gestione trasparente delle griglie DatiD  
-----------------------------------------------------------------------------------------------------  
versione precedente  
 Restituisce il valore contenuto in una cella MNE [GRIGLIA]  
 call "sm2_utl::SUB_FIND_MNE"  
-------------------------------------------------------------------------------------------------------------  
## GET NUMERO COLONNA MNE  
 Restituisce il NUMERO della colonna puntata da mne                                        
   
 Esempio per griglia 1  
 call "sm2_utl::SUB_FIND_MNE_COL",psg_gdat1$[ALL],psg_gchd1$[ALL],psg_gcps1$[ALL],0,gar_dat[1,4],"DocConsegna",D_OUT$                                           
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
