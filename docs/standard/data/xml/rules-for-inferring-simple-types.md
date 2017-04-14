---
title: "Regole per l&#39;inferenza di tipi semplici | Microsoft Docs"
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
ms.assetid: 394624d6-4da0-430a-8a88-46efe40f14de
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Regole per l&#39;inferenza di tipi semplici
Describes how the <xref:System.Xml.Schema.XmlSchemaInference> class infers the data type for attributes and elements.  
  
 La classe <xref:System.Xml.Schema.XmlSchemaInference> inferisce il tipo di dati per attributi ed elementi come tipi semplici.  Contenuto della sezione vengono descritti i tipi che possono essere inferiti, la risoluzione delle differenze di più valori diversi in un unico tipo e la gestione degli attributi `xsi` di definizione dello schema.  
  
## Tipi inferiti  
 La classe <xref:System.Xml.Schema.XmlSchemaInference> inferisce i valori di elementi e attributi come tipi semplici e include un attributo Type nello schema risultante.  Tutti i tipi inferiti sono tipi semplici.  I tipi o i facet di base non sono inclusi nello schema risultante.  
  
 I valori vengono esaminati singolarmente quando vengono rilevati nel documento XML.  Il tipo viene inferito per il valore riscontrato nel momento in cui viene esaminato.  Se è stato inferito un tipo per un attributo o un elemento e viene rilevato un valore per l'attributo o elemento che non corrisponde al tipo inferito, la classe <xref:System.Xml.Schema.XmlSchemaInference> promuove il tipo per un set di regole.  Tali regole vengono illustrate nella sezione Promozione dei tipi, più avanti in questo argomento.  
  
 Nella tabella seguente sono elencati i tipi che possono essere inferiti per lo schema risultante.  
  
|Tipo semplice|Descrizione|  
|-------------------|-----------------|  
|boolean|True, false, 0, 1.|  
|byte|Numeri interi nell'intervallo compreso tra \-128 e 127.|  
|unsignedByte|Numeri interi nell'intervallo compreso tra 0 e 255.|  
|short|Numeri interi nell'intervallo compreso tra \-32768 e 32767.|  
|unsignedShort|Numeri interi nell'intervallo compreso tra 0 e 65535.|  
|int|Numeri interi nell'intervallo compreso tra \-2147483648 e 2147483647.|  
|unsignedInt|Numeri interi nell'intervallo compreso tra 0 e 4294967295.|  
|long|Numeri interi nell'intervallo compreso tra \-9223372036854775808 e 9223372036854775807.|  
|unsignedLong|Numeri interi nell'intervallo compreso tra 0 e 18446744073709551615.|  
|integer|Un numero finito di cifre che può essere preceduto dal prefisso "\-".|  
|decimal|Valori numerici che contengono da 0 a 28 cifre di precisione.|  
|float|Decimali eventualmente seguiti da "E" o "e", quindi da un numero intero che rappresenta l'esponente.  I valori decimali possono essere compresi tra \-16777216 e 16777216  I valori dell'esponente tra –149 e 104.<br /><br /> Il tipo float consente ai valori speciali di rappresentare i valori infinito e quelli non numerici.  I valori speciali per float sono i seguenti: 0, \-0, INF \- INF, NaN.|  
|double|Analogo a float, ad eccezione del fatto che i valori decimali possono essere compresi tra \-9007199254740992 e 9007199254740992 e i valori dell'esponente tra –1075 e 970.<br /><br /> Il tipo double consente ai valori speciali di rappresentare i valori infinito e quelli non numerici.  I valori speciali per float sono i seguenti: 0, \-0, INF \- INF, NaN.|  
|duration|Formato della durata W3C.|  
|dateTime|Formato dateTime W3C.|  
|ora|Formato di ora W3C.|  
|date|I valori relativi agli anni sono compresi tra 0001 e 9999.|  
|gYearMonth|Formato dell'anno e del mese gregoriano W3C.|  
|string|Uno o più caratteri Unicode.|  
  
## Promozione tipo  
 La classe <xref:System.Xml.Schema.XmlSchemaInference> esamina i valori di attributi ed elementi singolarmente.  Quando i valori vengono rilevati, viene inferito il tipo più restrittivo e senza segno.  Se è stato inferito un tipo per un attributo o elemento ed è stato rilevato un nuovo valore che non corrisponde al tipo inferito, quest'ultimo viene promosso a un nuovo tipo applicabile sia al tipo inferito che al nuovo valore.  Durante la promozione del tipo inferito, la classe <xref:System.Xml.Schema.XmlSchemaInference> valuta i valori precedenti.  
  
 Ad esempio, si considerino i seguenti frammenti XML provenienti da due documenti XML:  
  
 `<MyElement1 attr1="12" />`  
  
 `<MyElement1 attr1="52344" />`  
  
 Quando viene rilevato il primo valore `attr1`, il tipo di `attr1` viene inferito come `unsignedByte` in base al valore `12`.  Quando viene rilevato il secondo valore `attr1`, il tipo viene promosso a `unsignedShort` in base al tipo inferito di `unsignedByte` e al valore corrente `52344`.  
  
 Si consideri ora il seguente codice XML proveniente da due documenti XML:  
  
 `<MyElement2 attr2="0" />`  
  
 `<MyElement2 attr2="true" />`  
  
 Quando viene rilevato il primo valore `attr2`, il tipo di `attr2` viene inferito come `unsignedByte` in base al valore `0`.  Quando viene rilevato il secondo valore `attr2`, il tipo viene promosso a `string` in base al tipo inferito di `unsignedByte` e al valore corrente `true`, poiché la classe <xref:System.Xml.Schema.XmlSchemaInference> valuta i valori precedenti durante la promozione del tipo dedotto.  Se tuttavia entrambe le istanze di `attr2` fossero state rilevate all'interno dello stesso documento XML e non in due documenti XML diversi come descritto in precedenza, `attr2` sarebbe stato inferito come `boolean`.  
  
### Attributi ignorati dallo spazio dei nomi dell'istanza di XML Schema all'indirizzo http:\/\/www.w3.org\/2001\/XMLSchema\-instance \(informazioni in lingua inglese\)  
 Di seguito sono riportati gli attributi di definizione dello schema che vengono ignorati durante l'inferenza dello schema.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`xsi:type`|Se viene rilevato un elemento con `xsi:type` specificato, l'attributo `xsi:type` viene ignorato.|  
|`xsi:nil`|Se viene rilevato un elemento con un attributo `xsi:nil`, la dichiarazione dell'elemento nello schema inferito presenta il valore `nillable="true"`.  Un elemento con un attributo `xsi:nil` impostato su `true` non può contenere elementi figlio.|  
|`xsi:schemaLocation`|Se rilevato, l'attributo `xsi:schemaLocation` viene ignorato.|  
|`xsi:noNamespaceSchemaLocation`|Se rilevato, l'attributo `xsi:noNamespaceSchemaLocation` viene ignorato.|  
  
## Vedere anche  
 [SOM \(Schema Object Model\) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)   
 [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)   
 [Regole per l'inferenza dello schema per tipi di nodo e struttura](../../../../docs/standard/data/xml/rules-for-inferring-schema-node-types-and-structure.md)