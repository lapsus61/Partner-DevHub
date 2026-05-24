---   
title:Possibilita' di visualizzare i dati di un d_out classico con testata e riga un una form stile pop-up   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Possibilita' di visualizzare i dati di un d_out classico con testata e riga un una form stile pop-up
Keywords  

  [D_OUT][DOUT][GRID][GRIGLIA][MSG][POP-UP]  
   
 VisualizzazioneDOUT  
 Possibilita di visualizzare i dati di un d_out classico con testata e riga in una form stile pop-up  
 Se avete un d_out$ nella classica forma -quindi con primo record di testata e altri di riga e con separatore di campo $09$ e separatore di riga $0a$,  
 e volete mostrarlo stile pop-up cioe con una finestra che si apre potete usare questa nuova routine  
 d_in$="|"+str(gb__sysgui)+"|"+str(gb__current_context)+"|"  
 call "sm2_utl::sub_msgbox_grid",d_in$,d_out$  
  La routine vi mostra i dati in una griglia con le formattazioni classiche (data/numero/decimali/etc) e si chiude con un check box.  
 Non prevede nessun tasto funzione, solo visualizzazione  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
