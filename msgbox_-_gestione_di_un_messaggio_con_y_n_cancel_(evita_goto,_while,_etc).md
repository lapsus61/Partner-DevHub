---   
title:MSGBOX - Gestione di un messaggio con Y/N/Cancel (evita goto, while, etc)   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# MSGBOX - Gestione di un messaggio con Y/N/Cancel (evita goto, while, etc)
Keywords  

   
   
 call "sm2_utl::sub_msg_YNC"," |0|48|"+messg$+"|Titolo|",d_out$  
 Gestione di un messaggio con Y/N/Cancel (evita goto, while, etc)  
   
   
 REM ==  Evita la gestione del Cancel con while                     
 D_IN                                                       
  1 X0                                                    
  2 Tipo (future epansioni)                               
   0=Y/N/Cancel                                          
  3 icona (0/16/32/48,64)                                 
  4 Messaggio                                             
  5 Titolo                                                
 D_OUT Contiene il valore msgbox  decodificato              
  1 (O)K    2 (C)ancel  3 (A)bort  4 (R)etry  5 (I)gnore 6 (Y)es   7 (N)o                                        
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
