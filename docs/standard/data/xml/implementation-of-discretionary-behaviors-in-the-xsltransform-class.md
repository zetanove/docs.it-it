---
title: "Implementazione di comportamenti discretionary nella classe XslTransform | Microsoft Docs"
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
ms.assetid: d2758ea1-03f6-47bd-88d2-0fb7ccdb2fab
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Implementazione di comportamenti discretionary nella classe XslTransform
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]. È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>. Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 Sono definiti discretionary i comportamenti, elencati nella raccomandazione W3C \(World Wide Web Consortium\) \(www.w3.org\/TR\/xslt\) XSL Transformations \(XSLT\) Version 1.0 \(informazioni in lingua inglese\), nei quali l'implementazione sceglie una delle numerose opzioni disponibili per gestire una determinata situazione. Nella sezione 7.3 Creating Processing Instructions della raccomandazione W3C, ad esempio, viene specificato che la creazione di nodi diversi da nodi di tipo text durante la creazione di un'istanza del contenuto di `xsl:processing-instruction` costituisce un errore. Per alcuni problemi, il W3C fornisce una linea d'azione per il caso in cui il processore tenta di risolvere l'errore. Per l'errore illustrato nella sezione 7.3 viene spiegato che il problema può essere risolto ignorando i nodi e il relativo contenuto.  
  
 Pertanto, nella tabella seguente sono elencati, per ciascuno dei comportamenti discretionary consentiti dal W3C, i comportamenti discretionary relativi all'implementazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] della classe <xref:System.Xml.Xsl.XslTransform> e la sezione della raccomandazione W3C XSL Transformations \(XSLT\) 1.0 \(informazioni in lingua inglese\) in cui viene trattato tale problema.  
  
|Problema|Comportamento|Sezione|  
|--------------|-------------------|-------------|  
|Nodo di tipo text corrispondente sia a `xsl:strip-space` sia a `xsl:preserve-space`.|Ripristino|3.4|  
|Nodo di origine corrispondente a più di una regola dei modelli.|Ripristino|5.5|  
|Un URI dello spazio dei nomi è dichiarato come alias per più URI dello spazio dei nomi, tutti con la stessa precedenza di importazione.|Ripristino|7.1.1|  
|L'attributo del nome in `xsl:attribute` e `xsl:element` generato da un modello del valore dell'attributo non è un nome completo valido \(QName\).|Generazione di eccezione|7.1.12 e 7.1.3|  
|Aggiunta di un attributo a un elemento dopo che al nodo dell'elemento sono già stati aggiunti nodi figlio.|Ripristino|7.1.3|  
|Aggiunta di un attributo in una posizione diversa da un nodo Element.|Ripristino|7.1.3|  
|L'istanza del contenuto dell'elemento `xsl:attribute` creata non è un nodo di tipo text.|Ripristino|7.1.3|  
|Due set di attributi hanno la stessa precedenza di importazione e lo stesso nome espanso. Entrambi hanno lo stesso attributo e non sono presenti altri set di attributi contenenti l'attributo comune, con lo stesso nome e con un'importanza superiore.|Ripristino|7.1.4|  
|`xsl:processing-instruction` non restituisce un nome senza due punti \(NCName\), né una destinazione dell'istruzione di elaborazione.|Ripristino|7.3|  
|La creazione di un'istanza del contenuto `xsl:processing-instruction` crea nodi diversi da quelli di testo.|Ripristino|7.3|  
|I risultati della creazione di un'istanza del contenuto di `xsl:processing-instruction` contengono la stringa "`?>`".|Ripristino|7.3|  
|I risultati della creazione di un'istanza del contenuto di `xsl:comment`  contengono la stringa "\-\-" o terminano con "\-".|Ripristino|7.4|  
|I risultati della creazione di un'istanza del contenuto di `xsl:comment` creano nodi diversi da quelli di testo.|Ripristino|7.4|  
|Il modello all'interno di un elemento di associazione della variabile restituisce un nodo Attribute o un nodo dello spazio dei nomi.|Ripristino|11.2|  
|Si verifica un errore durante il recupero della risorsa dall'URI passato nella funzione del documento.|Generazione di eccezione|12.1|  
|Il riferimento all'URI nella funzione del documento contiene un identificatore di frammento e si verifica un errore nell'elaborazione di tale identificatore.|Generazione di eccezione|12.1|  
|Esistono più attributi con lo stesso nome che non sono denominati `cdata-section-elements` in `xls:output` e tali attributi hanno la stessa precedenza di importazione.|Ripristino|16|  
|Il processore non supporta il valore di codifica dei caratteri fornito nell'attributo `encoding` dell'elemento `xsl:output`.|Ripristino|16.1|  
|L'attributo `disable-output-escaping` viene usato per un nodo di tipo text che a sua volta viene usato per creare un elemento diverso da un nodo di tipo text nell'albero risultato.|L'attributo `disable-output-escaping` viene ignorato|16.4|  
|Conversione di un frammento di albero risultato in un numero o stringa, se il frammento contiene un nodo di tipo text con l'escape dell'output abilitato.|Ignorato|16.4|  
|L'escape dell'output è disabilitato per i caratteri che non possono essere rappresentati nella codifica usata dal processore XSLT per l'output.|Ignorato|16.4|  
|Aggiunta di un nodo dello spazio dei nomi a un elemento dopo che a tale elemento sono stati aggiunti elementi figlio o attributi.|Ripristino|Errata e25|  
|`xsl:number` è un valore NaN, infinito o minore di 0,5.|Ripristino|Errata e24|  
|Il secondo set di nodi dell'argomento della funzione del documento è vuoto e il riferimento all'URI è relativo.|Ripristino|Errata e14|  
  
 Le sezioni Errata si trovano in XSL Transformations \(XSLT\) Version 1.0 Specification Errata, all'indirizzo http:\/\/www.w3.org\/1999\/11\/REC\-xslt\-19991116\-errata \(informazioni in lingua inglese\).  
  
## Comportamenti dell'implementazione definiti dall'utente  
 Alcuni comportamenti sono caratteristici solo dell'implementazione della classe <xref:System.Xml.Xsl.XslTransform>. Contenuto della sezione vengono descritte l'implementazione di `xsl:sort` specifica del provider e le funzionalità supportate dalla classe <xref:System.Xml.Xsl.XslTransform>.  
  
## xsl:sort  
 Nella raccomandazione W3C XSLT 1.0 \(informazioni in lingua inglese\) sono contenute alcune osservazioni relative a come eseguire un ordinamento usando le trasformazioni. Ad esempio:  
  
-   Due processori XSLT possono essere conformi, ma potrebbero eseguire l'ordinamento ordinare in maniera differente.  
  
-   Non tutti i processori XSLT supportano le stesse lingue.  
  
-   In relazione alle lingue, è possibile che processori diversi eseguano l'ordinamento in modo diverso per una particolare lingua non specificata da `xsl:sort.`.  
  
 Nella tabella seguente viene descritta la modalità di ordinamento per ciascun tipo di dati nell'implementazione .NET Framework di una trasformazione tramite il tipo <xref:System.Xml.Xsl.XslTransform>.  
  
|Tipo di dati|Modalità di ordinamento|  
|------------------|-----------------------------|  
|Text|I dati vengono ordinati usando il metodo String.Compare di Common Language Runtime \(CLR\) e le impostazioni locali specifiche della lingua. Quando il tipo di dati risulta uguale a "text", l'ordinamento nella classe <xref:System.Xml.Xsl.XslTransform> si svolge in modo identico ai comportamenti nel confronto delle stringhe del CLR.|  
|Numero|I valori numerici vengono considerati come numeri XPath e vengono ordinati in base alle informazioni contenute nella sezione 3.5 della raccomandazione W3C XML Path Language \(XPath\) Version 1.0, disponibile all'indirizzo www.w3.org\/TR\/xpath.html\#numbers \(informazioni in lingua inglese\).|  
  
## Funzionalità opzionali supportate  
 Nella tabella seguente sono riportate le funzionalità la cui implementazione è facoltativa per un processore XSLT e che vengono implementate nella classe <xref:System.Xml.Xsl.XslTransform>.  
  
|Funzionalità|Posizione del riferimento|Note|  
|------------------|-------------------------------|----------|  
|Attributo `disable-output-escaping` sui tag `<xsl:text...>` e `<xsl:value-of...>`.|Raccomandazione W3C XSLT 1.0,<br /><br /> Sezione 16.4|L'attributo `disable-output-escaping` viene ignorato quando gli elementi `xsl:text` o `xsl:value-of` sono usati in un elemento `xsl:comment`, `xsl:processing-instruction`, o `xsl:attribute`.<br /><br /> I frammenti di albero risultato, che contengono testo e l'output di testo di cui è stato eseguito l'escape, non sono supportati.<br /><br /> L'attributo disable\-output\-escaping viene ignorato durante l'esecuzione di una trasformazione in un oggetto <xref:System.Xml.XmlReader> o <xref:System.Xml.XmlWriter>.|  
  
## Vedere anche  
 <xref:System.Xml.Xsl.XslTransform>   
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)   
 [Trasformazioni XSLT con la classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [XPathNavigator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)   
 [XPathNodeIterator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)   
 [Input di XPathDocument in XslTransform](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)   
 [Input di XmlDataDocument in XslTransform](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)   
 [Input di XmlDocument in XslTransform](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)