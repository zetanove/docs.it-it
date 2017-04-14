---
title: "Risoluzione di fogli di stile e documenti XSLT esterni | Microsoft Docs"
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
ms.assetid: 920cfe3b-d525-4bb2-abf6-9431651f9cf9
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Risoluzione di fogli di stile e documenti XSLT esterni
Durante una trasformazione si presentano vari casi in cui può essere necessario risolvere le risorse esterne.  
  
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
 Durante una trasformazione si presentano vari casi in cui può essere necessario risolvere le risorse esterne:  
  
-   Durante l'esecuzione del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> per individuare un foglio di stile esterno.  
  
-   Durante l'esecuzione del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> per risolvere gli eventuali elementi `<xsl:include>` o `<xsl:import>` presenti nel foglio di stile.  
  
-   Durante l'esecuzione del metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> per risolvere eventuali funzioni `document()`.  
  
## Utilizzo della classe XmlResolver  
 Se per accedere a una risorsa di rete è richiesta l'autenticazione, usare i metodi <xref:System.Xml.Xsl.XslTransform.Load%2A> contenenti un parametro <xref:System.Xml.XmlResolver> per passare l'oggetto <xref:System.Xml.XmlResolver> che contiene il set di credenziali necessario.  
  
 Se si dispone di un oggetto <xref:System.Xml.XmlResolver> personalizzato che si desidera usare o se è necessario specificare credenziali diverse, occorre eseguire le attività riportate nella tabella seguente, che dipendono dal momento in cui è necessario risolvere la risorsa esterna.  
  
|Processo che richiede la risoluzione|Attività richiesta|  
|------------------------------------------|------------------------|  
|Durante l'esecuzione del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> per individuare il foglio di stile.|Specificare il metodo di overload <xref:System.Xml.Xsl.XslTransform.Load%2A> che accetta come parametro il tipo <xref:System.Xml.XmlResolver>, qualora il foglio di stile si trovi in una risorsa che richiede credenziali.|  
|Durante l'esecuzione del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> per risolvere `<xsl:include>` o `<xsl:import>`.|Specificare il metodo di overload <xref:System.Xml.Xsl.XslTransform.Load%2A> che accetta come parametro un tipo <xref:System.Xml.XmlResolver>.  Il tipo <xref:System.Xml.XmlResolver> viene usato per caricare i fogli di stile a cui fa riferimento l'istruzione `import` o `include`.  Se viene passato il valore `null`, le risorse esterne non vengono risolte.|  
|Durante una trasformazione per risolvere eventuali funzioni `document()`.|Specificare il tipo <xref:System.Xml.XmlResolver> durante la trasformazione usando il metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> che accetta un argomento <xref:System.Xml.XmlResolver>.|  
  
 Oltre ai dati XML iniziali forniti dal flusso di input, la funzione `document()` consente di recuperare da un foglio di stile anche altre risorse XML.  Poiché questa funzione consente di includere i dati XML che si trovano in altre posizioni, se al metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> viene fornito un tipo <xref:System.Xml.XmlResolver> con valore `null`, la funzione `document()` non può essere eseguita.  Se si desidera usare la funzione `document()`, usare il metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> che accetta un tipo <xref:System.Xml.XmlResolver> come parametro, oltre a impostare il set di autorizzazioni appropriato.  
  
 Per altre informazioni sul metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> e sul relativo uso del tipo <xref:System.Xml.XmlResolver>, vedere il metodo <xref:System.Xml.Xsl.XslTransform.Load%28System.String%2CSystem.Xml.XmlResolver%29?displayProperty=fullName>.  
  
 Quando viene chiamato il metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A>, le autorizzazioni vengono calcolate in base all'evidenza fornita in fase di caricamento e il set di autorizzazioni viene assegnato all'intero processo di trasformazione.  Se la funzione `document()` tenta di avviare un'azione che richiede autorizzazioni non presenti nel set, viene generata un'eccezione.  
  
## Vedere anche  
 [Trasformazioni XSLT con la classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)   
 [Output da un XslTransform](../../../../docs/standard/data/xml/outputs-from-an-xsltransform.md)   
 [Trasformazioni XSLT su diversi archivi](../../../../docs/standard/data/xml/xslt-transformations-over-different-stores.md)   
 [XsltArgumentList per i parametri dei fogli di stile e gli oggetti di estensione](../../../../docs/standard/data/xml/xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md)   
 [Scripting dei fogli di stile XSLT utilizzando \<msxsl:script\>](../../../../docs/standard/data/xml/xslt-stylesheet-scripting-using-msxsl-script.md)   
 [Supporto per la funzione msxsl:node\-set\(\)](../../../../docs/standard/data/xml/support-for-the-msxsl-node-set-function.md)   
 [XPathNavigator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)   
 [XPathNodeIterator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)   
 [Input di XPathDocument in XslTransform](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)   
 [Input di XmlDataDocument in XslTransform](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)   
 [Input di XmlDocument in XslTransform](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)