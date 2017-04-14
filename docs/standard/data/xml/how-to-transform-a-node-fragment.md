---
title: "Procedura: trasformare un frammento di nodo | Microsoft Docs"
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
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Procedura: trasformare un frammento di nodo
Quando si trasformano i dati contenuti in un oggetto <xref:System.Xml.XmlDocument> o in un oggetto <xref:System.Xml.XPath.XPathDocument>, le trasformazioni XSLT si applicano a un documento completo.  In altre parole, se viene passato un nodo diverso dal nodo radice del documento, il processo di trasformazione accederà comunque a tutti i nodi nel documento caricato.  Per trasformare un frammento di nodo, è necessario creare un oggetto contenente solo il frammento di nodo e passare tale oggetto al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## Procedure  
  
#### Per trasformare un frammento di nodo  
  
1.  Creare un oggetto contenente il documento di origine.  
  
2.  Individuare il frammento di nodo da trasformare.  
  
3.  Creare un oggetto separato con il frammento di nodo.  
  
4.  Passare il frammento di nodo al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## Esempio  
 Nell'esempio seguente un frammento di nodo viene trasformato e il risultato viene visualizzato sulla console.  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### Input  
  
##### books.xml  
 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### single.xsl  
 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### Output  
 Il titolo del libro è L'uomo di fiducia.  
  
## Vedere anche  
 [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)