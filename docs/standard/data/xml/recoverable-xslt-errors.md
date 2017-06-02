---
title: "Errori XSLT risolvibili | Microsoft Docs"
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
ms.assetid: 484929b0-fefb-4629-87ee-ebdde70ff1f8
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Errori XSLT risolvibili
Nella raccomandazione W3C, XSL Transformations \(XSLT\) Version 1.0, sono incluse aree in cui il provider dell'implementazione può decidere come gestire una determinata situazione.  Queste aree si considerano come aree di comportamento discretionary.  Nella sezione 7.3 Creating Processing Instructions della raccomandazione XSLT 1.0, ad esempio, viene specificato che la creazione di nodi diversi da nodi di tipo text durante la creazione di un'istanza del contenuto di `xsl:processing-instruction` costituisce un errore.  Per alcuni problemi, la raccomandazione XSLT 1.0 fornisce una linea d'azione nel caso in cui il processore tenti di risolvere l'errore.  Per l'errore illustrato nella sezione 7.3 viene spiegato che il problema può essere risolto ignorando i nodi e il relativo contenuto.  
  
## Comportamenti discretionary  
 Nella tabella seguente viene elencato ogni comportamento discretionary consentito dalla raccomandazione XSLT 1.0 e il modo in cui tali comportamenti vengono gestiti dalla classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   "Ripristino" indica che la classe <xref:System.Xml.Xsl.XslCompiledTransform> eseguirà la correzione dell'errore.  È possibile usare l'evento <xref:System.Xml.Xsl.XsltArgumentList.XsltMessageEncountered?displayProperty=fullName> per segnalare tutti gli eventi dal processore XSLT.  
  
-   "Errore" indica che è stata generata un'eccezione per questa condizione.  
  
-   I riferimenti alle sezioni sono reperibili nei documenti [W3C XSL Transformations \(XSLT\) Version 1.0 Recommendation](http://go.microsoft.com/fwlink/?LinkId=49919) e [W3C XSL Transformations \(XSLT\) Version 1.0 Specification Errata](http://go.microsoft.com/fwlink/?LinkId=49917).  
  
|Condizione XSLT|Sezione|Comportamento di XslCompiledTransform|  
|---------------------|-------------|-------------------------------------------|  
|Nodo di tipo text corrispondente sia a `xsl:strip-space` sia a `xsl:preserve-space`.|3.4|Ripristino|  
|Nodo di origine corrispondente a più di una regola dei modelli.|5.5|Ripristino|  
|Un URI dello spazio dei nomi è dichiarato come alias per più URI dello spazio dei nomi, tutti con la stessa precedenza di importazione.|7.1.1|Ripristino|  
|L'attributo `name` in `xsl:attribute` e `xsl:element` generato da un valore dell'attributo non è un QName.|7.1.2, 7.1.3|Errore\*|  
|Due set di attributi con la stessa precedenza di importazione e lo stesso nome espanso hanno un attributo in comune e non sono presenti altri set di attributi contenenti l'attributo comune con lo stesso nome e con un'importanza superiore.|7.1.4|Ripristino|  
|Aggiunta di un attributo a un elemento dopo che ad esso sono stati aggiunti elementi figlio.|7.1.3|Errore\*|  
|Creazione di un attributo denominato "xmlns".|7.1.3|Errore\*|  
|Aggiunta di un attributo a un nodo diverso da un nodo di elemento.|7.1.3|Errore\*|  
|Creazione di nodi diversi da nodi di tipo text durante la creazione di un'istanza del contenuto dell'attributo `xsl:attribute`.|7.1.3|Errore\*|  
|L'attributo `name` di un'istruzione `xsl:processing-instruction` non restituisce sia un NCName che una destinazione dell'istruzione di elaborazione.|7.3|Errore\*|  
|La creazione di un'istanza del contenuto `xsl:processing-instruction` crea nodi diversi da quelli di testo.|7.3|Errore\*|  
|Il risultato della creazione di un'istanza del contenuto di `xsl:processing-instruction` contiene la stringa "?\>"|7.3|Ripristino|  
|Il risultato della creazione di un'istanza del contenuto di `xsl:processing-instruction` contiene la stringa "\-\-" o termina con "\-".|7.4|Ripristino|  
|Il risultato della creazione di un'istanza del contenuto di `xsl:comment` crea nodi diversi da quelli di tipo text.|7.4|Errore\*|  
|Il modello all'interno di un elemento di associazione della variabile restituisce un nodo Attribute o un nodo dello spazio dei nomi.|11.2|Errore\*|  
|Si verifica un errore durante il recupero della risorsa dall'URI passato nella funzione del documento.|12.1|Errore|  
|Il riferimento all'URI nella funzione del documento contiene un identificatore di frammento e si verifica un errore nell'elaborazione di tale identificatore.|12.1|Ripristino\*|  
|Esistono più attributi con lo stesso nome ma con valori diversi che non sono elementi sezioni cdata denominati in `xsl:output` e tali attributi hanno la stessa precedenza di importazione.|16|Ripristino|  
|Il processore non supporta la codifica nell'attributo di codifica `xsl:output`.|16.1|Ripristino|  
|Disabilitazione dell'escape dell'output per un nodo di tipo text usato per scopi diversi da quelli di un nodo di tipo text nell'albero dei risultati.|16.4|Ripristino\*|  
|Conversione di un frammento di albero risultato in un numero o stringa, se il frammento contiene un nodo di tipo text con l'escape dell'output abilitato.|16.4|Ripristino\*|  
|L'escape dell'output è disattivato per un carattere che non può essere rappresentato nella codifica usata dal processore XSLT per l'output.|16.4|Ripristino\*|  
|Aggiunta di un nodo dello spazio dei nomi a un elemento dopo che a tale elemento sono stati aggiunti elementi figlio o attributi.|errata 25|Errore\*|  
|L'attributo `value` di un `xsl:number` è un valore NaN, infinito o minore di 0,5.|errata 24|Ripristino|  
|Il secondo set di nodi dell'argomento della funzione del documento è vuoto e il riferimento all'URI è relativo.|errata 14|Ripristino|  
  
 <sup>*</sup> Questo comportamento è diverso rispetto a quello della classe <xref:System.Xml.Xsl.XslTransform>.  Per altre informazioni, vedere [Implementazione di comportamenti discretionary nella classe XslTransform](../../../../docs/standard/data/xml/implementation-of-discretionary-behaviors-in-the-xsltransform-class.md).  
  
## Vedere anche  
 [Trasformazioni XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)