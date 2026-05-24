---   
title:Iva - Libreria - smd_iiv   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Iva - Libreria - smd_iiv
Keywords  

   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
DATI COMPLETI P/NOTA E IVA (vedi anche SUB_ENTER_SVL_IVA)   
 call "smd_iiv","KeyPnota|ContatoreIva|",d_out$[all]  
 Legge la prima nota indicata ed il registro iva per il contatore indicato (nel caso la registrazione prevedesse piu' record di registro), e  
 restituisce un d_out  
 IN  
 >(1) key prima nota  
 >(2) contatore registro  
 OUT  
 >DIM D_OUT$:"cpo[200]:c(500*=9)"  
 > [  1]=MI.DTRG$                                            
 > [  2]=MI.DTPR$                                            
 > [  3]=MI.NART$                                            
 > [  4]=MI.CDCN$                                            
 > [  5]=CVS(PC.DES$,35)                                     
 > [  6]=CVS(AC.DES$+" "+AC.RAG2$,35)                        
 > [  7]=MI.NRPR$                                            
 > [  8]=MI.CTRS$                                            
 > [  9]=MI.REG$                                             
 > [10]=CVS(IR.COD$+" - "+IR.DES$,35)                      
 > [11]=MI.IDF$                                            
 > [12]=MI.DOC$                                            
 > [13]=CVS(IT.COD$+" - "+IT.DES$,35)                      
 > [14]=STR(MI.PGRG)                                       
 > [15]=TIPOOP$(NUM(PN.FLG1$(3,1))*15+1,14)                       
 > [16]=IVASOS$((POS(PN.FLG1$(4,1)="LGN ")-1)*12+1,12)            
 > [17]=IVA$((POS(PN.FLG1$(12,1)="+-")-1)*8+1,8)                                                               
 > [18]=MOD770$((POS(PN.FLG1$(5,1)="PGN ")-1)*12+1,12)  
 > [19]=D_OUT.CPO$[19]+MI.CTRS$            
 > [20]=CVS(PNC.DES$,35)                                          
 > [21]=OP.COD$                                                   
 > [22]=CVS(OP.DES$,35)                                           
 > [23]=Lista contatore riga p/nota   
 > [24]=D_OUT.CPO$[24]+MI.REG$                          
 > [25]=MI.STS_LIQ$                                        
 > [26]=MI.DT_LIQ$                                         
 > [27]=MI.SPLIT$                                          
 > [31]=MP.COD$                                                   
 > [32]=CVS(MP.DES$,35)                                           
 > [33]=MI.DT_LIQ$                                      
 > [41]="1"; IF MI.SIVA$="-" THEN LET D_OUT.CPO$[41]="-1"                         
 > [51]=VALE.COD$                                                 
 > [52]=CVS(VALE.DES$,35)                                         
 > [53]=STR(PN.IMVAL)       
 > [60+((APP+2)/3)*3-2]=CVS(IR.COD$+" - "+IR.DES$,35)   
 > [60+((APP+2)/3)*3-1]=CVS(IT.COD$+" - "+IT.DES$,35)   
 > [60+((APP+2)/3)*3-0]=STR(MI.PGRG)     
 > [100]=ASSIVA$             
 > [101]=STR(TOTIMP)         
 > [102]=STR(TOTIVA)         
 > [103]=STR(TOTIMP+TOTIVA)  
 > [104]=STR(TOTIRR)         
 > [105]=STR(TOTIVA-TOTIRR)  
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
DATI COMPLETI SOLO PARTE IVA  
 Legge la parte iva dell'assoggettamento indicato e  restituisce un d_out  
  call "smd_iiv",SUB_ENTER_SVL_IVA,"Assiva| | | | | | | | | |i1|i2|i3|i4|i5|i6|i7| | | |iv1|iv2|iv3|iv4|iv5|iv6|iv7|",d_out$  
 IN  
 > [1] Assiva  
 > [11-17] Imponibili  
 > [21-27] Iva  
 OUT  
 > [110+J]=IV.COD$  
 > [120+J]=CVS(IV.DES$,35)  
 > [130+J]=STR(IV.ALI)  
 > [140+J]=IV.IDN$  
 > [150+J]=STR(IMPL[J])  
 > [160+J]=STR(IMPS[J])  
 > [170+J]=TALL$(NUM(IV.ALL$(1,1))*12+1,12)  
 > [180+J]=STR(IVA_IRR)         
      
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
VERIFICA CHIUSURA IVA  
  call "smd_iiv",SUB_DET_CPP  
  Loop alla ricerca dell'ultimo vi.cpp caricato che sia precedente alla data di inizio richiesta  
  IN  
  >  
  OUT  
  >D_out con campi separati da $09$  
   >ULT_VI$ $09$  periodo nella forma aaaamm dell'ultima liquidazione registrata  
   >ULT_CPP+$09$  valore della liquidazione  
   >CPP_ANNO+$09$  anno primo periodo successivo  
   >CPP_MESE+$09$  mese periodo successivo               
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
