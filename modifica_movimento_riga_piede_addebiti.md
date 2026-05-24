---   
title:Modifica movimento riga/piede/addebiti    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Modifica movimento riga/piede/addebiti 
Keywords  [CODESTD][g-rmcrig][MV2][MV3][MOD][UPD]

## ARGOMENTI  
 gb__arg.key$      aaaammggnnnnnncccc movimento                          
 gb__arg.GenDoc         N=Non abilita tasto GeneraDocumento Y=Abilita tasto GeneraDocumento F=Forza child GeneraDocumento                                 
 gb__arg-l_rddt  Lista documenti cosi come generato da rdu_mag::sub_mov_cli_ddt ma con * invece di $0a$  
   Se passata viene sovrascritta a quella eleborato in Sub_Show_generale                             
 Permessi di modifica su riga - vanno parametrizzati sull'utente          
 RIG_PERMS$="11000"                                                       
  >1 Puo' modificare la quantita                    
  >2 Puo' modificare il prezzo e quindi gli sconti   
  >3 Puo' modificare l'ordine di riferimento e di conseguenza evaso si/no                                                            
  >4 libero                                         
  >5 libero                                         
  vedi routineSub_Set_Permessi_Riga                  
   
## RIGA  
 DIM GB__ARG$:"key:c(18),Gendoc:c(1),l_rddt:c(1000),mod_flg:c(1)"  
 GB__ARG.KEY$=k_sk_ctr$   
 gb__arg.Gendoc$="N"     
 gb__arg.l_rddt$=mv1.rf1$(15,3)+" "+fnd10$(mv1.rf1$(1,8))+" "+mv1.rf1$(9,6)+" ["+mv1.dtrg$+mv1.nrrf$+"]"+"*"                          
 CALL "g-rmcrig",GB__ARG$  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:29 in ambiente Oblivion/ECHO*
