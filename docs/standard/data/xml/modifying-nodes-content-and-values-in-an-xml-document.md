---
title: "Modifica di nodi, contenuto e valori in un documento XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 761773e0-db72-4986-b9f5-a522213d8397
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Modifica di nodi, contenuto e valori in un documento XML
Sono disponibili molti modi per modificare i nodi e il contenuto in un documento.  È possibile:  
  
-   Modificare il valore dei nodi usando la proprietà <xref:System.Xml.XmlNode.Value%2A>.  
  
-   Modificare un intero set di nodi, sostituendoli con nodi nuovi.  Questa operazione viene eseguita tramite la proprietà <xref:System.Xml.XmlNode.InnerXml%2A>.  
  
-   Sostituire i nodi esistenti con nodi nuovi usando il metodo <xref:System.Xml.XmlNode.RemoveChild%2A>.  
  
-   Aggiungere ulteriori caratteri ai nodi che ereditano dalla classe <xref:System.Xml.XmlCharacterData> usando il metodo <xref:System.Xml.XmlCharacterData.AppendData%2A>, <xref:System.Xml.XmlCharacterData.InsertData%2A> o <xref:System.Xml.XmlCharacterData.ReplaceData%2A>.  
  
-   Modificare il contenuto rimuovendo una serie di caratteri con il metodo <xref:System.Xml.XmlCharacterData.DeleteData%2A> nei tipi di nodo che ereditano da <xref:System.Xml.XmlCharacterData>.  
  
 Una tecnica semplice per modificare il valore di un nodo consiste nell'usare `node.Value = "new value";`.  Nella tabella seguente sono elencati i tipi di nodo sui quali funziona quest'unica riga di codice ed esattamente quali dati verranno modificati per quel tipo di nodo.  
  
|Tipo di nodo|Dati modificati|  
|------------------|---------------------|  
|Attributo|Valore dell'attributo.|  
|CDATASection|Contenuto di CDATASection.|  
|Commento|Contenuto del commento.|  
|ProcessingInstruction|Contenuto eccetto la destinazione.|  
|Text|Il contenuto del testo.|  
|XmlDeclaration|Il contenuto della dichiarazione, esclusi i markup `<?xml` e `?>`.|  
|Whitespace|Il valore dello spazio vuoto.  È possibile impostare il valore in modo che sia uno dei quattro caratteri di spazio vuoto XML riconosciuti: spazio, tabulazione, ritorno a capo o avanzamento riga.|  
|SignificantWhitespace|Il valore dello spazio vuoto significativo.  È possibile impostare il valore in modo che sia uno dei quattro caratteri di spazio vuoto XML riconosciuti: spazio, tabulazione, ritorno a capo o avanzamento riga.|  
  
 Qualsiasi tipo di nodo non elencato nella tabella non è un tipo di nodo valido in base al quale impostare il valore.  Se si imposta un valore su qualsiasi altro tipo di nodo, viene generato un tipo <xref:System.InvalidOperationException>.  
  
 La proprietà <xref:System.Xml.XmlNode.InnerXml%2A> consente di modificare il markup dei nodi figlio per il nodo corrente.  Se si imposta questa proprietà, i nodi figlio vengono sostituiti con il contenuto analizzato della stringa specificata.  L'analisi viene eseguita nel contesto dello spazio dei nomi corrente.  Inoltre, la proprietà <xref:System.Xml.XmlNode.InnerXml%2A> consente di rimuovere le dichiarazioni ridondanti dello spazio dei nomi.  Di conseguenza, anche in caso di numerose operazioni di taglia e incolla, le dimensioni del documento non aumenteranno a causa di dichiarazioni ridondanti dello spazio dei nomi.  Per un esempio di codice in cui viene illustrato l'effetto degli spazi dei nomi sull'operazione <xref:System.Xml.XmlNode.InnerXml%2A>, vedere la proprietà <xref:System.Xml.XmlDocument.InnerXml%2A>.  
  
 Quando vengono usati, i metodi <xref:System.Xml.XmlCharacterData.ReplaceData%2A> e <xref:System.Xml.XmlNode.RemoveChild%2A> restituiscono il nodo sostituito o rimosso,  che può quindi essere reinserito altrove nel DOM XML.  Il metodo <xref:System.Xml.XmlCharacterData.ReplaceData%2A> consente di eseguire due controlli di convalida sul nodo che viene inserito nel documento.  Il primo controllo assicura che il nodo stia diventando figlio di un nodo che può avere nodi figlio del suo tipo.  Il secondo controllo assicura che il nodo inserito non sia progenitore del nodo del quale sta diventando figlio.  In presenza della violazione di una di queste condizioni, viene generato un tipo <xref:System.InvalidOperationException>.  
  
 L'aggiunta o la rimozione di un figlio in sola lettura da un nodo che può essere modificato è un'operazione valida.  Ma se si tenta di modificare il nodo in sola lettura, viene generato un tipo <xref:System.InvalidOperationException>.  Un esempio di questa situazione è la modifica dei nodi figlio di un nodo <xref:System.Xml.XmlEntityReference>.  Poiché i nodi figlio sono in sola lettura, non possono essere modificati  e se si tenta di modificarli, viene generato un tipo <xref:System.InvalidOperationException>.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)