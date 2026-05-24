---   
title:Libreria rbgres    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria rbgres 
Keywords  [FORM][OBJ][ID][BRC][GB__CONTROL][WIN][MONITOR]

   
## Costrusice la form  
MAIN  
Costruisce la form video  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
##  Proporziono  
<b>Funzione</b> SUB_SCALE_BRC  
<b>Sintassi</b>`call "rbgres::sub_scale_brc",d_in$,d_out$  
<b>Descrizione e specifiche</b>  
REM ----------------------------------------------------------     
REM > Proporziono mantenendo il rapp della form non del monitor    
REM --- I monitor sono     w      h    rapporto                    
REM --->                  800 x  600    1.33                       
REM --->                 1024 x  768    1.33                       
REM --->                 1280 x  720    1.78                       
REM --->                 1920 x 1080    1.78           
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## Monitor elaborazione  
<b>Funzione</b> SUB_BRC  
<b>Sintassi</b>`call "rbgres::sub_brc",d_in$,d_out$  
   
<b>Descrizione e specifiche</b>  
Monitor elaborbazione - Costruisce SOLO una form nella quale IL PROGRAMMA CHIAMANTE puo' visualizzare un monitor del progresso della elaborazione   
La form smd_win.brx creata contiene un oggetto TEXT con ID  799 nel quale il programma chiamante puo' printare lo stato di avanzamento un oggetto CHECK con ID 798 attraverso il quale il programma chiamante puo' interrompere la visualizzazione. ENTRAMBI GLI OGGETTI vanno gestiti dal pgm chiamante"  
   
   
 D_INBRC$=" | |Testomessaggio|Titolo form|"             
 CALL "smd_win::sub_brc",D_INBRC$,D_OUTBRC$             
 C_SY=NUM(D_OUTBRC$(1,4)),C_CX=NUM(D_OUTBRC$(5,4))                                                            
 IN                                                                  
  1                                                               
  2                                                               
  3 Testo messaggio   (Default 'Load.....")                       
  4 Titolo form       (Avra' come prefisso RDeP + PGM-1 + PGM-2)  (Default 'Monitor Elaborazione')            
 OUT                                                                 
  sssscccc  
  ssss=Canale Sysgui  
  cccc=Contesto         
Per ottenere la visualizzazione dello stato di avanzamento si deve  
Inserire la print(c_sy)'title'(799,............)  
Chiudere in uscita print (c_sy)'destroy'(0); close(c_sy)          
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_FORM_DEDICATA:                                                        
REM            ATTENZIONE  
REM in questa Routine accedo due volte                                    
REM  -quando eseguo il programma                                          
REM  -da rbgres stesso quando verifico se form dedicata                   
REM Nel secondo caso NON devo aggiornare l'history pgmstore               
REM  perche' lo ho appena aggiornato                                       
REM --------------------------------------------------------------        
REM Questa routine restituisce il nome della form collegata               
REM  all' utente/societa/programma/nrpgm                                  
REM In Enter/D_out c'e' la form di default che viene modificata           
REM  solo se ne viene trovata una dedicata e valida                       
REM Allo stato dell'arte 12/12/2022, acquisisco programma e nrpgm         
REM  dalle variabili globali settate da g-start (vedi 14/01/2025)         
REM  Questo impedisce di lanciare il programma da un altro poiche,        
REM   non passando per g-start,non sarebbero valide                       
REM >29/08/2024 utilizzo il d_in per restituire 0=standard 1=dedicata     
REM >(*5) 14/01/2025 NO ! Il nome del programma posso acquisirlo da app$  
REM >                     pero' non il numero programma                   
REM >                     Dovrei passare in app$ anche quello             
ENTER D_IN$,D_OUT$                                                        
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_RIP_PGMSTORE:                                                 
REM Ripristino pgmstore                                           
ENTER D_IN$,D_OUT$                                                
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_TB_STD:                                                                
SETERR SUBERR                                                              
REM ---------------------------------------------------------------------  
REM Scopo di questa routine era inizialmente di utilizzare un metodo       
REM  che mi permettesse di evitare il rebuild di tutti i programmi         
REM  in seguito alla implementazione di un tasto o ad una modifica         
REM Questo scopo e' pero'raggiunto solo parzualemente poiche potrei essere  
REM  costretto a passare un parametro in piu' o riceverne uno in piu'        
REM Allo stesso modo, con lo stesso scopo e le stesse limitazioni,         
REM  utilizzo SUB_TB_STD_OUT per decodificare il d_out restituito          
REM ---------------------------------------------------------------------  
REM Questa routine dovra essere utilizzata da tutti i programmi            
REM  nella sezione di utilizzo dei tasti funzione standard                 
REM -> va testat per essere certi di passare tutti i parametri             
REM -> in enter e ricevere tutti i parametri in exit                       
REM --- utilizzata per 731  prima del 29/07/2024                           
REM --- utilizzata per 734  al        29/07/2024                           
REM --- utilizzata per 740  prima del 10/12/2020                           
REM --- utilizzata per 714  dal       29/01/2025                           
ENTER D_IN$,D_OUT$,PS__ARG$                                                
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_TB_STD699:                                                              
SETERR SUBERR                                                               
ENTER GB__SYSGUI,PS__CPO,PS_PATH$,GB__EVENT$,PS__EDCHG,FILENM$              
PRINT 'PUSH'                                                                
LET ACC$=STBL("acc")                                                        
CALL "smd_s17::sub_load_s17","|91069"+$09$+"z00-explorev1||D|",EXPLORE_V1$  
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_FORM_IQ:   
ENTER SYSGUI   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_TB_STD_DOUT:                                           
REM Vedi SUB_TD_STD per le specifiche                      
ENTER D_IN$,D_OUT$,PS__ARG$,ID,CODE$,FLAGS,EDCHG,CPO_OUT$  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_GAR_GRID_STD:                                                     
REM Questa routine dovra essere utilizzata da tutti i programmi       
REM  nella sezione ps_sub_gar                                         
REM  in questo modo le modifiche apportate in questo modulo saranno   
REM  immediatamente disponibili in tutti i programmi senza dover      
REM  necessariamente eseguire il rebuild                              
REM --- al 15/3/2023 la sto testando                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## SUB_DET_OBJ  
46510 REM =====================================================            
46515 REM == Restituisce le caratteristiche di un oggetto                  
46520 REM == >1 canale sysgui                                              
46525 REM == >2 ctx nel quale si trova l'oggetto                           
46530 REM == >3 ctx nel quale ci si vuole riposizionare in uscita (-1=no)  
46535 REM == >4 id oggetto                                                 
46540 REM                                                                  
46545 REM == >d_out$[1 posizione x                                         
46550 REM == >d_out$[2 posizione y                                         
46555 REM == >d_out$[3 larghezza w                                         
46560 REM == >d_out$[4 altezza h                                           
46565 REM == >d_out$[5 name                                                
46570 REM == >d_out$[6 type                                                
46575 REM == >d_out$[7 background color                                    
46580 REM == >d_out$[8 foreground color                                    
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
Struttura gb__control$  
 TYPE:N(2*=0),WINDOW_ID:C(16*=0),NAME:C(30*=0),CTL_ID:N(3*=0),X:N(3*=0),Y:N(3*=0),W:N(3*=0),H:N(3*=10)  
 type  tipo oggetto  
 window_id vuoto se form principale altrimenti ID CHILD (non contesto)  
 name  
 ctl_id  id oggetto all'interno della window_id  
Struttura gb__child$  
 "name:c(16*=0),id:c(16*=0),context:n(4*=0),emask:c(8*=0),flags:c(8*=10)"    
 name  nome cosi come dichiarato nell'oggetto della child nella FORM. Non e' il nome dato alla child nella lista child      
valori g-rmuvis al 21/12/2025  
>print gb__window_context$  
101=0                       
101.4001=2                  
101.4002=3                  
101.4003=4                  
101.4004=5                  
>print gb__context_window$  
0=101                       
2=101.4001                  
3=101.4002                  
4=101.4003                  
5=101.4004                  
>print gb__win_id$  
101                 
>print gb__child_list$                                    
verifica Ean40056C3F007C400010010                         
InquiryMovCliFor40067C3F007C400010010                     
Child Window40078C3F007C400010010                         
FattureXml40089C3F007C400010010                           
EstrattoConto400910C3F007C400010010                       
GiornaleMaga401011C3F007C400010010                        
OrdiniInseriti401112C3F007C400010010                      
Verifica Pre Invio SDI401213C3F007C400010010              
ControlloWeb_Costi401314C3F007C400010010                  
InquiryK54401415C3F007C400010010                          
ExportArticoli401516C3F007C400010010                      
Inqury_cfo_tpf401617C3F007C400010010                      
Child Window401718C3F007C400010010                        
Child Window401919C3F007C400010010                        
Child Window402020C3F007C400010010                        
Analisi Componenti DIiba su Ordini402121C3F007C400010010  
Child Window180501C3F007C400010010                        
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
