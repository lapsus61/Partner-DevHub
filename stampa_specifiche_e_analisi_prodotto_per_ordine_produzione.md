---   
title:Stampa Specifiche e Analisi Prodotto per Ordine Produzione    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Stampa Specifiche e Analisi Prodotto per Ordine Produzione 
Keywords  [smd_anl][ANALISI]MVU]

   
REM ---------------------------------------------------------------------  
REM     smd_anl contiene le routine presenti prima in smd_odp  
REM      che pero' riguardavano Analisi e non ODP  
REM ---------------------------------------------------------------------  
   
##  SUB_STP_SPEC_TECNICHE  
ENTER DATI$[ALL],C[ALL],CRP_AGG_MAIL$,D_OUT$  
   
##SUB_CANL_COSTI  
 Passata Key Gruppo o Precertificato  
 Restituisce Costi totali  
 Se d_in$[3]="Y"- i cosi da restituire sono solo per le righe con mvu_c.rif$<>""  
   
## SUB_CANL_GRID_SHOW:                                   
 Crea una griglia con smd_win::sub_brc_grid                          
SETERR SUBERR                                         
ENTER D_IN$,D_OUT$                                    
CALL "sm2_utl::sub_set_din",D_IN$,REC_IN$             
LET X0$=REC_IN.CPO$[1]                                
LET KEY$=REC_IN.CPO$[2]+FILL(13," "),KEY$=KEY$(1,13)  
   
## SUB_CANL_GENERAP:                                                        
 Genera il precertificato di un ODP con le voci di analisi del processo relativo                                            
REM d_in$                                                                
REM      >1 X0                                                           
REM      >2 TIP  Tipo precertificato P/F/I/R/S                           
REM      >3 ART  Codice Articolo                                         
REM      >4 RIF  ODP per il quale generare il precertificato             
REM               nella forma tip+aaaammgg+nrrf+ctr                      
REM              MOV riferimento movimento di carico materia prima       
REM               nella forma tip+aaaammgg+nrrf+ctr                      
REM      >5 STS ODP in ingresso                                          
REM      >6 Flag Generazione File pdf   Y = Genero file                  
REM                                     N = NON Genero file              
REM      >7 Flag Formato Stampa         P = PDF                          
REM                                     W = Word .docx                   
REM ===================================================================  
   
##SUB_CANL_SEARCH1:                                     
  Forniti in ingresso TIP e ODP/MOV restituisce in dout il record PDC$                        
REM d_in$                                             
REM      >1 X0                                        
REM      >2 TIP                                       
REM      >3 Key ODP/MOV                               
## SUB_CANL_SEARCH2:                                                     
REM == Restituisce una lista dei record nel   tipo/sts richiesto ==   
REM == In d_out$ il numero dei record trovati                         
REM == In v_pdc$[] i dati richesti                                    
REM d_in$                                                             
REM      >1 X0                                                        
REM      >2 TIP                                                       
REM      >3 Status                                                    
REM      >4 Tipo out   R=Record K=Key  L=Key ListButton in v_pdc[1]   
   
## SUB_SOST_ANALISI_GRP:                                             
 Sostituisce ANALISI A in tutti i gruppi in cui e' presente con codice  ANALISI B                                         
REM D_IN                                                          
REM >1 x0                                                         
REM >2 Tipi gruppi da controllare                                 
REM >3 Analisi obsoleta                                           
REM >4 Analisi da sostituire                                      
REM ------------------------------------------------------------  
   
   
##SUB_CANL_SEARCH3:                                                    
 Restituisce una lista dei record relativi all'articolo e nel tipo/sts richiesto  
 In d_out$ il numero dei record trovati                        
 In v_pdc$[] i dati richesti                                   
REM d_in$                                                            
REM      >1 X0                                                       
REM      >2 TIP                                                      
REM      >3 Status                                                   
REM      >4 Articolo                                                 
REM      >5 Tipo out   R=Record K=Key L=Key ListButton in v_pdc[1]   
REM      >             G=Rif a mov/ord                               
REM      >6 Lotto per filtro                                         
REM      >7 Data scadenza per filtro                                 
REM      >8 Cella per filtro  
   
   
##   SUB_CANL_SEARCH0:                                                     
REM == Riceve in ingresso la knum 0 e restitusice il record relativo  
REM == Se nella key trova i caratteri speciali [ e ]             ==   
REM ==  restituiti da  sub_canl_serch2 e sub_canl_search3 esegue ==   
REM ==  prima il decode                                               
REM == In d_out$ il record                                            
REM d_in$                                                             
REM      >1 X0                                                        
REM      >2 key                                                       
   
## SUB_STAMPA_COA:                                                            
REM ===================================================================    
REM ==     Riceve in input Precertificato analisi P - F - I - R      ==    
REM ==       Stampa usando il modulo sysgui_COA.arc                  ==    
REM ==       D_in$                                                    ==   
REM ==       <0,1   x0                                               ==    
REM ==       <0,2   Tipo Precertificato                               ==   
REM ==       <0,3   Mvu_c.key                                        ==    
REM ==       <0,4   Param Stampa -> P = PRECERT -  C = COA            ==   
REM ==       <0,5   Param formato -> P = PDF - W = Word              ==    
REM ==              (solo per precertificato) GG 14-07-2025          ==    
REM ==       D-out$                                                   ==   
REM ==       <1     Stampa Avvenuta con Successo                     ==    
REM ==       <-1    Errore in fase di stampa                          ==   
REM ===================================================================    
   
   
   
   
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
