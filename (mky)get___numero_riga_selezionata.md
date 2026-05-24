---   
title:(MKY)GET > numero riga selezionata    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)GET > numero riga selezionata 
Keywords  [ROW][RIGA][GRIGLIA]

rigaGET > numero riga selezionata [ROW][RIGA][GRIGLIA]  
restituisce riga selezionata  
app$=SENDMSG(gb__sysgui,grid_id1,45,0,$$); row=DEC($00$+app$)+1 (zero based)  
Si posiziona su riga selezionata  
ROW$=SENDMSG(gb__sysgui,grid_id2,48,row-1,$$); rem Mi posiziono sula riga originaria  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:20 in ambiente Oblivion/ECHO*
