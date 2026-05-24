---   
title:Lanciare un programma carattere da un programma grafico    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Lanciare un programma carattere da un programma grafico 
Keywords  [CARATTERE][GUI][RUN][LANCIARE][PGM:smd_win::SUB_GUI_TO_CHAR[PGM:smd_win::SUB_CHAR_TO_GUI]

LET D_IN$=STR(GB__SYSGUI)+"|"+STR(GB__CURRENT_CONTEXT)+"|"  
CALL "smd_win::SUB_GUI_TO_CHAR","",""       run  
....                                     
CALL "smd_win::SUB_CHAR_TO_GUI",D_IN$,D_OUT$ al ritorno  
#######################################################################################################  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
