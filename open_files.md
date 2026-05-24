---   
title:Open files    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Open files 
Keywords  [smd_opn][standard][tfil][provvisori]MAG][INI][smd_opn]

   
-----------------------------------------------------------------------------------------------------------------------------------------------------------   
OPEN FILE  
 CALL "smd_opn","keytfil",canale  
 Esegue la open del file keytfil e restituisce in 'canale' il numero di canale utilizzato   
   
-----------------------------------------------------------------------------------------------------------------------------------------------------------  
OPEN FILE NON PRESENTE IN TFIL  
 call "smd_opn::sub_open_org","nomefile",canale  
 >Enter  
 nomefile  nome del file da aprire cui saranno aggiunti org e rifsoc :: ..  
 canale  numero canale sul quale si vuole aprire il file (vedi out)  
 >Out  
 canale  se in ingresso canale contiene -1, contiene il numero canale su cui il file e' stato aperto.  
-----------------------------------------------------------------------------------------------------------------------------------------------------------   
OPEN FILE ORDINI PROVVISORI   
 call "smd_opn::SUB_OPEN_P",D_IN$,D_OUT$,C40,C40A,C40B  
 Esegue la open del file ordini provvisorio rfor:.P  
   
 >Enter   
 E' necessario che sul canale 740 sia aperto il file degli ordini  
 >Out  
 Chiude il file ordini su 740 e apre il file rfor::P su 740,c40,c40a,c40b  
   
 call "smd_opn::SUB_RESTORE_P",D_IN$,D_OUT$,C40,C40A,C40B  
 Ripristina il file ordini standard rfor::  
   
-----------------------------------------------------------------------------------------------------------------------------------------------------------   
OPEN FILE PARAMETRI MOVIMENTI DI MAGAZZINO  
   
 call "rmamvx::sub_open_file_rmemvx.ini","",d_out$; c_txt=num(d_out$)  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:22 in ambiente Oblivion/ECHO*
