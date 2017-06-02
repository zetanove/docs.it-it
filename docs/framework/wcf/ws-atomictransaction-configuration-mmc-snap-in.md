---
title: "Snap-in MMC di configurazione di WS-AtomicTransaction | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 23592973-1d51-44cc-b887-bf8b0d801e9e
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Snap-in MMC di configurazione di WS-AtomicTransaction
Lo Snap\-in MMC di Configurazione di WS\-AtomicTransaction è utilizzato per configurare una parte delle impostazioni WS\-AtomicTransaction su computer locali e remoti.  
  
## Osservazioni  
 Se si sta eseguendo [!INCLUDE[wxp](../../../includes/wxp-md.md)] o [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], è possibile trovare lo snap\-in MMC passando a **Pannello di controllo\/Strumenti di amministrazione\/Servizi componenti\/**, facendo clic con il pulsante destro del mouse su **Risorse del computer** e scegliendo **Proprietà**.Si tratta dello stesso percorso nel quale è possibile configurare MSDTC.Le opzioni disponibili per la configurazione sono raggruppate sotto la scheda **WS\-AT**.  
  
 Se si esegue Windows Vista o [!INCLUDE[lserver](../../../includes/lserver-md.md)], è possibile trovare lo snap\-in MMC facendo clic su **Start** e digitando `dcomcnfg.exe` nella casella **Cerca**.Quando la console MMC viene aperta, passare al nodo **Risorse del computer\\Distributed Transaction Coordinator\\DTC locale**, fare clic con il pulsante destro del mouse e scegliere **Proprietà**.Le opzioni disponibili per la configurazione sono raggruppate sotto la scheda **WS\-AT**.  
  
 I passaggi precedenti vengono utilizzati per avviare lo snap\-in per la configurazione di un computer locale.Se si vuole configurare un computer remoto, è necessario trovare il nome del computer remoto in **Pannello di controllo\/Strumenti di amministrazione\/Servizi componenti\/**ed eseguire una procedura simile se si sta eseguendo [!INCLUDE[wxp](../../../includes/wxp-md.md)] o [!INCLUDE[ws2003](../../../includes/ws2003-md.md)].Se si sta eseguendo Windows Vista o [!INCLUDE[lserver](../../../includes/lserver-md.md)], eseguire i passaggi precedenti per Vista e [!INCLUDE[lserver](../../../includes/lserver-md.md)], ma utilizzare il nodo **Distributed Transaction Coordinator\/DTC locale** sotto il nodo del computer remoto.  
  
 Per utilizzare l'interfaccia fornita dallo strumento è necessario registrare il file WsatUI.dll, disponibile nel percorso seguente:  
  
 **%PROGRAMFILES%\\Microsoft SDKs\\Windows\\v6.0\\Bin\\WsatUI.dll**  
  
 La registrazione può essere effettuata con il comando seguente:  
  
```Output  
regasm.exe /codebase WsatUI.dll  
```  
  
 È possibile utilizzare questo strumento per modificare le impostazioni WS\-AtomicTransaction di base.Ad esempio, è possibile abilitare e disabilitare il supporto del protocollo WS\-AtomicTransaction, configurare le porte HTTP per WS\-AT, associare un Certificato SSL alla porta HTTP, configurare certificati specificando nomi dell'oggetto del certificato, selezionare la modalità Traccia e impostare i timeout massimi e predefiniti.  
  
 Se è necessario configurare il supporto di WS\-AtomicTransaction solo sul computer locale, è possibile utilizzare la versione della riga di comando di questo strumento.[!INCLUDE[crabout](../../../includes/crabout-md.md)] strumento della riga di comando, vedere l'argomento [Utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md).  
  
 È necessario tenere presente che Snap\-in MMC e lo strumento da riga di comando non supportano la configurazione di tutte le impostazioni WS\-AT.Queste impostazioni possono essere modificate solo modificando direttamente il Registro di sistema.[!INCLUDE[crabout](../../../includes/crabout-md.md)] queste impostazioni del Registro di sistema, vedere [Configurazione del supporto transazioni WS\-Atomic](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md).  
  
### Descrizione dell'interfaccia utente  
 **Abilitazione del supporto di rete WS\-Atomic Transaction**:  
  
 L’attivazione di questa casella di comando abilita o disabilita tutti i componenti GUI di questo snap\-in.  
  
 Prima di selezionare questa casella, è necessario assicurarsi che l’accesso alla rete DTC sia abilitato con comunicazione in entrata e\/o in uscita.Questo valore può essere verificato nella scheda **Sicurezza** dello snap\-in MSDTC.  
  
#### Casella di gruppo di rete  
 È possibile specificare la porta HTTPS e impostazioni di sicurezza aggiuntive, ad esempio crittografia SSL, nel gruppo della Rete.Questo gruppo è disabilitato \(visualizzato in grigio\) se le transazioni di rete DTC non sono state abilitate.  
  
 **Porta HTTPS**  
  
 Si tratta del valore della porta HTTPS utilizzata per WS\-AT.Il valore deve essere un numero compreso nell'intervallo da 1 a 65535 \(per rappresentare una porta valida\).Cambiando la porta HTTP si modifica la configurazione del servizio http, di conseguenza l’indirizzo di servizio WS\-AT precedentemente utilizzato viene  Servizio Indirizzo usato viene rilasciato e viene registrato un nuovo indirizzo di servizio WS\-AT in base alla nuova porta.La porta appena selezionata è inoltre crittografata con il certificato attualmente selezionato per la Crittografia SSL.  
  
> [!NOTE]
>  Se prima di eseguire questo strumento è già stato abilitato il firewall, la porta viene automaticamente registrata nell'elenco delle eccezioni.Se il firewall è stato disabilitato prima di eseguire questo strumento, non verranno configurati elementi aggiuntivi riguardanti il firewall.  
  
 Se si abilita il firewall dopo aver configurato WS\-AT, sarà necessario eseguire di nuovo questo strumento e fornire il numero della porta che utilizza questo parametro.Se si disabilita il firewall dopo la configurazione, WS\-AT rimarrà in funzione senza input aggiuntivo.  
  
 **Certificato dell'endpoint**  
  
 Facendo clic sul pulsante **Seleziona** viene visualizzato un elenco dei certificati attualmente disponibili sul computer locale, consentendo all'utente di selezionare il certificato che può essere utilizzato per la crittografia SSL.I certificati devono disporre di una chiave privata.In caso contrario, viene generato un messaggio di errore.  
  
> [!NOTE]
>  Impostando un certificato SSL per una porta selezionata, il certificato SSL originale associato a quella porta, se presente, viene sovrascritto.  
  
 **Account autorizzati**  
  
 Facendo clic sul pulsante **Seleziona** viene richiamato l’editor dell’elenco di controllo di accesso di Windows, nel quale è possibile specificare l'utente o il gruppo che può partecipare nelle transazioni WS\-Atomic selezionando la casella **Consenti** o **Nega** nel gruppo di autorizzazione **Partecipa**.  
  
 **Certificati autorizzati**  
  
 Facendo clic su **Seleziona** viene visualizzato un elenco di certificati attualmente disponibili su LocalMachine.È quindi possibile selezionare quali identità del certificato possono partecipare nelle transazioni WS\-Atomic.  
  
#### Casella di gruppo Timeout  
 La casella di gruppo **Timeout** consente di specificare il timeout predefinito e massimo per una transazione WS\-Atomic.Un valore valido per il timeout in uscita è compreso tra 1 e 3600.Un valore valido per il timeout in entrata è compreso tra 0 e 3600.  
  
#### Casella di gruppo Traccia e registrazione  
 La casella di gruppo **Traccia e registrazione** consente di configurare il livello di traccia e registrazione desiderato.  
  
 Facendo clic su **Opzioni** viene richiamata una pagina nella quale è possibile specificare impostazioni aggiuntive.  
  
 La casella combinata **Livello traccia** consente di scegliere un valore valido dell'enumerazione <xref:System.Diagnostics.TraceLevel>.È inoltre possibile utilizzare le caselle di controllo per specificare se si desidera eseguire attività di traccia, propagazione di attività o raccogliere informazioni identificabili personali.  
  
 È inoltre possibile specificare sessioni di registrazione nella casella di gruppo **Sessione di registrazione**.  
  
> [!NOTE]
>  Quando il provider di traccia WS\-AT è utilizzato da un altro consumer di traccia, non è possibile creare una nuova sessione di registrazione per gli eventi di traccia.Se si tenta di configurare la registrazione in questo momento verrà generato il messaggio di errore non “Errore durante l’abilitazione del provider”.Codice di errore: 1”.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] traccia e registrazione, vedere [Amministrazione e diagnostica](../../../docs/framework/wcf/diagnostics/index.md).  
  
## Vedere anche  
 [Configurazione del supporto transazioni WS\-Atomic](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)   
 [Utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)   
 [Amministrazione e diagnostica](../../../docs/framework/wcf/diagnostics/index.md)