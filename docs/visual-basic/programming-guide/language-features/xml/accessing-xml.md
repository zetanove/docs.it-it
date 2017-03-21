---
title: Accesso a XML in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- LINQ to XML [Visual Basic], accessing XML
- Visual Basic code, XML
- accessing XML [Visual Basic], axis properties
- XML [Visual Basic], axis properties
- XML [Visual Basic], accessing
ms.assetid: c47f88b2-3cbc-4bb1-b4b9-be60f71ffc6a
caps.latest.revision: 18
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 215f057f0b4d884369aad53cbbdbb98f240b56c4
ms.lasthandoff: 03/13/2017

---
# <a name="accessing-xml-in-visual-basic"></a>Accesso a XML in Visual Basic
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce proprietà axis XML per l'accesso e la navigazione [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] strutture. Queste proprietà utilizzano una sintassi speciale per consentire di accedere a elementi e attributi specificando i nomi XML.  
  
 Nella tabella seguente sono elencate le funzionalità del linguaggio che consentono di accedere agli elementi XML e attributi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### <a name="xml-axis-properties"></a>Proprietà Axis XML  
  
|Descrizione della proprietà|Esempio|Descrizione|  
|--------------------------|-------------|-----------------|  
|*asse child*|`contact.<phone>`|Ottiene tutti `phone` gli elementi che sono elementi figlio del `contact` elemento.|  
|*asse attribute*|`phone.@type`|Ottiene tutti `type` gli attributi del `phone` elemento.|  
|*asse descendant*|`contacts...<name>`|Ottiene tutti `name` elementi di `contacts` elemento, indipendentemente dal livello di profondità della gerarchia che si verificano.|  
|*indicizzatore di estensione*|`contacts...<name>(0)`|Ottiene il primo `name` elemento dalla sequenza.|  
|*value*|`contacts...<name>.Value`|Ottiene la rappresentazione di stringa del primo oggetto nella sequenza, o `Nothing` se la sequenza è vuota.|  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Procedura: Accedere agli elementi discendenti XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md)  
 Di seguito viene illustrato come utilizzare una proprietà axis descendant per accedere a tutti gli elementi XML che hanno un nome specificato e che sono contenuti in un elemento XML specificato.  
  
 [Procedura: Accedere agli elementi figlio XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-child-elements.md)  
 Viene illustrato come utilizzare un elemento figlio proprietà axis per accedere a tutti gli elementi figlio XML che hanno un nome specificato in un elemento XML.  
  
 [Procedura: Accedere agli attributi XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-attributes.md)  
 Di seguito viene illustrato come utilizzare una proprietà axis dell'attributo per accedere a tutti gli attributi XML che hanno un nome specificato in un elemento XML.  
  
 [Procedura: Dichiarare e usare prefissi dello spazio dei nomi XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-declare-and-use-xml-namespace-prefixes.md)  
 Viene illustrato come dichiarare un prefisso dello spazio dei nomi XML e utilizzarlo per creare e accedere agli elementi XML.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Proprietà Axis XML](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)  
 Vengono forniti collegamenti alle sezioni che descrivono le varie proprietà di accesso XML.  
  
 [Panoramica di LINQ to XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)  
 Viene fornita un'introduzione all'utilizzo di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] in Visual Basic.  
  
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 Viene fornita un'introduzione all'utilizzo di valori letterali XML in Visual Basic.  
  
 [Modifica di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)  
 Vengono forniti collegamenti alle sezioni sul caricamento e modifica di XML in Visual Basic.  
  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)  
 Vengono forniti collegamenti a sezioni in cui viene illustrato come utilizzare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] in Visual Basic.
