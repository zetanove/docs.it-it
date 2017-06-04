---
title: "Procedura: specificare un&#39;associazione al servizio in codice | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: specificare un&#39;associazione al servizio in codice
In questo esempio viene definito un contratto `ICalculator` per un servizio di calcolatrice. Il servizio viene implementato nella classe `CalculatorService` e il relativo endpoint viene quindi definito in codice, dove si specifica che il servizio deve utilizzare la classe <xref:System.ServiceModel.BasicHttpBinding>.  
  
 La procedura in genere consigliata consiste nello specificare le informazioni su associazione e indirizzo nella configurazione in modo dichiarativo anziché in modo imperativo nel codice.La definizione di endpoint nel codice non è generalmente pratica perché le associazioni e gli indirizzi per un servizio distribuito sono solitamente diversi da quelli utilizzati durante lo sviluppo del servizio.Più in generale, se le informazioni su associazione e indirizzo non vengono incluse nel codice, tali dati possono essere modificati senza dover compilare o distribuire nuovamente l'applicazione.  
  
 Per una descrizione di come configurare questo servizio utilizzando elementi di configurazione anziché tramite codice, vedere [Procedura: specificare un'associazione al servizio in configurazione](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
### Per specificare in codice l'utilizzo dell'associazione BasicHttpBinding per il servizio  
  
1.  Definire un contratto di servizio per il tipo di servizio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2.  Implementare il contratto di servizio in una classe di servizio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3.  Nell'applicazione host, creare l'indirizzo di base del servizio e l'associazione da utilizzare con il servizio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4.  Creare l'host del servizio, aggiungere l'endpoint e quindi aprire l'host.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### Per modificare i valori predefiniti delle proprietà dell'associazione  
  
1.  Per modificare uno dei valori di proprietà predefiniti della classe <xref:System.ServiceModel.BasicHttpBinding>, impostare il valore di proprietà dell'associazione sul nuovo valore prima di creare l'host.Ad esempio, per modificare i valori di timeout di apertura e chiusura predefiniti da 1 minuto a 2 minuti, utilizzare il codice seguente:  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## Vedere anche  
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Specifica di un indirizzo endpoint](../../../docs/framework/wcf/specifying-an-endpoint-address.md)