---
title: "Istruzioni del firewall | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: a7dc429f-65ac-4faf-974a-77d5fb977fe1
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# Istruzioni del firewall
È necessario abilitare più porte o programmi nel firewall in modo tale che gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possano funzionare.In molti degli esempi la comunicano avviene tramite le porte comprese nell'intervallo 8000\-8003 e la porta 9000.Il firewall viene attivato per impostazione predefinita e impedisce l'accesso a queste porte.Per abilitare il firewall per gli esempi, completare una delle procedure descritte di seguito, a seconda dei requisiti e dell’ambiente di sicurezza:  
  
-   Opzione 1: abilitazione degli esempi in modo interattivo durante l’esecuzione.Non apportare nessuna modifica alla configurazione del firewall in anticipo e procedere con l’avvio e l’esecuzione degli esempi.Durante l’esecuzione di un esempio, viene visualizzata una finestra di dialogo **Avviso di sicurezza Windows**.Il programma di esempio in questione può essere quindi aggiunto, in modo interattivo, a un elenco sbloccato.Questa procedura può richiedere il riavvio dell'esempio.  
  
-   Opzione 2: abilitazione dei programmi di esempio in anticipo.Avviare l'applet **Pannello di controllo di Windows Firewall** e abilitare i programmi di esempio che si intende eseguire.Per creare file eseguibili, è necessario prima compilare i programmi.Informazioni più dettagliate sono descritte nella procedura seguente.  
  
-   Opzione 3: abilitazione dell’intervallo delle porte in anticipo.Avviare l'applet del **Pannello di controllo** di **Windows Firewall** e abilitare le porte 80, 443, 8000\-8003 e 9000, utilizzate dagli esempi.Informazioni più dettagliate sono descritte nella procedura seguente.Questa opzione è meno sicura rispetto alle altre in quanto consente a qualsiasi programma di utilizzare queste porte, non solo agli esempi.  
  
 In caso di dubbi su quale procedura utilizzare, scegliere la prima opzione.Se si sta eseguendo un firewall di un altro fornitore, potrebbe essere necessario apportare modifiche simili.  
  
> [!IMPORTANT]
>  La modifica della configurazione del firewall influisce sulla sicurezza.È consigliabile registrare le modifiche apportate e rimuoverle una volta completate le operazioni con gli esempi.  
  
### Abilitazione dei programmi di esempio in anticipo.  
  
1.  Compilare l'esempio.  
  
2.  Fare clic sul pulsante **Start**, scegliere **Esegui** e digitare `firewall.cpl`.Verrà visualizzata l’applet del **Pannello di controllo di Windows Firewall**.  
  
    > [!NOTE]
    >  Per modificare le impostazioni del firewall ed eseguire gli esempi che richiedono la possibilità di comunicare con Windows Firewall, è necessario disporre delle autorizzazioni necessarie.Se alcune impostazioni del firewall non sono disponibili e il computer è connesso a un dominio, è possibile che queste impostazioni vengano controllate dall'amministratore di sistema tramite Criteri di gruppo.  
  
3.  Completare uno dei passaggi operativi specifici seguente per consentire a un programma l'accesso con Windows Firewall:  
  
    -   In Windows 7 o Windows Server 2008 R2 fare clic su **Consenti programma o funzionalità con Windows Firewall**.Fare clic su **Cambia impostazioni**, **Consenti un altro programma**.  
  
    -   In [!INCLUDE[wv](../../../../includes/wv-md.md)] o [!INCLUDE[lserver](../../../../includes/lserver-md.md)] fare clic su **Consenti programma con Windows Firewall**.  
  
4.  Fare clic su **Aggiungi programma** nella scheda **Eccezioni**.  
  
5.  Fare clic su **Sfoglia** e selezionare il file eseguibile dell'esempio che si intende eseguire.  
  
6.  Ripetere i passaggi 4 e 5 fino a quando non si saranno aggiunti i file eseguibili di tutti gli esempi che si intende eseguire.  
  
7.  Scegliere **OK** per chiudere l’applet firewall.  
  
### Abilitazione di un intervallo delle porte in anticipo.  
  
1.  Fare clic sul pulsante **Start**, scegliere **Esegui** e digitare `firewall.cpl`.Verrà visualizzata l’applet del **Pannello di controllo di Windows Firewall**.  
  
2.  In Windows 7 o Windows Server 2008 R2 attenersi alla procedura seguente:  
  
    1.  Fare clic su **Impostazioni avanzate** nella colonna sinistra della finestra Windows Firewall.  
  
    2.  Fare clic su **Regole in entrata** nella colonna sinistra.  
  
    3.  Fare clic su **Nuove regole** nella colonna destra.  
  
    4.  Selezionare **Porta**, quindi fare clic su **Avanti**.  
  
    5.  Selezionare **TCP** e immettere `8000, 8001, 8002, 8003, 9000, 80, 443` nel campo **Porte locali specifiche**.  
  
    6.  Fare clic su **Avanti**.  
  
    7.  Selezionare **Consenti la connessione** e fare clic su **Avanti**.  
  
    8.  Selezionare **Dominio** e **Privato**, quindi fare clic su **Avanti**.  
  
    9. Assegnare a questa regola il nome `WCF-WF 4.0 Samples` e fare clic su **Fine**.  
  
    10. Fare clic su **Regole in uscita** e ripetere i passaggi da C a H.  
  
3.  In [!INCLUDE[wv](../../../../includes/wv-md.md)] o [!INCLUDE[lserver](../../../../includes/lserver-md.md)] attenersi alla procedura seguente:  
  
    1.  Fare clic su **Consenti programma con Windows Firewall**.  
  
    2.  Fare clic su **Aggiungi porta** nella scheda **Eccezioni**.  
  
    3.  Immettere un nome, quindi immettere 8000 come numero di porta e selezionare l'opzione **TCP**.  
  
    4.  Scegliere **Cambia ambito**, selezionare l’opzione **Solo la rete \(subnet\) locale** e fare clic su **OK**.  
  
    5.  Ripetere i passaggi da B a D per le porte 8001, 8002, 8003, 9000, 80 e 443.  
  
4.  Fare clic su **OK** per chiudere l'applet del firewall.  
  
> [!NOTE]
>  Rimuovere le eventuali eccezioni del firewall dopo aver completato le operazioni con gli esempi.A tale scopo, aprire l'applet del **Pannello di controllo di Windows Firewall** e rimuovere tutte le voci relative ai programmi o alle porte aggiunte alle procedure precedenti.