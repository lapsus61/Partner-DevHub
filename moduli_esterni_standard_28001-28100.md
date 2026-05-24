---   
title:Moduli esterni STANDARD 28001-28100    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Moduli esterni STANDARD 28001-28100 
Keywords  [rbg28N][28000][ResBuilder][brc]

   
Tasti Funzione riservati  
Programma da chiamare                     Tasto Parametro richiesto                    
   
- g-rmisk2 Inquiry skeda                    28011 "KeyMovimento"  
- g-rmior2 Inquiry ordine                   28012 "KeyOrdine")    
- g-rpgana Anagrafica cli/for               28013 "CodiceCli/For"   
- g-rmagana Anagrafica Articoli             28014 "18chrCodiceArticolo4ChrChild"    
- g-rmimvc Inquiry movimento                28015 "KeyMovimento"   
- g-rmgan2 Angarfica Articoli               28021 "CodiceCli/For"    
- g-rmgan2 Anagrafica Articoli              28022 "CodiceArticolo"  
- g-rmeorf,nrpgm:0222 Ordini                28061 ""  
- g-rmeorf,nrpgm:021 Ordini                 28062 ""  
- g-rmeorf,nrpgm:0221 Ordini                28063 ""  
- g-rpgana Tabella indirizzi supplementari  28064 "CodiceCli/For"    pgm:g-epelav ID=28064 ResBuilder=28_cpo:00001015,pgm:,nrpgm:_28  
- g-rmgtdp Tabella depositi                 28070 ""    
- g-rmgttd Tabella tipo documento           28071 ""    
- g-rmscsl Lotti in Scadenza                28075 ""  
- g-rpgtgl,nrpgm:pdd Tabella Voci Analisi   28076 ""  
   
Casi  
   
- I dati da passare SONO PRESENTI nella form/child  
indicare nel name dell'oggetto la sequenza e non e' necessario fare altro  
Esempio : Resbuilder 28_cpo:0000100100101050,pgm:,nrpgm:_28 >utilizzera' ctx0,id1001 e ctx1,id1050 come parametri  
ATTENZIONE: per questo tipo di utilizzo, NESSUNA routine deve essere attivata sul tasto interessato, neanche vuota.  
   
- I dati da passare NON sono presenti nella form/child ma in altri oggetti  
nell'evento desiderato vanno settati nella stbl rbg28n_name ed eseguito il gosub alla subroutine  
app$=stbl("rbg28n_name","KeyMovimento")  
gosub PS_TOOL_BUT  
   
   
- I dati sono presenti nella griglia e l'ID del tasto e' quello corrispondente - ad esempio Inquiry Movimenti  
call"smdVmgd::SUB_GET_ROWCOL",d_in$,gb__sysgui,gar_dat [1,2],gar_dat[1,1],psg_gdat1$[ALL],psg_gchd1$[all],psg_gcps1$[all],0,0,mne$,d_out$,dd_array[all]   
app$=stbl("rbg28n_name",d_out$)  
gosub PS_TOOL_BUT  
   
- ALCUNI dati sono presenti nella form/child ed altri NON lo sono  
si deve sia caricare la sequenza, sia settare la variabile ed eseguire il gosub  
Esempio : Resbuilder 28_cpo:0000000000101050,pgm:,nrpgm:_28 >Utilizzera' rbg28n_name+ctx1,id1050  
Codice app$=stbl("rbg28n_name","KeyMovimento");gosub PS_TOOL_BUT   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
