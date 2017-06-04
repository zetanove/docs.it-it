---
title: "Funzioni e variabili definite dall&#39;utente | Microsoft Docs"
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
ms.assetid: 4772f20e-1e7f-496e-93c2-1484473be555
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Funzioni e variabili definite dall&#39;utente
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usato per interagire con i dati dell'oggetto <xref:System.Xml.XPath.XPathDocument>.  È possibile integrare le funzioni XPath standard implementando le funzioni di estensione e le variabili da usare nelle espressioni di query XPath.  Il metodo <xref:System.Xml.XPath.XPathExpression.SetContext%2A> può accettare un contesto definito dall'utente derivato dall'oggetto <xref:System.Xml.Xsl.XsltContext>.  Le funzioni definite dall'utente vengono risolte dal contesto personalizzato.  
  
 Le funzioni di estensione e le variabili possono essere utili per evitare attacchi XML injection.  In questi scenari, l'input dell'utente viene assegnato a variabili personalizzate ed elaborato dalle funzioni di estensione, non come input non elaborato concatenato alle istruzioni di elaborazione.  Le funzioni di estensione e le variabili contengono l'input dell'utente in modo che agisca solo sui dati XML come previsto nella finestra di progettazione.  
  
 Per usare le estensioni è necessario implementare una classe <xref:System.Xml.Xsl.XsltContext> personalizzata insieme alle interfacce <xref:System.Xml.Xsl.IXsltContextFunction> e <xref:System.Xml.Xsl.IXsltContextVariable> che supportano le funzioni di estensione e le variabili.  Un oggetto <xref:System.Xml.XPath.XPathExpression> aggiunge l'input dell'utente con il relativo oggetto <xref:System.Xml.Xsl.XsltArgumentList> all'oggetto <xref:System.Xml.Xsl.XsltContext> personalizzato.  
  
 L'oggetto <xref:System.Xml.XPath.XPathExpression> rappresenta una query compilata usata dall'oggetto <xref:System.Xml.XPath.XPathNavigator> per individuare ed elaborare i nodi identificati dall'espressione.  
  
 Nell'esempio seguente viene illustrata l'implementazione di una classe del contesto personalizzata derivata dall'oggetto <xref:System.Xml.Xsl.XsltContext>.  I commenti nel codice descrivono i membri della classe e il relativo uso nelle funzioni personalizzate.  Le implementazioni delle funzioni e delle variabili e un'applicazione di esempio che usa tali implementazioni si attengono a questo segmento di codice.  
  
 [!code-csharp[XPathExtensionFunctions#2](../../../../samples/snippets/csharp/VS_Snippets_Data/xpathextensionfunctions/cs/xpathextensionfunctions.cs#2)]
 [!code-vb[XPathExtensionFunctions#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/xpathextensionfunctions/vb/xpathextensionfunctions.vb#2)]  
  
 Il codice seguente implementa l'oggetto <xref:System.Xml.Xsl.IXsltContextFunction>.  La classe che implementa l'oggetto <xref:System.Xml.Xsl.IXsltContextFunction> risolve ed esegue le funzioni definite dall'utente.  In questo esempio viene usata la funzione identificata dalla dichiarazione: `private int CountChar(string title, char charTocount)`.  
  
 I commenti nel codice descrivono i membri della classe.  
  
 [!code-csharp[XPathExtensionFunctions#3](../../../../samples/snippets/csharp/VS_Snippets_Data/xpathextensionfunctions/cs/xpathextensionfunctions.cs#3)]
 [!code-vb[XPathExtensionFunctions#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/xpathextensionfunctions/vb/xpathextensionfunctions.vb#3)]  
  
 Il codice seguente implementa l'oggetto <xref:System.Xml.Xsl.IXsltContextVariable>.  Questa classe risolve i riferimenti alle variabili definite dall'utente nelle espressioni di query XPath in fase di esecuzione.  Un'istanza di questa classe viene creata e restituita dal metodo <xref:System.Xml.Xsl.XsltContext.ResolveVariable%2A> sottoposto a override della classe <xref:System.Xml.Xsl.XsltContext> personalizzata.  
  
 I commenti nel codice descrivono i membri della classe.  
  
 [!code-csharp[XPathExtensionFunctions#4](../../../../samples/snippets/csharp/VS_Snippets_Data/xpathextensionfunctions/cs/xpathextensionfunctions.cs#4)]
 [!code-vb[XPathExtensionFunctions#4](../../../../samples/snippets/visualbasic/VS_Snippets_Data/xpathextensionfunctions/vb/xpathextensionfunctions.vb#4)]  
  
 Con le precedenti definizioni di classe incluse nell'ambito, nel codice seguente viene usata la funzione personalizzata per contare i caratteri negli elementi del documento `Tasks.xml`.  I commenti nel codice descrivono il codice che compila la funzione personalizzata e la esegue nel documento `Tasks.xml`.  
  
 [!code-csharp[XPathExtensionFunctions#1](../../../../samples/snippets/csharp/VS_Snippets_Data/xpathextensionfunctions/cs/xpathextensionfunctions.cs#1)]
 [!code-vb[XPathExtensionFunctions#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/xpathextensionfunctions/vb/xpathextensionfunctions.vb#1)]  
  
 In questo esempio vengono usati i seguenti dati XML.  
  
 [!code-xml[XPathExtensionFunctions#5](../../../../samples/snippets/xml/VS_Snippets_Data/xpathextensionfunctions/XML/tasks.xml#5)]