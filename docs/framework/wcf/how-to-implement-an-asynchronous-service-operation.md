---
title: "Procedura: implementare un&#39;operazione del servizio asincrona | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e5d2ea5-d8f8-4712-bd18-ea3c5461702c
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: implementare un&#39;operazione del servizio asincrona
Nelle applicazioni [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], un'operazione del servizio può essere implementata in modo sincrono o asincrono senza imporre al client la modalità di chiamata.È possibile, ad esempio, che operazioni del servizio asincrone vengano chiamate in modo sincrono e che operazioni del servizio sincrone vengano chiamate in modo asincrono.Per un esempio in cui viene illustrato come chiamare in modo asincrono un'operazione in un'applicazione client, vedere [Procedura: chiamare operazioni del servizio in modo asincrono](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] operazioni sincrone e asincrone, vedere [Progettazione dei contratti di servizio](../../../docs/framework/wcf/designing-service-contracts.md) e [Operazioni sincrone e asincrone](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).In questo argomento viene descritta la struttura di base di un'operazione del servizio asincrona \(il codice non è completo\).Per un esempio completo del client e del servizio, vedere [Asynchronous](http://msdn.microsoft.com/it-it/833db946-f511-4f64-a26f-2759a11217c7).  
  
### Implementazione di un'operazione del servizio in modo asincrono  
  
1.  Nel contratto di servizio, dichiarare una coppia di metodi asincroni in base alle linee guida di progettazione asincrona .NET.Il metodo `Begin` prende un parametro, un oggetto callback e un oggetto di stato e restituisce un <xref:System.IAsyncResult?displayProperty=fullName> e un metodo `End` corrispondente che prende un <xref:System.IAsyncResult?displayProperty=fullName> e restituisce il valore restituito.Per ulteriori informazioni sulle chiamate asincrone, vedere la pagina relativa alla [programmazione asincrona di modelli di progettazione](http://go.microsoft.com/fwlink/?LinkId=248221).  
  
2.  Contrassegnare il metodo `Begin` della coppia di metodi asincroni con l'attributo <xref:System.ServiceModel.OperationContractAttribute?displayProperty=fullName> e impostare la proprietà <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A?displayProperty=fullName> su `true`.Nel codice seguente, ad esempio, vengono eseguiti i passaggi 1 e 2.  
  
     [!code-csharp[C_SyncAsyncClient#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#6)]
     [!code-vb[C_SyncAsyncClient#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#6)]  
  
3.  Implementare la coppia di metodi `Begin/End` nella classe del servizio in base alle linee guida di progettazione asincrona.Nell'esempio di codice seguente viene illustrata un'implementazione nella quale una stringa viene scritta nella console sia nella parte `Begin` che nella parte `End` dell'operazione del servizio asincrona e viene restituito al client il valore restituito dell'operazione `End`.Per un esempio completo di codice, vedere la sezione degli esempi.  
  
     [!code-csharp[C_SyncAsyncClient#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#3)]
     [!code-vb[C_SyncAsyncClient#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#3)]  
  
## Esempio  
 Negli esempi di codice seguenti viene illustrato:  
  
1.  Un'interfaccia del contratto di servizio con:  
  
    1.  Un'operazione `SampleMethod` sincrona.  
  
    2.  Un'operazione `BeginSampleMethod` asincrona.  
  
    3.  Una coppia di operazioni `BeginServiceAsyncMethod`\/`EndServiceAsyncMethod` asincrone.  
  
2.  Un'implementazione del servizio tramite un oggetto <xref:System.IAsyncResult?displayProperty=fullName>.  
  
 [!code-csharp[C_SyncAsyncClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#1)]
 [!code-vb[C_SyncAsyncClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#1)]  
  
## Vedere anche  
 [Progettazione dei contratti di servizio](../../../docs/framework/wcf/designing-service-contracts.md)   
 [Operazioni sincrone e asincrone](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)