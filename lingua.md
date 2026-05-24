---   
title:Lingua   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Lingua
Keywords  

   
SUB_LABEL:                                                         
REM ====================LABEL====================================  
REM -------------------------------------------------------------  
REM Set label per utenti stranieri                                 
REM I dati da modificare devono essere contenuti in                
REM  un file ascii delimitato da tabulazione                       
REM  con nome <nomeprogramma>.bab                                  
REM le righe del file sono costituite dai campi                    
REM <contesto> <tab> <id> <tab> <Inglese> <tab> <Francese> <tab>   
REM -------------------------------------------------------------  
 CALL "rbglng",GB__SYSGUI,GB__CURRENT_CONTEXT,PGM(-2),ACC$(79,2)                                                                                     
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
1010 SUB_PRESET:                                                         
1020 REM ====================PRESET===================================   
1030 REM -------------------------------------------------------------   
1040 REM Set contenuto iniziale                                          
1045 REM QUESTA ROUTINE VA ESEGUITA ANCHE SUL CLEAR DI 1001              
1050 REM I dati da modificare devono essere contenuti in                 
1060 REM  un file ascii delimitato da tabulazione                        
1070 REM  con nome <nomeprogramma><nrpgm><user>.set                      
1080 REM   oppure se inesistente                                         
1090 REM  con nome <nomeprogramma><nrpgm>.set                            
1100 REM le righe del file sono costituite dai campi                     
1110 REM <contesto> <tab> <id> <tab> <Preset>                            
1120 REM                              +------> check box/radio button    
1130 REM                              +------> 0=uncheck 1=check         
1140 REM -------------------------------------------------------------   
1150 ENTER SYSGUI,CTX_ORG,PGM$,APP$; REM app$ per future espansioni    
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------  
SUB_SET_CONFIGURAZIONE:                                     
REM Utilizzato per selezionare o creare una configurazione  
REM  specifica per l'utente                                   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
