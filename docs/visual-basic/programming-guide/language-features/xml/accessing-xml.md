---
title: "Accessing XML in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "LINQ to XML [Visual Basic], accessing XML"
  - "Visual Basic code, XML"
  - "accessing XML [Visual Basic], axis properties"
  - "XML [Visual Basic], axis properties"
  - "XML [Visual Basic], accessing"
ms.assetid: c47f88b2-3cbc-4bb1-b4b9-be60f71ffc6a
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Accessing XML in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce le proprietà axis XML per l'accesso e la navigazione di strutture [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  Queste proprietà utilizzano una sintassi speciale per consentire l'accesso a elementi e attributi specificando i nomi XML.  
  
 Nella tabella seguente vengono elencate le funzionalità del linguaggio che consentono di accedere a elementi e attributi XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### Proprietà Axis XML  
  
|Descrizione della proprietà|Esempio|Descrizione|  
|---------------------------------|-------------|-----------------|  
|*axis elemento figlio*|`contact.<phone>`|Ottiene tutti gli elementi `phone` che sono elementi figlio dell'elemento `contact`.|  
|*axis attributo*|`phone.@type`|Ottiene tutti gli attributi `type` dell'elemento `phone`.|  
|*axis discendenti*|`contacts...<name>`|Ottiene tutti gli elementi `name` dell'elemento `contacts`, indipendentemente dal punto della gerarchia nel quale si trovano.|  
|*indicizzatore di estensione*|`contacts...<name>(0)`|Ottiene il primo elemento `name` dalla sequenza.|  
|*valore*|`contacts...<name>.Value`|Ottiene la rappresentazione di stringa del primo oggetto nella sequenza, o `Nothing` se la sequenza è vuota.|  
  
## In questa sezione  
 [How to: Access XML Descendant Elements](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md)  
 Viene illustrato come utilizzare una proprietà descendant axis per accedere a tutti gli elementi XML che hanno un nome specificato e che sono contenuti in un elemento XML specificato.  
  
 [How to: Access XML Child Elements](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-child-elements.md)  
 Viene illustrato come utilizzare una proprietà child axis per accedere a tutti gli elementi figlio XML che hanno un nome specificato in un elemento XML.  
  
 [How to: Access XML Attributes](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-attributes.md)  
 Viene illustrato come utilizzare una proprietà axis attribute per accedere a tutti gli attributi XML che hanno un nome specificato in un elemento XML.  
  
 [How to: Declare and Use XML Namespace Prefixes](../../../../visual-basic/programming-guide/language-features/xml/how-to-declare-and-use-xml-namespace-prefixes.md)  
 Viene illustrato come dichiarare un prefisso dello spazio dei nomi XML e usarlo per creare e accedere a elementi XML.  
  
## Sezioni correlate  
 [XML Axis Properties](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)  
 Vengono forniti i collegamenti alle sezioni in cui vengono descritte le varie proprietà di accesso a XML.  
  
 [Overview of LINQ to XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)  
 Viene fornita un'introduzione all'utilizzo di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] in Visual Basic.  
  
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 Viene fornita un'introduzione all'utilizzo dei valori letterali XML in Visual Basic.  
  
 [Manipulating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)  
 Vengono forniti i collegamenti alle sezioni relative a come caricare e modificare l'XML in Visual Basic.  
  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)  
 Fornisce collegamenti alle sezioni in cui viene descritto come utilizzare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] in Visual Basic.