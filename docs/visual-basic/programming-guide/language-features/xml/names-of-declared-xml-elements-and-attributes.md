---
title: I nomi di elementi XML dichiarati e attributi (Visual Basic) | Documenti di Microsoft
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
- declarations [XML in Visual Basic]
- element names [XML in Visual Basic]
- names in XML literals
- attribute names [XML in Visual Basic]
- XML literals [Visual Basic], element names
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: ed8ecf69170acf9745a4038975e7e3421722d52d
ms.lasthandoff: 03/13/2017

---
# <a name="names-of-declared-xml-elements-and-attributes-visual-basic"></a>Nomi di elementi e attributi XML dichiarati (Visual Basic)
In questo argomento vengono [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] linee guida per la denominazione di elementi XML e attributi nei valori letterali XML.  In un valore letterale XML, è possibile specificare un nome locale o un nome completo. Un nome completo è costituito da un prefisso dello spazio dei nomi XML, i due punti e un nome locale. Per ulteriori informazioni sui prefissi dello spazio dei nomi XML, vedere [letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## <a name="rules"></a>Regole  
 Un nome locale di un elemento o attributo in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] devono essere conformi alle regole seguenti.  
  
-   È possibile iniziare con uno spazio dei nomi. Deve iniziare con un carattere alfabetico o un carattere di sottolineatura (`_`).  
  
-   Deve contenere solo caratteri alfabetici, cifre decimali, caratteri di sottolineatura, punti (.) e trattini (-).  
  
-   Non è necessario più di 1.024 caratteri.  
  
-   I due punti presenti nei nomi indicano demarcazione dello spazio dei nomi. Pertanto, è possibile utilizzare i due punti solo per specificare uno spazio dei nomi XML per un determinato nome.  
  
 Inoltre, è necessario rispettare le seguenti indicazioni.  
  
-   La specifica XML 1.0 si riserva tutti i nomi che iniziano con la stringa "xml", di qualsiasi variazione di maiuscole. Pertanto, non utilizzare tali nomi per l'elemento e i nomi degli attributi.  
  
### <a name="name-length-guidelines"></a>Linee guida per la lunghezza nome  
 Ai fini pratici, un nome deve essere il più breve possibile durante identificare chiaramente la natura dell'elemento. Ciò migliora la leggibilità del codice e si riduce la dimensione della linea di lunghezza e file di origine.  
  
 Tuttavia, il nome non deve essere troppo breve che non adeguatamente descrive l'elemento o come utilizzato dal codice. Ciò è importante per la leggibilità del codice. Se qualcun altro sta tentando di capire o dall'utente sono guardando molto tempo dopo che è stato scritto, i nomi di elemento appropriato possono risparmiare tempo.  
  
## <a name="case-sensitivity-in-names"></a>Distinzione maiuscole/minuscole nei nomi  
 I nomi degli elementi XML sono sensibili alle maiuscole. Ciò significa che quando il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore confronta due nomi che differiscono solo case in ordine alfabetico, li interpreta come diversi nomi. Ad esempio, interpreta `ABC` e `abc` come riferiti a elementi distinti.  
  
## <a name="xml-namespaces"></a>Spazi dei nomi XML  
 Quando si crea un elemento XML letterale, è possibile specificare il prefisso dello spazio dei nomi XML per il nome dell'elemento. Per ulteriori informazioni, vedere [letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
