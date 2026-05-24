---   
title:Libreria effetti / riba    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria effetti / riba 
Keywords  [EFFETTI][RIBA][GENERAZIONE][rceffe][smd_uef][spese]

  
Elenco   
  
- SUB_GENERA_EFFETTI  Emissione effetti da fatture emesse  
- SUB_VER_SPESE_FISSE  Verifica se vanno calcolate le spese fisse mp.spf sul documento. Restituisce il valore delle spese  
- SUB_VERIFICA_EFFETTI  
- SUB_ANN_DISTINTA  
- SUB_RAGGRUPPA_EFFETTI  
- SUB_INS  
  
-----------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_GENERA_EFFETTI  
  
=== Emissione effetti da fatture emesse ========================   
  
---  Legge tutte le fatture                                            
---  Filtra codici clienti                                             
---  Scarta documenti con tipo modalita di pagamento non di interesse             
---  Sviluppa scadenze                                                 
---  Aggrega                                                           
---   Riba singola fattura = N : aggrega per cliente/scadenza          
---   Riba singola fattura = Y : aggrega per cliente/fattura/scadenza  
  
================================================================       
  
- data doc inizio            
- data doc fine              
- data nc inizio             
- data nc fine               
- tipo scadenze considerate  
- messaggio di fine elaborazione Y/N                  
- Codice cliente inizio      
- Codice cliente fine        
- Numero documento inzio     
- Nr documento fine  
  
d_in$="|"+DATAIN$+"|"+DATAFN$+"|"+DATANCIN$+"|"+DATANCFN$+"|"+DEFS$+"|Y|"+CDCN1$(6,5)+CDCN1$(1,5)+"|"+CDCN2$(6,5)+CDCN2$(1,5)+"|"NRDC_IN$+"|"+NRDC_FN$+"|"                          
 CALL "smd_uef::SUB_GENERA_EFFETTI",D_IN$,D_OUT$     
----------------------------------------------------------------------------------------------------------------------------------------------------        
## SUB_VER_SPESE_FISSE                                                     
 Verifica se vanno calcolate le spese fisse mp.spf sul documento.        
(La lista dei tipi documento si rende necessaria poiche' potrebbero  )   
(esistere documenti con segno iva +,che vanno nel riporto contabile,)   
(che hanno modpag riba MA CHE NON mi interessano (NotaDebito)       )   
   
  
Controlli  
  
- se escludo spese fisse (sac.ribas$) =Y set spf=0 e esco subito  
- se modpag NON RIBA (mp.tip$) assumo mp.spf e esco subito  
- se riba per singola fattura (sac.riba$) =Y assumo mp.spf e  esco subito  
- restitituisco importo spese fisse (mp.spf) se prima fattura altrimenti ZERO  
  
  
D_IN  
  
- [1] X0  
- [2] DTIN$ data doc inizio                            
- [3] DTFN$ data doc fine                              
- [4] CFO$  Codice cliente sssssmmccc                  
- [5] MP$  record Modalita' di pagamento del doc da emettere  
- [6] L_TD$ Lista tipi documenti da considerare step 3    
  
D_OUT  
  
- importo spese fisse da addebitare       
  
-----------------------------------------------------------------------------------------------------------------------------------------------------  
REM =========================================================   
REM ---    restituisce un analisi del contenuto del file  ----  
SUB_VERIFICA_EFFETTI:                                           
REM =========================================================  
REM --- Annullamento distinta -------------------------------  
REM ---  set a blank il numero di distinta                     
SUB_ANN_DISTINTA:                                              
SUB_RAGGRUPPA_EFFETTI:   
SETERR SUBERR            
ENTER D_IN$,D_OUT$       
ESCAPE; REM mai testato  
5010 SUB_INS:                                                              
5020 REM ================================================================  
5030 REM === Crea Riba ==================================================  
5040 REM ================================================================  
5050 ENTER D_IN$,D_OUT$                                                    
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
