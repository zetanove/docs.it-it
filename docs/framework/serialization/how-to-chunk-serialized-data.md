---
title: "Procedura: bloccare i dati serializzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "serializzazione binaria, blocco dei dati"
  - "serializzazione binaria, esempi"
  - "blocco dei dati serializzati"
  - "blocco di dati"
  - "blocco di set di dati di grandi dimensioni"
  - "serializzazione, blocco dei dati"
  - "serializzazione, esempi"
ms.assetid: 22f1b818-7e0d-428a-8680-f17d6ebdd185
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: bloccare i dati serializzati
Di seguito sono illustrati due problemi che si verificano durante l'invio di set di dati di grandi dimensioni nei messaggi del servizio Web.  
  
1.  Un working set \(memoria\) di grandi dimensioni, dovuti alla memorizzazione dei dati nel buffer da parte del motore di serializzazione.  
  
2.  Consumo di larghezza di banda non controllato, dovuto all'ingrandimento del 33 percento successivo alla codifica Base64.  
  
 Per risolvere questi problemi, implementare l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable> per controllare la serializzazione e la deserializzazione.In particolare, implementare i metodi <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> e <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> per suddividere i dati.  
  
### Per implementare il chunking lato server  
  
1.  Sul server, il metodo Web deve disattivare la memorizzazione nel buffer ASP.NET e restituire un tipo che implementi <xref:System.Xml.Serialization.IXmlSerializable>.  
  
2.  Il tipo che implementa <xref:System.Xml.Serialization.IXmlSerializable>, suddivide i dati nel metodo <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>.  
  
### Per implementare l'elaborazione lato client  
  
1.  Modificare il metodo Web sul proxy client in modo che restituisca il tipo che implementa <xref:System.Xml.Serialization.IXmlSerializable>.È possibile utilizzare <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> per eseguire automaticamente questa procedura ma tale operazione non viene mostrata in questo esempio.  
  
2.  Implementare il metodo <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> per leggere il flusso di dati suddiviso e scrivere i byte su disco.Questa implementazione genera inoltre eventi relativi allo stato di avanzamento che possono essere utilizzati da un controllo grafico, ad esempio un indicatore di stato.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene mostrato il metodo Web sul client che disattiva la memorizzazione nel buffer ASP.NET.L'esempio mostra inoltre l'implementazione lato client dell'interfaccia <xref:System.Xml.Serialization.IXmlSerializable> che suddivide i dati nel metodo <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>.  
  
 [!code-csharp[HowToChunkSerializedData#1](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#1)]
 [!code-vb[HowToChunkSerializedData#1](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#1)]  
[!code-csharp[HowToChunkSerializedData#2](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#2)]
[!code-vb[HowToChunkSerializedData#2](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#2)]  
[!code-csharp[HowToChunkSerializedData#3](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#3)]
[!code-vb[HowToChunkSerializedData#3](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#3)]  
  
## Compilazione del codice  
  
-   Nel codice riportato di seguito vengono utilizzati i seguenti spazi dei nomi: <xref:System>, <xref:System.Runtime.Serialization>, <xref:System.Web.Services>, <xref:System.Web.Services.Protocols>, <xref:System.Xml>, <xref:System.Xml.Serialization> e <xref:System.Xml.Schema>.  
  
## Vedere anche  
 [Serializzazione personalizzata](../../../docs/framework/serialization/custom-serialization.md)