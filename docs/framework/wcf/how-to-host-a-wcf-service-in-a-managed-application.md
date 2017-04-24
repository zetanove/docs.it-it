---
title: "Procedura: ospitare un servizio WCF in un&#39;applicazione gestita | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 5eb29db0-b6dc-4e77-8c68-0a62f79d743b
caps.latest.revision: 42
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 42
---
# Procedura: ospitare un servizio WCF in un&#39;applicazione gestita
Per ospitare un servizio all'interno di un'applicazione gestita, incorporare il codice per il servizio nel codice dell'applicazione, definire un endpoint per il servizio in modo imperativo nel codice, in modo dichiarativo tramite la configurazione o tramite endpoint predefiniti, quindi creare un'istanza di <xref:System.ServiceModel.ServiceHost>.  
  
 Per iniziare a ricevere messaggi, chiamare <xref:System.ServiceModel.ICommunicationObject.Open%2A> su <xref:System.ServiceModel.ServiceHost>.In tal modo viene creato e aperto il listener per il servizio.Questo tipo di hosting di un servizio viene spesso chiamato "self\-hosting"" perché è la stessa applicazione gestita a svolgere il lavoro di hosting.Per chiudere il servizio, chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Close%2A?displayProperty=fullName> su <xref:System.ServiceModel.ServiceHost>.  
  
 Un servizio può essere ospitato anche in un servizio Windows gestito, in Internet Information Services \(IIS\) o nel servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\).[!INCLUDE[crabout](../../../includes/crabout-md.md)] opzioni di hosting per un servizio, vedere [Servizi host](../../../docs/framework/wcf/hosting-services.md).  
  
 L'hosting di un servizio in un'applicazione gestita è l'opzione più flessibile perché richiede la distribuzione di un'infrastruttura minima.[!INCLUDE[crabout](../../../includes/crabout-md.md)] servizi di hosting nelle applicazioni gestite, vedere [Hosting in un'applicazione gestita](../../../docs/framework/wcf/feature-details/hosting-in-a-managed-application.md).  
  
 Nella procedura seguente viene illustrato come implementare un servizio indipendente in un'applicazione console.  
  
### Per creare un servizio indipendente  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
2.  Nell'elenco **Modelli installati** selezionare **Visual C\#**, **Windows** o **Visual Basic**, quindi **Windows**.In base alle impostazioni di [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], sotto il nodo **Altri linguaggi** nell'elenco **Modelli istallati** potrebbero essere presenti una o entrambe queste opzioni.  
  
3.  Selezionare **Applicazione console** dall'elenco **Windows**.Digitare `SelfHost` nella casella **Nome**, quindi fare clic su **OK**.  
  
4.  Fare clic con il pulsante destro del mouse su **SelfHost** in **Esplora soluzioni** e selezionare **Aggiungi riferimento**.Selezionare **System.ServiceModel** nella scheda **.NET**, quindi fare clic su **OK**.  
  
    > [!TIP]
    >  Se la finestra **Esplora soluzioni** non è visibile, selezionarla nel menu **Visualizza**.  
  
5.  Fare doppio clic sul file **Program.cs** o **Module1.vb** nella finestra **Esplora soluzioni** per aprirlo nella finestra del codice.Aggiungere le seguenti istruzioni all'inizio del file.  
  
     [!code-csharp[CFX_SelfHost4#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#1)]
     [!code-vb[CFX_SelfHost4#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#1)]  
  
6.  Definire e implementare un contratto di servizio.In questo esempio viene definito un codice `HelloWorldService` che restituisce un messaggio in base all'input del servizio.  
  
     [!code-csharp[CFX_SelfHost4#2](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#2)]
     [!code-vb[CFX_SelfHost4#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#2)]  
  
    > [!NOTE]
    >  [!INCLUDE[crabout](../../../includes/crabout-md.md)] modalità di definizione e di implementazione di un'interfaccia del servizio, vedere [Procedura: definire il contratto di servizio](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md) e [Procedura: implementare un contratto di servizio](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md).  
  
7.  All'inizio del metodo `Main`, creare un'istanza della classe <xref:System.Uri> con l'indirizzo di base del servizio.  
  
     [!code-csharp[CFX_SelfHost4#3](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#3)]
     [!code-vb[CFX_SelfHost4#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#3)]  
  
8.  Creare un'istanza della classe <xref:System.ServiceModel.ServiceHost>, passando un <xref:System.Type> che rappresenta il tipo di servizio e l'URI \(Uniform Resource Identifier\) dell'indirizzo di base a [ServiceHost\(Type, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Type%2CSystem.Uri%5B%5D%29>.Abilitare la pubblicazione dei metadati, quindi chiamare il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A> sull'oggetto <xref:System.ServiceModel.ServiceHost> per inizializzare il servizio e prepararlo a ricevere messaggi.  
  
     [!code-csharp[CFX_SelfHost4#4](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#4)]
     <!-- TODO: review snippet reference [!code-vb[CFX_SelfHost4#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#4)]  -->  
  
    > [!NOTE]
    >  In questo esempio vengono utilizzati endpoint predefiniti e per il servizio non è necessario alcun file di configurazione.Se non è specificato alcun endpoint, il runtime ne crea uno per ogni indirizzo di base per ciascun contratto del servizio implementato.[!INCLUDE[crabout](../../../includes/crabout-md.md)] endpoint predefiniti, vedere [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
9. Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
### Per eseguire il test del servizio  
  
1.  Premere CTRL\+F5 per eseguire il servizio.  
  
2.  Aprire **Client di prova WCF**.  
  
    > [!TIP]
    >  Per visualizzare **Client di prova WCF**, aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], quindi eseguire **WcfTestClient.exe**.  
  
3.  Scegliere **Aggiungi servizio** dal menu **Progetto**.  
  
4.  Digitare `http://localhost:8080/hello` nella casella degli indirizzi, quindi fare clic su **OK**.  
  
    > [!TIP]
    >  Verificare che il servizio sia in esecuzione. In caso contrario, il passaggio non viene eseguito.Se nel codice è stato modificato l'indirizzo di base, in questo passaggio utilizzare l'indirizzo di base modificato.  
  
5.  Fare doppio clic su **SayHello** sotto il nodo **Progetti di servizi**.Nella colonna **Valore** dell'elenco **Richiesta** digitare il proprio nome, quindi fare cic su **Richiama**.Nell'elenco **Risposta** verrà visualizzato un messaggio di risposta.  
  
## Esempio  
 Nell'esempio seguente viene creato un oggetto <xref:System.ServiceModel.ServiceHost> per ospitare un servizio di tipo `HelloWorldService`, quindi viene chiamato il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A> su <xref:System.ServiceModel.ServiceHost>.Nel codice viene fornito un indirizzo di base, viene abilitata la pubblicazione di metadati e vengono utilizzati endpoint predefiniti.  
  
 [!code-csharp[CFX_SelfHost4#5](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#5)]
 [!code-vb[CFX_SelfHost4#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#5)]  
  
## Vedere anche  
 <xref:System.Uri>   
 <xref:System.Configuration.ConfigurationManager.AppSettings%2A>   
 <xref:System.Configuration.ConfigurationManager>   
 [Procedura: ospitare un servizio WCF in IIS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)   
 [Servizio indipendente](../../../docs/framework/wcf/samples/self-host.md)   
 [Servizi host](../../../docs/framework/wcf/hosting-services.md)   
 [Procedura: definire il contratto di servizio](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)   
 [Procedura: implementare un contratto di servizio](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md)