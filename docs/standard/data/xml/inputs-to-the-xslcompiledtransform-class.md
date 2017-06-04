---
title: "Input alla classe XslCompiledTransform | Microsoft Docs"
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
ms.assetid: 834049f1-ab41-449e-9f10-4a1d0701bc48
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Input alla classe XslCompiledTransform
Il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> accetta tre tipi di input per il documento di origine: un oggetto che implementa l'interfaccia <xref:System.Xml.XPath.IXPathNavigable>, un oggetto <xref:System.Xml.XmlReader> che legge il documento di origine o un URI della stringa.  
  
> [!NOTE]
>  Per impostazione predefinita, la classe <xref:System.Xml.Xsl.XslCompiledTransform> conserva gli spazi vuoti  in conformità con la sezione 3.4 della raccomandazione W3C XSLT 1.0 all'indirizzo http:\/\/www.w3.org\/TR\/xslt.html\#strip.  
  
## Interfaccia IXPathNavigable  
 L'interfaccia <xref:System.Xml.XPath.IXPathNavigable> è implementata nelle classi <xref:System.Xml.XmlNode> e <xref:System.Xml.XPath.XPathDocument>.  Queste classi rappresentano una cache di dati XML in memoria.  
  
-   La classe <xref:System.Xml.XmlNode> è basata sul modello DOM \(Document Object Model\) W3C e include funzionalità di modifica.  
  
-   La classe <xref:System.Xml.XPath.XPathDocument> è un archivio dati di sola lettura basato sul modello dati XPath.  Si consiglia di usare la classe <xref:System.Xml.XPath.XPathDocument> per l'elaborazione di XSLT,  in quanto fornisce prestazioni più veloci rispetto alla classe <xref:System.Xml.XmlNode>.  
  
> [!NOTE]
>  Le trasformazioni si applicano all'intero documento.  In altre parole, se viene passato un nodo diverso dal nodo radice del documento, il processo di trasformazione accederà comunque a tutti i nodi nel documento caricato.  Per trasformare un frammento di nodo, è necessario creare un oggetto contenente solo il frammento di nodo e passare tale oggetto al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  Per altre informazioni, vedere [Procedura: trasformare un frammento di nodo](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md).  
  
 Nell'esempio seguente viene usato il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> per trasformare il file books.xml nel file books.html mediante il foglio di stile transform.xsl.  I file books.xml e transform.xsl si trovano nell'argomento [Procedura: eseguire una trasformazione XSLT utilizzando un assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#1)]
 [!code-vb[XslCompiledTransform.Transform2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#1)]  
  
## Oggetto XmlReader  
 Il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> consente di caricare il nodo corrente del tipo <xref:System.Xml.XmlReader> tramite i relativi elementi figlio.  In tal modo è possibile usare una parte di un documento come documento di contesto.  Dopo la restituzione del metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>, il tipo <xref:System.Xml.XmlReader> viene posizionato sul nodo successivo dopo la fine del documento di contesto.  Se viene raggiunta la fine del documento, l'oggetto <xref:System.Xml.XmlReader> viene posizionato alla fine del file \(EOF\).  
  
 Nell'esempio seguente viene usato il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> per trasformare il file books.xml nel file books.html mediante il foglio di stile transform.xsl.  I file books.xml e transform.xsl si trovano nell'argomento [Procedura: eseguire una trasformazione XSLT utilizzando un assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#2)]
 [!code-vb[XslCompiledTransform.Transform2#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#2)]  
  
## URI della stringa  
 È inoltre possibile specificare l'URI del documento di origine come input di XSLT.  L'URI verrà risolto da un tipo <xref:System.Xml.XmlResolver>.  È possibile specificare il tipo <xref:System.Xml.XmlResolver> da usare passandolo al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  Se non viene specificato alcun oggetto <xref:System.Xml.XmlResolver>, il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> utilizzerà un oggetto <xref:System.Xml.XmlUrlResolver> predefinito senza credenziali.  
  
 Nell'esempio seguente viene usato il metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> per trasformare il file books.xml nel file books.html mediante il foglio di stile transform.xsl.  I file books.xml e transform.xsl si trovano nell'argomento [Procedura: eseguire una trasformazione XSLT utilizzando un assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#3](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#3)]
 [!code-vb[XslCompiledTransform.Transform2#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#3)]  
  
 Per altre informazioni, vedere [Risoluzione delle risorse esterne durante l'elaborazione XSLT](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md).  
  
## Vedere anche  
 [Trasformazioni XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)