---
title: "Frammento di alberi risultato nelle trasformazioni | Microsoft Docs"
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
ms.assetid: df363480-ba02-4233-9ddf-8434e421c4f1
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Frammento di alberi risultato nelle trasformazioni
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 I frammenti di nodi, detti anche frammenti di albero risultato, sono semplicemente un particolare tipo di set di nodi.  Sui frammenti di nodi è possibile eseguire le stesse funzioni che sono eseguibili sui set di nodi.  È inoltre possibile usare la funzione `node-set()` per convertire un frammento di albero risultato in un set di nodi, quindi usarlo in qualsiasi posizione adatta.  
  
 Un frammento di albero risultato viene creato usando in modo specifico un elemento `<xsl:variable>` o `<xsl:param>` in un foglio di stile.  La sintassi degli elementi `variable` e `parameter` è la seguente:  
  
```  
<xsl:param name=Qname select= XPath Expression >  
    template body  
</xsl:param>  
  
<xsl:variable name=Qname select=XPath Expression >  
    template body  
</xsl:variable>  
```  
  
 Il valore del nome completo \(`Qname`\) dell'elemento `parameter` può essere assegnato in vari modi.  È possibile assegnare al parametro un valore predefinito tramite il contenuto restituito dall'espressione XPath nell'attributo `select` oppure usando il contenuto del corpo del modello.  
  
 Anche il valore dell'elemento `variable` può essere assegnato in diversi modi.  È possibile assegnarlo tramite il contenuto restituito dall'espressione XPath nell'attributo `select` oppure usando il contenuto del corpo del modello.  
  
 Da entrambi gli elementi `parameter` e `variable`, se viene assegnato un valore dall'espressione XPath, viene restituito uno dei quattro tipi XPath principali: Boolean, string, number o node set.  Se il valore viene assegnato usando un corpo del modello non vuoto, verrà restituito un tipo di dati non XPath, ovvero un frammento di albero risultato.  
  
 Una query XPath restituisce un tipo di dati che non appartiene a uno dei quattro tipi di oggetti XPath unicamente nel caso in cui una variabile è associata a un frammento di albero risultato, anziché a uno dei quattro tipi di dati XPath di base.  I frammenti di albero risultato e il relativo comportamento sono descritti nella specifica W3C, all'indirizzo http:\/\/www.w3.org\/XSLT, dalla sezione 11.1 Result Tree Fragments alla sezione 11.6 Passing Parameters to Templates \(informazioni in lingua inglese\).  Inoltre, nella sezione 1, Introduction, viene illustrato come i modelli possono contenere elementi dello spazio dei nomi XSLT che restituiscono o creano frammenti di albero risultato.  
  
 Un frammento di albero risultato si comporta, teoricamente, come un set di nodi con un unico nodo radice,  mentre gli altri nodi restituiti sono nodi figlio.  Per visualizzare i nodi figlio a livello di codice, copiare il frammento di albero risultato nell'albero risultato stessa usando l'elemento `<xsl:copy-of>`.  Questa operazione consente di copiare in sequenza tutti i nodi figlio nell'albero risultato.  Il frammento di albero risultato non farà parte dell'albero risultato o dell'output della trasformazione finché non viene usato un comando `copy` o `copy-of`.  
  
 Per eseguire un'iterazione sui nodi restituiti in un frammento di albero risultato, usare <xref:System.Xml.XPath.XPathNavigator>.  Nel codice di esempio seguente viene illustrata la creazione di un frammento di albero risultato in un foglio di stile, chiamando la funzione con un parametro `fragment` contenente dati XML.  
  
```  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
    <xsl:var name="fragment">  
        <node1>  
            <node2/>  
        </node1>  
    <xsl:var>  
  
  <msxsl:script language="C#" implements-prefix="user">  
    function NodeFragment(XPathNavigator nav)  
    {  
      if (nav.HasSelection == false)  
        XPathNavigator.MoveToNext();  
      return;  
    }  
  </msxsl:script>  
  
    <xsl:template match="/">  
            <xsl:value-of select="user:NodeFragment(msxml:node-set($fragment))"/>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
 Di seguito è riportato un altro esempio in cui viene mostrata una variabile, in RTF \(Rich Text Format\) e, di conseguenza, un tipo di frammento di albero risultato nodo non convertito in un set di nodi.  Il frammento viene passato a una funzione script e per esplorare i nodi viene usato il tipo <xref:System.Xml.XPath.XPathNavigator>.  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
        xmlns:user="urn:books"  
        exclude-result-prefixes="msxsl">  
  
<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>  
  
<xsl:variable name="node-fragment">  
    <book>Book1</book>  
    <book>Book2</book>  
    <book>Book3</book>  
    <book>Book4</book>  
</xsl:variable>  
  
<msxsl:script implements-prefix="user" language="c#">  
  
<![CDATA[  
    string func(XPathNavigator nav)  
    {  
        bool b = nav.MoveToFirstChild();  
        if (b)  
            return nav.Value;  
        else  
            return "Does not exist";  
    }  
  
]]>  
  
</msxsl:script>  
  
<xsl:template match="/">  
    <first_book>  
        <xsl:value-of select="user:func($node-fragment)"/>  
    </first_book>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
 Il risultato della trasformazione dei dati XML ottenuto usando questo foglio di stile è illustrato nell'output seguente.  
  
## Output  
  
```  
<first_book xmlns:user="urn:books">Book1</first_book>  
```  
  
 Come descritto in precedenza, la funzione `node-set` consente di convertire un frammento di albero risultato in un set di nodi.  Il nodo risultante contiene sempre un nodo singolo, costituito dal nodo radice dell'albero.  Se un frammento di albero risultato viene convertito in un set di nodi, potrà essere usato come un normale set di nodi, ad esempio in un'istruzione for\-each oppure nel valore di un attributo `select`.  Nelle righe di codice seguenti viene mostrato un frammento convertito in un set di nodi e usato come tale:  
  
 `<xsl:for-each select="msxsl:node-set($node-fragment)">`  
  
 `<xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>`  
  
 Per esplorare un frammento convertito in un set di nodi non viene più usato <xref:System.Xml.XPath.XPathNavigator>, bensì  <xref:System.Xml.XPath.XPathNodeIterator>.  
  
 Nell'esempio seguente `$var` è una variabile che rappresenta l'albero dei nodi del foglio di stile.  L'istruzione for\-each combinata con la funzione `node-set` consente all'utente di eseguire un'iterazione su questo albero come set di nodi.  
  
```  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
    <xsl:variable name="states">  
        <node1>AL</node1>  
        <node1>CA</node1>  
        <node1>CO</node1>  
        <node1>WA</node1>  
    </xsl:variable>  
  
    <xsl:template match="/">  
            <xsl:for-each select="msxsl:node-set($states)"/>   
    </xsl:template>  
</xsl:stylesheet>  
```  
  
 Di seguito è riportato un altro esempio di variabile in formato RTF, quindi di tipo frammento di albero risultato, convertita in set di nodi prima di essere passata a una funzione script come "XPathNodeIterator".  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
        xmlns:user="urn:books"  
        exclude-result-prefixes="msxsl">  
  
<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>  
  
<xsl:variable name="node-fragment">  
    <book>Book1</book>  
    <book>Book2</book>  
    <book>Book3</book>  
    <book>Book4</book>  
</xsl:variable>  
  
<msxsl:script implements-prefix="user" language="c#">  
  
<![CDATA[  
    string func(XPathNodeIterator it)  
    {  
        it.MoveNext();   
        return it.Current.Value;   
        //it.Current returns XPathNavigator positioned on the current node  
    }  
  
]]>  
  
</msxsl:script>  
<xsl:template match="/">  
    <books>  
        <xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>  
    </books>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
 Il risultato della trasformazione di dati XML con il presente foglio di stile è il seguente:  
  
```  
<books xmlns:user="urn:books">Book1Book2Book3Book4</books>  
```  
  
## Vedere anche  
 <xref:System.Xml.XPath.XPathNodeIterator>   
 <xref:System.Xml.XPath.XPathNodeIterator>   
 [Trasformazioni XSLT con la classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)