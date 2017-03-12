---
title: "Names of Declared XML Elements and Attributes (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declarations [XML in Visual Basic]"
  - "element names [XML in Visual Basic]"
  - "names in XML literals"
  - "attribute names [XML in Visual Basic]"
  - "XML literals [Visual Basic], element names"
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Names of Declared XML Elements and Attributes (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento vengono fornite linee guida di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] per denominare elementi e attributi XML nei valori letterali XML. In un valore letterale XML, è possibile specificare un nome locale o un nome completo.  Un nome completo è composto da un prefisso degli spazi dei nomi XML, i due punti e un nome locale.  Per ulteriori informazioni sui prefissi degli spazi dei nomi XML, vedere [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## Regole  
 Un nome locale di un elemento o attributo in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] deve rispettare le seguenti regole.  
  
-   Può iniziare con uno spazio dei nomi.  Deve iniziare con un carattere alfabetico o con un carattere di sottolineatura \(`_`\).  
  
-   Deve contenere solo caratteri alfabetici, cifre decimali, caratteri di sottolineatura, punti \(.\) o trattini \(\-\).  
  
-   Non deve superare la lunghezza massima di 1,024 caratteri.  
  
-   I due punti presenti nei nomi indicano la demarcazione dello spazio dei nomi.  Pertanto, è possibile utilizzare i due punti solo per specificare uno spazio dei nomi XML per un particolare nome.  
  
 Inoltre è necessario rispettare le seguenti indicazioni.  
  
-   Nelle specifiche XML 1.0, tutti i nomi che iniziano con la stringa "xml", in qualsiasi combinazione di maiuscole o minuscole, sono riservati  Pertanto tali nomi non devono essere utilizzati per i nomi di elementi e i attributi.  
  
### Indicazioni sulla lunghezza dei nomi  
 Per praticità, un nome dovrebbe essere il più breve possibile e al tempo stesso identificare chiaramente la tipologia dell'elemento.  Questo consente di migliorare la leggibilità del codice e di ridurre la lunghezza delle righe e la dimensione del file di origine.  
  
 Tuttavia è necessario che il nome abbia una lunghezza sufficiente per descrivere adeguatamente l'elemento o il modo in cui viene essere utilizzato dal codice.  Questa caratteristica è importante per la leggibilità del codice.  L'utilizzo di nomi adeguati consente infatti un notevole risparmio di tempo sia agli altri utenti che dovranno comprendere la funzione dell'elemento che allo stesso autore che dovrà riutilizzare l'elemento dopo un lungo periodo di tempo.  
  
## Distinzione tra maiuscole e minuscole nei nomi  
 Per i nomi degli elementi viene fatta distinzione tra maiuscole e minuscole.  Pertanto, quando il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] confronta due nomi che differiscono solo per le maiuscole e minuscole dei caratteri alfabetici, li interpreta come se fossero nomi diversi.  Ad esempio, `ABC` e `abc` vengono interpretati come riferiti a elementi distinti.  
  
## Spazi dei nomi XML  
 Quando si crea un valore letterale di un elemento XML, è possibile specificare il prefisso dello spazio dei nomi XML per il nome dell'elemento.  Per ulteriori informazioni, vedere [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## Vedere anche  
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)