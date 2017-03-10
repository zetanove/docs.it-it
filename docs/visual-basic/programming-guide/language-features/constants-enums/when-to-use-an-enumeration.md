---
title: "When to Use an Enumeration (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "enumerations [Visual Basic]"
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# When to Use an Enumeration (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Grazie alle enumerazioni l'utilizzo di insiemi di costanti correlate è più semplice.  Un'enumerazione, o `Enum`, è un nome simbolico che indica un insieme di valori.  Le enumerazioni sono considerate come tipi di dati e consentono di creare insiemi di costanti da utilizzare con variabili e proprietà.  
  
## Quando utilizzare un'enumerazione  
 È possibile utilizzare un'enumerazione ogni volta che una routine accetta un insieme limitato di variabili.  Le enumerazioni rendono il codice più chiaro e leggibile, in special modo quando vengono utilizzati nomi significativi.  
  
 Di seguito sono indicati i vantaggi offerti dall'uso delle enumerazioni.  
  
-   Riduzione degli errori causati dalla trasposizione o dall'errata digitazione dei numeri.  
  
-   Semplificazione delle successive operazioni di modifica ai valori.  
  
-   Semplificazione della lettura del codice con la conseguente riduzione delle probabilità di errore al suo interno.  
  
-   Garanzia di compatibilità con le versioni future.  Con le enumerazioni si riduce il rischio di errore del codice nell'eventualità di successive modifiche ai valori corrispondenti ai nomi dei membri.  
  
## Denominazione delle enumerazioni  
 Utilizzare una convenzione di denominazione per i membri delle enumerazioni.  Quando in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene rilevato un nome di membro dell'enumerazione, se altre librerie dei tipi di riferimento contengono lo stesso nome è possibile che venga generata un'eccezione.  Utilizzare un prefisso univoco per identificare i valori di un'applicazione o di un componente.  
  
 Quando si fa riferimento a un membro di un'enumerazione, è necessario qualificare il nome del membro con il nome dell'enumerazione o utilizzare l'istruzione `Imports`.  Per ulteriori informazioni, vedere [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md).  
  
## Enumerazioni predefinite  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili diverse enumerazioni predefinite, quali `FirstDayOfWeek` e `MsgBoxResul`, il cui scopo è quello di semplificare il codice.  Per un elenco di tali enumerazioni, vedere [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md).  
  
## Vedere anche  
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [How to: Refer to an Enumeration Member](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [How to: Iterate Through An Enumeration in Visual Basic](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [How to: Determine the String Associated with an Enumeration Value](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [Enum Statement](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)