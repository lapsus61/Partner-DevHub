---   
title:Mostra i dati d_out classici 09/0A in una griglia / Mostra d_out in griglia /    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Mostra i dati d_out classici 09/0A in una griglia / Mostra d_out in griglia / 
Keywords  [GRID][D_OUT][DOUT]

   
   
 Dati$ Dati griglia in formato $09/$0a completi di Header Colonna  
 D_IN$=STR(GB__SYSGUI:"0000")+STR(NRPGM_CTX:"00000")  
 D_OUT$=""                                            
 CALL "smd_win::sub_brc_grid",D_IN$,D_OUT$,DATI$          
   
   
 Mostra i dati d_out classici 09/0A in una griglia  
 Puo' essere richiamata anche da programmi carattere con un D_IN$ vuoto  
 Se HeaderColonna assenti vanno aggiunti   
  Ad esempio dati$="Key"+$09$+"Des"+$09$+"Qta"+$09$+$0a$+DatiGriglia  
  Non facendolo, la prima riga rappresentera' l'header colonne  
 [rmgsco vedi esempio][g-rmuvis child 4020 tb 2030 interessante]  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:23 in ambiente Oblivion/ECHO*
