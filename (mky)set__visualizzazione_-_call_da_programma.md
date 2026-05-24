---   
title:(MKY)SET> Visualizzazione - call da programma    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)SET> Visualizzazione - call da programma 
Keywords  [RBGFVS][RBGSFV]

VisualizzazioneSET> Visualizzazione - call da programma [RBGFVS][RBGSFV]  
 rem --------------------------------------------------------------------------------------------------------------------------------Metodo 1 app$=STBL("cinp","p10") ele=gb__event.id-1450 DIM PS__ARG$:"ksel:c(120*=)" CALL "rbgfvs",PS__ARG$ PRINT (GB_  
_SYSGUI)'CONTEXT'(GB__EVENT.CONTEXT) IF LEN(PS__ARG.KSEL$)=0 THEN PRINT (GB__SYSGUI)'FOCUS'(0),; goto rbgfvs10_end read record(c[5],knum=0,key=ps__arg.ksel$,dom=rbgfvs10_end)pc$ sv$[ele,1]=pc.cod$ call "rbgled",gb__sysgui,sv$[ele,1]+"-"+pc.des$+$0a$,  
0,1400+ele call "rbgsed",gb__SYSGUI,1400+ele,sv$[ele,1],0 rbgfvs10_end: return rem --------------------------------------------------------------------------------------------------------------------------------Metodo 2 CALL "susenv","000","03"; OPEN  
 (104)"tfil03" DIM CINP$:"pio:c(3),dbase:c(10*),dtab:c(15*)" LET CINP.PIO$="a01" LET APP$=STBL("cinp",CINP$) DIM PS__ARG$:"ksel:c(120*=)" CALL "rbgfvs",PS__ARG$ rem in ps__arg.ksel$ il codice selezionato rem ------------------------------------------  
------------------------------------------------------------------------------------  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
