---
title: "Installazione accodamento messaggi (MSMQ) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7ddcd497-3e04-427e-bc04-3610ad98b01e
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Installazione accodamento messaggi (MSMQ)
Le procedure seguenti mostrano come installare Accodamento messaggi 4.0 e Accodamento messaggi 3.0.  
  
> [!NOTE]
>  La versione 4.0 del sistema di accodamento dei messaggi non è disponibile in [!INCLUDE[wxp](../../../../includes/wxp-md.md)] e [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)].  
  
#### Per installare la versione 4.0 del sistema di accodamento dei messaggi in Windows Server 2008 o in Windows Server 2008 R2  
  
1.  In Server Manager, fare clic su **Funzionalità**.  
  
2.  Nel riquadro destro, in **Riepilogo funzionalità**, fare clic su **Aggiungi funzionalità**.  
  
3.  Nella finestra che viene visualizzata, espandere **Accodamento messaggi**.  
  
4.  Espandere **Servizi Accodamento messaggio**.  
  
5.  Fare clic su **Integrazione servizi directory** \(per i computer associati ad un dominio\), quindi fare clic su **Supporto HTTP**.  
  
6.  Fare clic su **Avanti**,quindi su **Installa**.  
  
#### Per installare la versione 4.0 del sistema di accodamento dei messaggi in Windows 7 o in windows Vista  
  
1.  Aprire il **Pannello di controllo**.  
  
2.  Fare clic su **Programmi** e quindi in **Programmi e funzionalità**, fare clic su **Attivazione e disattivazione delle funzionalità Windows**.  
  
3.  Espandere il server di accodamento messaggi Microsoft \(MSMQ\), espandere il server di base di accodamento messaggi Microsoft \(MSMQ\) e quindi selezionare le caselle di controllo per l’installazione delle funzionalità di Accodamento messaggi seguenti:  
  
    -   Integrazione dei Servizi di dominio Active Directory MSMQ \(per computer aggiunti a un Dominio\).  
  
    -   Supporto HTTP MSMQ.  
  
4.  Fare clic su **OK**.  
  
5.  Se viene richiesto di riavviare il computer, fare clic su **OK** per completare l'installazione.  
  
#### Per installare la versione 3.0 di Accodamento messaggi in Windows XP o Windows Server 2003  
  
1.  Aprire il **Pannello di controllo**.  
  
2.  Scegliere **Installazione applicazioni** e fare clic su **Installazione componenti di Windows**.  
  
3.  Selezionare Accodamento messaggi e fare clic su **Dettagli**.  
  
    > [!NOTE]
    >  Se è in esecuzione [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], selezionare Server applicazioni per accedere a Accodamento messaggi.  
  
4.  Assicurarsi che l'opzione Supporto HTTP MSMQ sia selezionata nella pagina dei dettagli.  
  
5.  Fare clic su **OK** per uscire dalla pagina dei dettagli, quindi fare clic su **Avanti**.Completare l’installazione.  
  
6.  Se viene richiesto di riavviare il computer, fare clic  su **OK** per completare l'installazione.  
  
## Vedere anche  
 [Istruzioni di configurazione](../../../../docs/framework/wcf/samples/set-up-instructions.md)