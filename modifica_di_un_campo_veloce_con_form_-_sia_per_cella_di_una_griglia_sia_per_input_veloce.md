---   
title:Modifica di un campo veloce con form - Sia per cella di una griglia sia per input veloce    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Modifica di un campo veloce con form - Sia per cella di una griglia sia per input veloce 
Keywords  [MOD][CELLA][UPD]

ModificaCella/Input  
   
NB : Non ho ancora implementato i controlli sul formato dell'input, quindi alfa, numerico con interi e decimali, data, etc ------------------------------------------------------------------------------------------------------------------------------  
## INPUT VELOCE  
Si ottiene la visualizzazione di una form per inserimento veloce di un dato con le seguenti istruzioni  
 DATO$=" " contenuto che si vuole mostrare (per modifica)  
 LABEL$="Dato di prova"; label campo - puo' essere vuota CAR$="000" ; rem caratteristiche campo cosi come in smd_mgd  
 CALL "smd_mgd::SUB_GRID_MODIFY_EXT",DATO$,LABEL$,CAR$ in dato$ si ottiene il campo cosi come digitato ----------------------------------------------------------------------------------------------------------------------  
## CELLA GRIGLIA  
Per richiamare la routine direttamente dalla modifica di una cella nella griglia, la call va inserita nella griglia che si intende modificare nell'evento Grid_Clicked  
La sintassi e la seguente if gb__notice.lparam=1 then return ; rem evita la call sia sul click che sul rilascio    
 d_in$="913|"+str(grid_id3)+"|"+str(gb__sysgui)+"|"+str(gb__current_context+4)  
 call "smd_mgd",d_in$,PSG_GDAT$[ALL],PSG_GCHD$[ALL],PSG_GCPS$[ALL],D_OUT$  
 gosub Sub_Grid_Show  
   
L'indicatore di funzione e 913 che e fisso e definito. Le colonne che si vuole vengano modificate devono avere l'indicatore Ovw: nel GCPS$[].  
Quindi nel Grid_Init ad esempio GCPS$[3]="172000000Ovw:"  
La modifica avviene solo sulla cella, quindi eventuali altre operazioni vanno fatte nel programma.  
In d_out$ restituisco riga selezionata e colonna selezionata nella forma rrrrcccc  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*
