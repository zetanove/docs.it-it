---
title: "Procedura: utilizzare una classe generica (Visual Basic) | Microsoft Docs"
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
  - "parametri di tipo, definizione"
  - "argomenti del tipo di dati, definizione"
  - "argomenti [Visual Basic], tipi di dati"
  - "Of (parola chiave), uso"
  - "parametri generici"
  - "parametri di tipo di dati"
  - "generics [Visual Basic], informazioni su generics"
  - "tipi di dati [Visual Basic], come parametri"
  - "tipi di dati [Visual Basic], come argomenti"
  - "parametri, tipo"
  - "tipi [Visual Basic], generici"
  - "parametri, generici"
  - "generics [Visual Basic], creazione di tipi generici"
  - "argomenti del tipo di dati"
  - "parametri, tipo di dati"
  - "parametri di tipo di dati, definizione"
  - "argomenti di tipo, definizione"
  - "argomenti [Visual Basic], tipo"
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Procedura: utilizzare una classe generica (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una classe che accetta *parametri di tipo* è chiamato *classe generica*. Se si usa una classe generica, è possibile generare una *classe costruita* da essa fornendo un *argomento di tipo* per ciascuno di questi parametri. È possibile quindi dichiarare una variabile del tipo di classe costruita, creare un'istanza della classe costruita e assegnarla alla variabile.  
  
 Oltre alle classi, è possibile definire e usare anche strutture, interfacce, routine e delegati generici.  
  
 La procedura seguente accetta una classe generica definita in [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] e crea un'istanza da essa.  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a>Per usare una classe che accetta un parametro di tipo  
  
1.  All'inizio del file di origine, includere un'[istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) per importare lo spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>. In questo modo è possibile fare riferimento alla classe <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> senza doverla specificare completamente per differenziarla da altre classi Queue come <xref:System.Collections.Queue?displayProperty=fullName>.  
  
2.  Creare l'oggetto in modo normale, ma aggiungere `(Of` `type``)` immediatamente dopo il nome della classe.  
  
     L'esempio seguente usa la stessa classe (<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>) per creare due oggetti queue che contengono elementi con tipi di dati diversi. Aggiunge gli elementi alla fine di ogni coda e quindi rimuove e visualizza gli elementi dall'inizio di ogni coda.  
  
     [!code-vb[VbVbalrDataTypes#9](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-use-a-generic-class_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)   
 [Of](../../../../visual-basic/language-reference/statements/of-clause.md)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Procedura: Definire una classe in grado di fornire funzionalità identiche con tipi di dati diversi](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)   
 [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)