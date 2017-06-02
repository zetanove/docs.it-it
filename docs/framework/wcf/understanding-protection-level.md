---
title: "Informazioni sul livello di protezione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Proprietà ProtectionLevel"
  - "WCF, sicurezza"
ms.assetid: 0c034608-a1ac-4007-8287-b1382eaa8bf2
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Informazioni sul livello di protezione
La proprietà `ProtectionLevel` è disponibile in molte classi diverse, ad esempio nelle classi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute>.Tale proprietà controlla la modalità di protezione di una parte del messaggio o dell'intero messaggio.In questo argomento ne viene illustrata la funzionalità in [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] e il funzionamento.  
  
 Per istruzioni sull'impostazione del livello di protezione, vedere [Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md).  
  
> [!NOTE]
>  È possibile impostare i livelli di protezione solo nel codice, non nella configurazione.  
  
## Nozioni fondamentali  
 Per comprendere la funzionalità del livello di protezione, le indicazioni di base sono le seguenti:  
  
-   Per tutte le parti di un messaggio sono disponibili tre livelli di protezione di base.La proprietà \(ovunque sia presente\) viene impostata su uno dei valori dell'enumerazione <xref:System.Net.Security.ProtectionLevel>.In ordine di protezione crescente, questi valori sono:  
  
    -   `None`.  
  
    -   `Sign`.Alla parte protetta viene apposta la firma digitale.In questo modo si garantisce il rilevamento di eventuali manomissioni della parte di messaggio protetta.  
  
    -   `EncryptAndSign`.Prima dell'apposizione della firma, la parte del messaggio viene crittografata per garantirne la riservatezza.  
  
-   È possibile impostare i requisiti di protezione solo per i *dati dell'applicazione* dotati di questa funzionalità.Ad esempio, le intestazioni WS\-Addressing sono dati dell'infrastruttura e pertanto `ProtectionLevel` non ha alcun effetto su di esse.  
  
-   Quando la modalità di sicurezza è impostata su `Transport`, l'intero messaggio è protetto dal meccanismo di trasporto.Di conseguenza, l'impostazione di un livello di protezione separato per parti diverse di un messaggio non ha alcun effetto.  
  
-   `ProtectionLevel` consente allo sviluppatore di impostare il *livello minimo* a cui un'associazione deve conformarsi.Quando un servizio viene distribuito, l'associazione effettiva specificata nella configurazione non necessariamente è in grado di supportare il livello minimo.Ad esempio, per impostazione predefinita, la classe <xref:System.ServiceModel.BasicHttpBinding> non fornisce protezione \(sebbene sia possibile attivarla\).Pertanto, se la si utilizza con un contratto con un'impostazione diversa da `None`, verrà generata un'eccezione.  
  
-   Se il servizio richiede che per tutti i messaggi il livello minimo di `ProtectionLevel` sia `Sign`, è possibile che un client, eventualmente creato mediante una tecnologia non [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], crittografi e firmi tutti i messaggi, ovvero più del minimo richiesto.In questo caso, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] non genererà un'eccezione perché il client ha fatto qualcosa in più del minimo.Si noti tuttavia che le applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(servizi o client\) non proteggeranno in eccesso una parte del messaggio, se possibile, ma si conformeranno al livello minimo.Inoltre, quando si utilizza `Transport` come modalità di sicurezza, è possibile che il trasporto protegga in eccesso il flusso del messaggio perché non è intrinsecamente in grado di fornire protezione a un livello più granulare.  
  
-   Se si imposta in modo esplicito la proprietà `ProtectionLevel` su `Sign` o su `EncryptAndSign`, è necessario utilizzare un'associazione protetta; in caso contrario verrà generata un'eccezione.  
  
-   Se si seleziona un'associazione protetta e non si imposta la proprietà `ProtectionLevel` nel contratto, tutti i dati dell'applicazione verranno crittografati e firmati.  
  
-   Se si seleziona un'associazione non protetta \(ad esempio, per impostazione predefinita la classe `BasicHttpBinding` non è protetta\) e non si imposta in modo esplicito la proprietà `ProtectionLevel`, non verrà protetto alcun dato dell'applicazione.  
  
-   Se si sta utilizzando un'associazione che applica la protezione a livello di trasporto, tutti i dati dell'applicazione saranno protetti in base alle funzionalità del trasporto.  
  
-   Se si utilizza un'associazione che applica la protezione a livello di messaggio, i dati dell'applicazione saranno protetti in base ai livelli di protezione impostati sul contratto.Se non si specifica un livello di protezione, tutti i dati dell'applicazione contenuti nei messaggi verranno crittografati e firmati.  
  
-   La proprietà `ProtectionLevel` può essere impostata a livelli di ambito diversi.All'ambito è associata una gerarchia, che viene illustrata nella sezione successiva.  
  
## Ambito  
 L'impostazione di `ProtectionLevel` nell'API superiore determina il livello di tutti gli altri livelli sottostanti.Se `ProtectionLevel` viene impostato su un valore diverso a un livello inferiore, tutte le API al di sotto di tale livello nella gerarchia verranno reimpostate sul nuovo livello \(le API al di sopra di esso continueranno tuttavia a essere determinate dal livello superiore\).La gerarchia è la seguente.Gli attributi allo stesso livello sono pari.  
  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
 <xref:System.ServiceModel.FaultContractAttribute>  
  
 <xref:System.ServiceModel.MessageContractAttribute>  
  
 <xref:System.ServiceModel.MessageHeaderAttribute>  
  
 <xref:System.ServiceModel.MessageBodyMemberAttribute>  
  
## Programmazione del livello di protezione  
 Per programmare `ProtectionLevel` in corrispondenza di un qualsiasi punto della gerarchia, è sufficiente impostare la proprietà su un valore appropriato quando si applica l'attributo.Per alcuni esempi, vedere [Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md).  
  
> [!NOTE]
>  Per l'impostazione della proprietà su contratti di messaggio ed errori, è necessario conoscere il funzionamento di tali funzionalità.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md) e [Utilizzo dei contratti di messaggio](../../../docs/framework/wcf/feature-details/using-message-contracts.md).  
  
## Dipendenza da WS\-Addressing  
 Nella maggior parte dei casi, l'utilizzo dello [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare un client garantisce che i contratti del client e del servizio siano identici.In presenza di contratti apparentemente identici, è tuttavia possibile che il client generi un'eccezione.Questo si verifica quando un'associazione non supporta la specifica WS\-Addressing e sul contratto sono specificati più livelli di protezione.Un esempio si ha con la classe <xref:System.ServiceModel.BasicHttpBinding> che non supporta la specifica o quando si crea un'associazione personalizzata che non supporta WS\-Addressing.Per abilitare livelli di protezione diversi su un singolo contratto, la funzionalità `ProtectionLevel` si basa sulla specifica WS\-Addressing.Se l'associazione non supporta la specifica WS\-Addressing, tutti i livelli verranno impostati sullo stesso livello di protezione.Il livello di protezione effettivo per tutti gli ambiti del contratto verrà impostato sul livello di protezione più sicuro utilizzato nel contratto.  
  
 Si può in questo modo generare un problema a prima vista difficile da risolvere con il debug.È possibile creare un contratto client \(un'interfaccia\) che include metodi per più di un servizio.In altri termini, la stessa interfaccia viene utilizzata per creare un client che comunica con molti servizi e tale singola interfaccia contiene i metodi per tutti i servizi.In questo raro scenario, lo sviluppatore deve accertarsi di richiamare solo quei metodi che sono applicabili a ogni particolare servizio.Se l'associazione è la classe <xref:System.ServiceModel.BasicHttpBinding>, non possono essere supportati più livelli di protezione.È tuttavia possibile che un servizio che risponde al client risponda a un client con un livello di protezione inferiore a quello richiesto.In questo caso, il client genererà un'eccezione poiché prevedeva un livello di protezione più elevato.  
  
 Tale problema viene dimostrato nell'esempio di codice seguentein cui viene illustrato un contratto di servizio e un contratto client.Si supponga che l'associazione sia l'elemento [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).Tutte le operazioni relative a un contratto hanno pertanto lo stesso livello di protezione.Tale livello di protezione uniforme viene determinato come livello massimo di protezione per tutte le operazioni.  
  
 Il contratto di servizio è il seguente:  
  
 [!code-csharp[c_ProtectionLevel#7](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#7)]
 [!code-vb[c_ProtectionLevel#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#7)]  
  
 Nell'esempio di codice seguente viene illustrata l'interfaccia del contratto client.Si noti che è incluso un metodo `Tax` che viene esteso per essere utilizzato con un servizio diverso:  
  
 [!code-csharp[c_ProtectionLevel#8](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#8)]
 [!code-vb[c_ProtectionLevel#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#8)]  
  
 Quando il client chiama il metodo `Price`, durante la ricezione di una risposta dal servizio, verrà generata un'eccezione.Questo avviene perché il client non specifica un `ProtectionLevel` su `ServiceContractAttribute` e pertanto il client utilizza l'impostazione predefinita \(<xref:System.Net.Security.ProtectionLevel>\) per tutti i metodi, incluso il metodo `Price`.Il servizio restituisce tuttavia il valore utilizzando il livello <xref:System.Net.Security.ProtectionLevel> perché il contratto di servizio definisce un solo metodo il cui livello di protezione è impostato su <xref:System.Net.Security.ProtectionLevel>.In questo caso, il client genererà un errore durante la convalida della risposta dal servizio.  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.MessageContractAttribute>   
 <xref:System.ServiceModel.MessageHeaderAttribute>   
 <xref:System.ServiceModel.MessageBodyMemberAttribute>   
 <xref:System.Net.Security.ProtectionLevel>   
 [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md)   
 [Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)   
 [Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)   
 [Utilizzo dei contratti di messaggio](../../../docs/framework/wcf/feature-details/using-message-contracts.md)