---   
title:(MKY)Visualizzazione dei dati del D_OUT senza il caricamento della matrice PSG_GDAT$    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)Visualizzazione dei dati del D_OUT senza il caricamento della matrice PSG_GDAT$ 
Keywords  [DOUT][D_OUT][GRIGLI

VisualizzazioneDOUT_nogrigliaVisualizzazione dei dati del D_OUT senza il caricamento della matrice PSG_GDAT$ [DOUT][D_OUT][GRIGLIA][DATI_D]  
Ciao ho implementato una funzione nella gestione delle griglie che evita il caricamento della matrice dati ma visualizza direttamente il d_out generato dalle routine. VisualPro5 non essendo un linguaggio matematico e lento nel caricamento delle matri  
ci gr andi. Con questa funzionalita si ottiene che in elaborazioni che generano molte righe - video skeda ad esempio oppure visualizzazione registro - si elimini la parte piu lenta della elaborazione stessa ottenendo quindi una performance migliore.  
L'abilitazione di questa funzionalita si ottiene semplicemente aggiungendo il prefisso 'DatiD:' nella variabile D_IN$ quando si lancia sm2_utl, nient'altro.  Alessandra, per una prova reale e la verifica della maggiore velocita, mi servirebbe che lo  
implementassi in qualche programma che - come dicevo - generi molte righe. Se va tutto bene ti accorgerai che la fase 'sm2_utl row di t_row' non ti apparira p iu e che il tempo di elaborazione totale sara minore. Al momento questa cosa funziona SOLO  
nella visualizzazione, quindi la metti, provi sa va meglio (mi raccomando molti dati) e poi la levi. Questo perche, non essendoci il gdat$[all] tutte le routine che prendono il contenuto per esempio per fare inqui ry, modifica dati, etc lavorano con  
le coordinate gdat$[row,col] della griglia. Poi se va, implemento. Stefano, puoi fare anche tu qualche prova se hai griglie grandi in iPartner, pero forse in Partner e piu facile ci siano  Fatemi sapere Ciao   Note tecniche La routine la implementi c  
osi D_IN$="xxxx"+"|"+"yyyyy"+"|"+"zzzzz"+"|"...etc Call "smd_sor::SUB_LOAD_KNUM4",D_IN$,D_OUT$ D_IN$="DatiD:"+D_OUT$; CALL "sm2_utl",D_IN$,TESTATA$,d_out$[all] <----- metti solo "DatiD:" davanti a D_IN$  quello che viene dopo lo lasci come prima IF N  
UM(d_out$[0,1])=0 THEN RETURN psg_gdat1$[all]=d_out$[all] call "sm2_utl::set_grid",testata$,psg_gdat1$[all],psg_gchd1$[all],psg_gcps1$[all],t_row1,t_col1 gar_dat[1,3]=t_row1 gar_dat[1,4]=t_col1 gar_gridID=18001 gosub PS_SUB_GAR_INIT gosub PS_SUB_GAR_  
SHOW    la parte lenta che si evita in sm2_utl e questa 1290 FOR ROW=1 TO T_ROW; LET APP=POS($0A$=REC_IN$),REC_APP$=REC_IN$(1,APP-1)+FIL L(20,$2009$); IF SYSGUI<>0 THEN PRINT (SYSGUI)'TITLE'(ID,"sm2_utl "+STR(ROW)+" d i "+STR(T_ROW)) FI; FOR COL=1 TO  
 T_COL; LET D_OUT$[ROW,COL-COL_STEP]=REC_APP.CPO $[COL]; NEXT COL; LET REC_IN$=REC_IN$(APP+1); NEXT ROW    Note di funzionamento Utilizzando 'DatiD:', sm2_utl genera un D_OUT$ con queste caratteristiche D_OUT$[1,1]=REC_IN$(APP+1); REM solo dati D_OUT  
$[0,1]=STR(POS($0A$=D_OUT$[1,1],1,0)); REM nr righe (come prima) D_OUT$[0,2]=STR(POS($09$=TESTATA$,1,0)); REM nr colonne (come prima) D_OUT$[0,3]="DatiD:"; REM set flag  rbgmgd si accorge di questo indicatore in D_OUT$[0,3] e setta delle variabili pr  
ima di caricare la griglia, utilizzando questa routine e poche altre istruzioni che controllano CV_FLG 0756 REM ---Verifica se DatiD - Set variabili -------------------------------- 0757 IF TOT_COL<3 THEN GOTO 0766 0758 IF GDAT$[0,3]<>"DatiD:" THEN G  
OTO 0766 0760 LET CV_FLG=1; REM SI:flag dati $09$/$0A$ 0761 LET CV_DAT$=GDAT$[1,1]; REM DatiD>Dati 0762 DIM CV_REC$:"cpo[100]:c(500*=9)"; REM DatiD>Template di appoggio 0766 REM ---show--------------------------------------------------------------- 0  
770 FOR ROW=ROW_TOP TO MIN(ROW_TOP+ROW_VIS-1,TOT_ROW) 0771 REM ==Utilizzo dout %09$/$0A$ (CoronaVirus Test)====================== 0772 IF CV_FLG=0 THEN GOTO 0781; REM non sono entrato con dout$ ma con gdat$[] 0773 LET CV_SIC=ROW; REM store valore ori  
ginale 0775 DIM GDAT$[1,TOT_COL]; REM dim un gdat$ cosi da non dover modificare tutto il programma 0776 LET CV_S=1; IF ROW<>1 THEN LET CV_S=POS($0A$=CV_DAT$,1,ROW-1); REM start 0777 LET CV_E=POS($0A$=CV_DAT$,1,ROW); REM $0a$ end 0778 LET CV_REC$=CV_D  
AT$(CV_S+1,CV_E-CV_S-1)+FILL(100,$09$); REM recupera dati 0779 FOR CV_C=1 TO TOT_COL; LET GDAT$[1,CV_C]=CV_REC.CPO$[CV_C]; NEXT CV_C ; rem carica dati 0780 LET ROW=1; REM set il numero riga a 1 fisso perche dopo lo usa  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
