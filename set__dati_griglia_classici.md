---   
title:SET> dati griglia classici    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# SET> dati griglia classici 
Keywords  [GRIGLIA][GRID][ROW]

   
 grigliaSET> dati griglia classici [GRIGLIA][GRID][ROW]  
 dopo aver eseguito il caricamento di d_out$ -- D_IN$="X0:"+STR(GB__SYSGUI:"0000")+STR(800:"00000")+D_OUT$  
 oppure D_IN$=D_OUT$ -- CALL "sm2_utl",D_IN$,TESTATA$,PSG_GDAT1$[ALL]  
 CALL "sm2_utl::set_grid",TESTATA$,PSG_GDAT1$[ALL],PSG_GCHD1$[ALL],PSG_GCPS  
1$[ALL],T_ROW1,T_COL1 se si vuole utilizzare una griglia standard forzando lo show gar_dat[1,3]=t_row1, gar_dat[1,4]=t_col1, gar_gridID=18001 gosub PS_SUB_GAR_INIT; gosub PS_SUB_GAR_SHOW ctr1=t_row1 ---------------------------------------------------  
------------------------------------------------------------- si posiziona su una riga specifica ROW$=SENDMSG(gb__sysgui,grid_id2,48,row-1,$$); rem Mi posiziono sula riga originaria --------------------------------------------------------------------  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- GRIGLIA NON STANDARD - LA ROUTINE CHE CARICA IL D_OUT CARICA ANCHE I NOMI COL  
ONNA E LE CARATTERISTICHE QUINDI NON SI USA sub_grid3_init call "smd_arx::SUB_DIR_XML","",d_xml$ ; rem carica il d_out (compreso header e caratteristiche) grid_id3=3601 ; rem ___________________________________________________________________________  
_______________________set numero griglia PRINT (GB__SYSGUI)'context'(gb__current_context+2),'title'(1505,"Fatture Elettroniche Ricevute") ; rem ________________________________set contesto d_in$=d_xml$; call "sm2_utl",d_in$,testata$,psg_gdat3$[all]  
; rem _______________________________________________________________estrae testata e matrice CALL "sm2_utl::set_grid",TESTATA$,PSG_GDAT3$[ALL],PSG_GCHD3$[ALL],PSG_GCPS3$[ALL],T_ROW3,T_COL3 ; rem _________________load header e caratteristiche - out:  
row e col call "rbgmgd::sub_initgrd",GB__SYSGUI,gb__current_context+2,GRID_ID3,t_row3,T_COL3,PSG_GCHD3$[ALL] ; rem ______________________set griglia CALL "rbgmgd::sub_colresize",GB__SYSGUI,gb__current_context+2,GRID_ID3,PSG_GDAT3$[ALL],PSG_GCPS3$[ALL  
]; rem ________________esegue resize gosub Sub_Grid3_Show ; rem show griglia (utilizzata anche da grid update) -------------------------------------------------------------------------------------------------------------------------------------------  
------------------------------------------------------------------------------------------------------  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:24 in ambiente Oblivion/ECHO*
