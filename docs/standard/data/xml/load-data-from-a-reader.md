---
title: "Caricamento di dati da un lettore | Microsoft Docs"
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
ms.assetid: 7e74918c-bc72-4977-a49b-e1520a6d8f60
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Caricamento di dati da un lettore
Se un documento XML viene caricato usando il metodo <xref:System.Xml.XmlDocument.Load%2A> e un parametro di un lettore <xref:System.Xml.XmlReader>, si otterrà un comportamento diverso rispetto alla situazione in cui i dati vengono caricati dagli altri formati.  Se il lettore è nel suo stato iniziale, il metodo <xref:System.Xml.XmlDocument.Load%2A> utilizzerà l'intero contenuto del lettore e compilerà il modello DOM XML usando tutti i dati nel lettore.  
  
 Se il lettore è già posizionato su un nodo in un punto del documento e quindi viene passato al metodo <xref:System.Xml.XmlDocument.Load%2A>, <xref:System.Xml.XmlDocument.Load%2A> tenta di leggere il nodo corrente e tutti i nodi di pari livello fino al tag di fine che chiude il livello corrente nella memoria.  La riuscita del metodo <xref:System.Xml.XmlDocument.Load%2A> dipende dal nodo sul quale si trova il lettore al momento del caricamento, in quanto con il metodo <xref:System.Xml.XmlDocument.Load%2A> viene verificato che l'XML del lettore sia nel formato corretto.  In caso contrario, il metodo <xref:System.Xml.XmlDocument.Load%2A> genererà un’eccezione.  Il set di nodi seguente, ad esempio, contiene due elementi di livello radice e poiché l'XML non ha un formato corretto, <xref:System.Xml.XmlDocument.Load%2A> genera un'eccezione.  
  
-   Nodo Comment, seguito da un nodo Element, seguito da un nodo Element, seguito da un nodo EndElement.  
  
 Dal seguente set di nodi viene creato un DOM incompleto, in quanto non vi è alcun elemento di livello radice.  
  
-   Nodo Comment, seguito da un nodo ProcessingInstruction, seguito da un nodo Comment, seguito da un nodo EndElement.  
  
 In questo caso non viene generata un'eccezione e i dati vengono caricati.  È possibile aggiungere un elemento radice sopra questi nodi e creare un XML in formato corretto che potrà essere salvato senza errori.  
  
 Se il lettore è posizionato su un nodo foglia non valido per il livello radice di un documento, quale un nodo spazio vuoto o attributo, il lettore continuerà a leggere finché non si posizionerà su un nodo che può essere usato per il livello radice.  Il caricamento del documento avverrà a partire da questo punto.  
  
 Per impostazione predefinita, il metodo <xref:System.Xml.XmlDocument.Load%2A> non verifica se l'XML è valido usando la DTD o la convalida dello schema.  Verifica solo che l'XML sia in formato corretto.  Affinché avvenga la convalida, è necessario creare un tipo <xref:System.Xml.XmlReader> usando la classe <xref:System.Xml.XmlReaderSettings>.  La classe <xref:System.Xml.XmlReader> consente di applicare la convalida usando una DTD o uno schema XSD \(Schema definition language\).  La proprietà <xref:System.Xml.ValidationType> della classe <xref:System.Xml.XmlReaderSettings> consente di determinare se l'istanza <xref:System.Xml.XmlReader> applica la convalida.  Per altre informazioni sulla convalida dei dati XML, vedere la sezione Note della pagina di riferimento <xref:System.Xml.XmlReader>.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)