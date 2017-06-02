---
title: "Procedura: Sostituire la prenotazione URL WCF con una prenotazione limitata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2754d223-79fc-4e2b-a6ce-989889f2abfa
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: Sostituire la prenotazione URL WCF con una prenotazione limitata
Una prenotazione URL consente di limitare chi può ricevere messaggi da un URL o un set di URL.Una prenotazione è costituita da un modello di URL, un elenco di controllo di accesso \(ACL\) e un set di flag.Il modello di URL definisce quali URL sono interessati dalla prenotazione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] come vengono elaborati i modelli di URL, vedere la pagina relativa al [routing delle richieste in ingresso](http://go.microsoft.com/fwlink/?LinkId=136764).L'elenco ACL controlla a quale utente o gruppo di utenti è permesso ricevere messaggi dagli URL specificati.I flag indicano se la prenotazione deve fornire a un utente o a un gruppo l'autorizzazione per ascoltare direttamente l'URL o delegare l'autorizzazione per ascoltare qualche altro processo.  
  
 Come parte della configurazione predefinita del sistema operativo, in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene creata una prenotazione globalmente accessibile per la porta 80 per consentire a tutti gli utenti di eseguire applicazioni che utilizzano un'associazione HTTP duale per la comunicazione duplex.Poiché l'elenco ACL in questa prenotazione è per tutti, gli amministratori non possono consentire o impedire in modo esplicito l'autorizzazione all'ascolto di un URL o un set di URL.In questo argomento viene illustrato come eliminare questa prenotazione e come ricrearne una con un ACL limitato.  
  
 In [!INCLUDE[wv](../../../../includes/wv-md.md)] o [!INCLUDE[lserver](../../../../includes/lserver-md.md)] è possibile visualizzare tutte le prenotazioni URL HTTP da un prompt dei comandi con privilegi elevati digitando `netsh http show urlacl`.Nell'esempio seguente viene mostrato l'aspetto di una prenotazione URL [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
```  
Reserved URL : http://+:80/Temporary_Listen_Addresses/  
        User: \Everyone  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;WD)  
```  
  
 La prenotazione è costituita da un modello di URL che viene utilizzato quando un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza un'associazione duale HTTP per la comunicazione duplex.Gli URL di questo form vengono utilizzati per un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per restituire messaggi al client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] durante la comunicazione in un'associazione duale HTTP.Tutti vengono dotati di autorizzazione per ascoltare sull'URL ma non per delegare l'ascolto di un altro processo.Infine, l'elenco ACL viene descritto nel linguaggio SSDL \(Security Descriptor Definition Language\).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] SSDL, vedere [SSDL](http://go.microsoft.com/fwlink/?LinkId=136789)  
  
### Per eliminare la prenotazione URL WCF  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, quindi **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi fare clic su **Esegui come amministratore** nel menu di scelta rapida che viene visualizzato.Fare clic su **Continua** nella finestra del controllo dell'account utente \(UAC\) nella quale potrebbero essere richieste delle autorizzazioni per continuare.  
  
2.  Digitare **netsh http delete urlacl url\=http:\/\/\+:80\/Temporary\_Listen\_Addresses\/** nella finestra del prompt dei comandi.  
  
3.  Se la prenotazione viene eliminata correttamente, viene visualizzato il messaggio seguente.**URL reservation successfully deleted**  
  
## Creazione di un nuovo gruppo di sicurezza e una nuova prenotazione URL limitata  
 Per sostituire la prenotazione URL [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con una prenotazione limitata è necessario innanzitutto creare un nuovo gruppo di sicurezza.Tale gruppo può essere creato da una finestra del prompt dei comandi o dalla console di gestione del computer.Occorre scegliere una delle due modalità.  
  
#### Per creare un nuovo gruppo di sicurezza da un prompt dei comandi  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, quindi **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi fare clic su **Esegui come amministratore** nel menu di scelta rapida che viene visualizzato.Fare clic su **Continua** nella finestra del controllo dell'account utente \(UAC\) nella quale potrebbero essere richieste delle autorizzazioni per continuare.  
  
2.  Digitare **net localgroup "\<security group name\>" \/comment:"\<security group description\>" \/add** al prompt dei comandi.Sostituire **\<security group name\>** con il nome del gruppo di sicurezza che si desidera creare e **\<security group description\>** con una descrizione adeguata al gruppo di sicurezza.  
  
3.  Se il gruppo di sicurezza viene creato correttamente, viene visualizzato il messaggio seguente.**The command completed successfully.**  
  
#### Per creare un nuovo gruppo di sicurezza dalla console di gestione del computer  
  
1.  Fare clic **Start**, selezionare **Pannello di controllo**, **Strumenti di amministrazione** e fare clic su **Gestione computer** per aprire la console di gestione del computer.Fare clic su **Continua** nella finestra del controllo dell'account utente \(UAC\) nella quale potrebbero essere richieste delle autorizzazioni per continuare.  
  
2.  Fare clic su **Utilità di sistema**, fare clic su **Utenti e gruppi locali**, fare clic con il pulsante destro del mouse sulla cartella **Gruppi** e fare clic su **Nuovo gruppo** nel menu di scelta rapida che viene visualizzato.Digitare il **Nome gruppo**, la **Descrizione** e gli altri dettagli desiderati di questo nuovo gruppo di sicurezza e fare clic sul pulsante **Crea** per creare il gruppo di sicurezza.  
  
#### Per creare la prenotazione URL limitata  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, quindi **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi fare clic su **Esegui come amministratore** nel menu di scelta rapida che viene visualizzato.Fare clic su **Continua** nella finestra del controllo dell'account utente \(UAC\) nella quale potrebbero essere richieste delle autorizzazioni per continuare.  
  
2.  Digitare **netsh http add urlacl url\=http:\/\/\+:80\/Temporary\_Listen\_Addresses\/ user\="\<machine name\>\\\<security group name\>** al prompt dei comandi.Sostituire **\<machine name\>** con il nome del computer nel quale deve essere creato il gruppo e **\<security group name\>** con il nome del gruppo di sicurezza precedentemente creato.  
  
3.  Se la prenotazione viene creata correttamente, viene visualizzato il messaggio seguente.**URL reservation successfully added**.