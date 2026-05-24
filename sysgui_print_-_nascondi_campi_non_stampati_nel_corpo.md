---   
title:sysgui print - Nascondi campi non stampati nel corpo    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# sysgui print - Nascondi campi non stampati nel corpo 
Keywords  [CTH][COL TO HIDE][SYSGUI][rbgarc][rbgpfm]

   
 - Necessaria versione 11/5/2026 di rbgarc  
 - Inserire nel campo TITLE della form principale (non name)  
  il prefisso _COL:  
  l'elenco dei primi campi delle colonne da oscurare formattati con mask 00000  
  il suffisso _  
  Esempio Modulo Ordine 01_COL:0030101001002010120100401005010070101101_  
   Oscura le colonne il cui primo campo ha nel name #cp00301, #cp01001,#cp00201 etc  
 - Modificare il programma che esegue la stampa (tipicamente rbgpso, rbgpsp, etc) richiamando nella routine SYSGUI_PRINT la call  
  CALL "rbgarc::SUB_HIDE_COL",FILENM$,R_DATI$[ALL],ELE_RIG-1  
  La call va inserita dopo la routine che ha compilato i campi e prima di quella di stampa  
  Esempio in rbgpso  
   33470 CALL "rbgarc",FILENM$,R_CPO$[ALL],R_DATI$[ALL]  
   33472 CALL "rbgarc::SUB_HIDE_COL",FILENM$,R_DATI$[ALL],ELE_RIG-1  
   33480 CALL "rbgpfm",R_DATI$[ALL],R_PRM1$[ALL],GCH  
   ele_rig rappresenta il numero delle righe attive nella pagina in stampa ed e' gia' calcolata da SYSGUI_PRINT  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
