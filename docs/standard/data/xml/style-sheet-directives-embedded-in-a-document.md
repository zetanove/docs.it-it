---
title: "Fogli di stile incorporati in un documento | Microsoft Docs"
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
ms.assetid: d79fb295-ebc7-438d-ba1b-05be7d534834
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Fogli di stile incorporati in un documento
Può accadere che il codice XML esistente contenga la direttiva dei fogli di stile di `<?xml:stylesheet?>` che viene accettata da Microsoft Internet Explorer come alternativa alla sintassi `<?xml-stylesheet?>`.  Quando i dati XML contengono una direttiva `<?xml:stylesheet?>`, come nei dati seguenti, se si tenta di caricare questi dati nel DOM XML, viene generata un'eccezione.  
  
```  
<?xml version="1.0" ?>  
<?xml:stylesheet type="text/xsl" href="test2.xsl"?>  
<root>  
    <test>Node 1</test>  
    <test>Node 2</test>  
</root>  
```  
  
 Questo si verifica perché `<?xml:stylesheet?>` viene considerata una **ProcessingInstruction** non valida per il DOM.  In base alla specifica XML degli spazi dei nomi, una **ProcessingInstruction** può essere solo un NCName \(No Column Name, nome senza due punti\).  
  
 In base alla sezione 6 della specifica sugli spazi dei nomi in XML, la conformità dei metodi **Load** e **LoadXml** alla specifica significa che in un documento:  
  
-   Tutti i tipi di elementi e i nomi di attributi contengono uno zero o un segno di due punti.  
  
-   Nessun nome di entità, destinazione di ProcessingInstruction o nome di notazione contiene alcun segno di due punti.  
  
 Poiché `<?xml:stylesheet?>` contiene un segno di due punti, viene violata la regola del secondo punto.  
  
 Secondo la raccomandazione W3C \(World Wide Web Consortium\) Associating Style Sheets with XML documents Version 1.0 \(informazioni in lingua inglese\), disponibile all'indirizzo www.w3.org\/TR\/xml\-stylesheet, l'istruzione di elaborazione per associare un foglio di stile XSL a un documento XML è `<?xml-stylesheet?>`, con un trattino al posto del segno di due punti.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)