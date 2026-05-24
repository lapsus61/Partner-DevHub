---   
title:Libreria Files    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria Files 
Keywords  [N][pdf][doc][xml][dms][smdNdoc][rbgdst]

Scopo di questa libreria e' racchiudere le operazioni ripetitive eseguite sui file documenti/ordini/dms. Di certo esistono molte altre routine similari  
   
   
---------------------------------------------------------------------------------------------------------------------------------------------  
Routine contenute  
   
| Routine | File |Esegue | Note |  
| :--- | :--- | :--- | :--- |  
| SUB_GET_KDOC            | DOC | GET       | Restituisce la key del file DOCUMENTO|  
| SUB_GET_DOC_ESI      | DOC | GET  | Restituisce un indicatore 0/1 su esistenza del file PDF DOCUMENTO sviluppandone la path|  
| SUB_DEF_COPY            | DOC | GET | Restituisce il nome file completo di path del file PDF DOCUMENTO |  
| SUB_FILE_NO_PATH     | DOC | GET | Divide path da files restituendo il solo flnm o la sola path |  
| SUB_GEN_DOC_PDF    | DOC | GEN     | Genera PDF DOCUMENTO |  
| SUB_COPY_FILE             | Tutti | COPY | Esegue la copia di un file |  
| SUB_CHANGE_SOC_SET | Tutti | SET | Esegue il cambio di societa' |   
---------------------------------------------------------------------------------------------------------------------------------------------  
   
## SUB_GET_KDOC  
Restituisce per il MOVIMENTO indicato                  
- 1 La key per la stampa con rbgpsp                     
- 2 La key dtdc+nrdc+tdc per la creazione del file pdf  
Nel caso di FRP+DDT permette la scelta                
   
call "smdNdoc::SUB_GET_KDOC"," |"+"n|"+mv1.flg$+"|"+mv1.rf1$+"|"+mv1.rf2$,d_out$  
   
DIN  
   
- [1] X0$  
- [2] Tipo out desiderato 1 o 2  
- [3] FLG1$ mv1.flg1$            
- [4] RIF1$  mv1.rf1$  
- [5] RIF2$  mv1.rf2$  
   
DOUT  
---------------------------------------------------------------------------------------------------------------------------------------------  
   
## SUB_GET_DOC_ESI                            
Fornito in ingresso il DOCUMENTO cosi come restituito da SUB_GET_KDOC, verifica se esiste il file PDF relativo      
call "smdNdoc::SUB_GET_DOC_ESI"," |"+keydoc$+"|"+cfo$+"|",d_out$  
   
DIN  
   
- [1] X0$  
- [2] key documento cosi come restituito da get_kdoc (aaaammggnnnnnndoc)   
- [3] Codice cliente solo sottoconto  
   
DOUT  
   
- 0 Inesistente  
- 1 Esistente  
---------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_DEF_COPY  
   
   
 D_IN$=" |1|"+KPDF$(1,8)+"|"+KPDF$(9,6)+"|"+KPDF$(15,3)+"|00000|"         
 CALL "rbgdst::sub_def_copy",D_IN$,FLNM$,FLNM1$,"","",V1$[ALL],V1[ALL],D_OUT$                                                                                 
DIN  
- [1] X0  
- [2] Fisso 1  
- [3] Data documento  
- [4] Numeo documento  
- [5] Tipo documento  
- [6] Codice cliente (obsoleto)   
DOUT  
- flnm$  Nome file PDF DOCUMENTO completo di path   
- flnm1$ Nome file locale per appoggio  
---------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_FILE_NO_PATH  
   
 call "rbgdst::SUB_FILE_NO_PATH",n,FLNM$,FLNM_NOPATH$   
DIN  
- FLNM$ Nome del file completo di path  
DOUT  
- se n = 1 FLNM_NO_PATH$ Nome del file senza path  
- se n = 2 FLNM_NO_PATH$ Solo path  
-----------------------------------------------------------------------------------------------------------------------------------------------  
   
## SUB_GEN_DOC_PDF                      
Fornito in ingresso il DOCUMENTO cosi come restituito da SUB_DEF_DOC_TO_PDF, genera il file pdf del documento lanciando RBGPSP  
call "smdNdoc::SUB_GEN_DOC_PDF"," |"+keydoc$+"|"   
DIN  
   
- [1] X0$  
- [2] key documento nella forma   flg+aaaammgg+nnnnnn+doc oppure  flg+aaaammgg+nnnnnn+doc+aaaammgg+nnnnnn+doc  
- [3] def_stp default -1  
- [4] c[0]  default 281061  
- [5] wc[0]  default 281061  
- [6] wc[1]  default 0  
---------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_COPY_FILE                                                        
Copia un file con RBGCPM  
   
Call "smdNdoc::SUB_COPY_FILE"," |"+file_srg$+"|"+file_dst$+"| 0| 0|",d_out$  
[1] X0$                                              
[2] FILE_SRG$ completo di path  
[3] FILE_DST$ completo di path  
[4] ESITO  default 0  
[5] FLG  default 0  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*
