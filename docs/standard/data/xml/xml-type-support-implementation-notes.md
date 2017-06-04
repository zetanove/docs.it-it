---
title: "Note sull&#39;implementazione del supporto per il tipo XML | Microsoft Docs"
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
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Note sull&#39;implementazione del supporto per il tipo XML
In questo argomento vengono descritti alcuni dettagli sull'implementazione di cui è consigliabile essere a conoscenza.  
  
## Mapping degli elenchi  
 I tipi <xref:System.Collections.IList>, <xref:System.Collections.ICollection>, <xref:System.Collections.IEnumerable>, **Type\[\]** e <xref:System.String> vengono usati per rappresentare i tipi di elenco XSD \(XML Schema definition language\).  
  
## Mapping delle unioni  
 I tipi di unione vengono rappresentati usando il tipo <xref:System.Xml.Schema.XmlAtomicValue> o <xref:System.String>.  Pertanto, il tipo di origine o il tipo di destinazione devono sempre essere <xref:System.String> o <xref:System.Xml.Schema.XmlAtomicValue>.  
  
 Se l'oggetto <xref:System.Xml.Schema.XmlSchemaDatatype> rappresenta un tipo di elenco, tale oggetto converte il valore della stringa di input in un elenco di uno o più oggetti.  Se l'oggetto <xref:System.Xml.Schema.XmlSchemaDatatype> rappresenta un tipo di unione, viene eseguito un tentativo di analisi del valore di input come tipo membro dell'unione.  Se il tentativo di analisi non viene eseguito correttamente, viene tentata la conversione con il successivo membro dell'unione e così via fino a quando la conversione non viene eseguita correttamente o non sono disponibili altri tipi di membro con cui provare. In questo caso verrà generata un'eccezione.  
  
## Differenze tra i tipi di dati CLR e XML  
 Di seguito vengono descritte alcune corrispondenze errate che si possono verificare tra i tipi di dati CLR e i tipi di dati XML e la loro eventuale gestione.  
  
> [!NOTE]
>  Il prefisso `xs` è associato all'indirizzo http:\/\/www.w3.org\/2001\/XMLSchema e all'URI dello spazio dei nomi.  
  
### System.TimeSpan e xs:duration  
 Il tipo `xs:duration` è parzialmente ordinato, poiché alcuni valori di durata sono diversi ma equivalenti.  Ciò significa che per il tipo `xs:duration` il valore di 1 mese \(P1M\) è minore di 32 giorni \(P32D\), maggiore di 27 giorni \(P27D\) ed equivalente a 28, 29 o 30 giorni.  
  
 La classe <xref:System.TimeSpan> non supporta questo ordinamento parziale.  Invece, stabilisce un numero specifico di giorni per 1 anno e 1 mese: rispettivamente 365 e 30 giorni.  
  
 Per altre informazioni sul tipo `xs:duration`, vedere la raccomandazione W3C XML Schema Part 2: Datatypes all'indirizzo http:\/\/www.w3.org\/TR\/xmlschema\-2\/ \(informazioni in lingua inglese\).  
  
### xs:time, tipi di date gregoriane e System.DateTime  
 Quando un valore `xs:time` è associato a un oggetto <xref:System.DateTime>, il campo <xref:System.DateTime.MinValue> viene usato per inizializzare le proprietà relative alla data dell'oggetto <xref:System.DateTime> \(ad esempio, <xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A> e <xref:System.DateTime.Day%2A>\) impostandole sul valore <xref:System.DateTime> più basso possibile.  
  
 Allo stesso modo, anche istanze di `xs:gMonth`, `xs:gDay`, `xs:gYear`, `xs:gYearMonth` e `xs:gMonthDay` vengono associate a un oggetto <xref:System.DateTime>.  Le proprietà inutilizzate nell'oggetto <xref:System.DateTime> vengono inizializzate impostandole su quelle da <xref:System.DateTime.MinValue>.  
  
> [!NOTE]
>  Non è possibile usare il valore <xref:System.DateTime.Year%2A?displayProperty=fullName> quando il contenuto è tipizzato come `xs:gMonthDay`.  In questo caso il valore <xref:System.DateTime.Year%2A?displayProperty=fullName> è sempre impostato su 1904.  
  
### xs:anyURI e System.Uri  
 Quando un'istanza di `xs:anyURI` che rappresenta un URI relativo viene associata a un tipo <xref:System.Uri>, l'oggetto <xref:System.Uri> non dispone di un URI di base.  
  
## Vedere anche  
 [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)