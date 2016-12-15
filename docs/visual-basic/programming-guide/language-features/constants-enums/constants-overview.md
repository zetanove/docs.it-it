---
title: "Constants Overview (Visual Basic) | Microsoft Docs"
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
  - "constants"
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Constants Overview (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una costante è un nome significativo non soggetto a modifiche utilizzato in sostituzione di un numero o di una stringa.  Nelle costanti vengono memorizzati valori che, come suggerisce il nome, devono rimanere costanti durante l'esecuzione di un'applicazione.  L'utilizzo delle costanti consente di migliorare notevolmente la leggibilità del codice e di semplificarne la manutenzione.  Si consiglia di utilizzarle soprattutto nei codici che contengono valori utilizzati più volte o che dipendono da determinati numeri che risultano difficili da ricordare o che non hanno un chiaro significato.  
  
## Creazione e utilizzo delle costanti  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sono disponibili numerose costanti predefinite, utilizzate principalmente per la stampa e la visualizzazione.  È anche possibile creare costanti personalizzate mediante l'istruzione `Const`, utilizzando le stesse regole adottate per la creazione dei nomi di variabile.  Se `Option Strict` è `On`, è necessario dichiarare il tipo di costante in modo esplicito.  
  
 L'ambito di una costante, ovvero la parte del codice che può fare riferimento alla costante senza qualificarne il nome, corrisponde a quello di una variabile dichiarata nella stessa posizione.  Per creare una costante che esista all'interno dell'ambito di una routine particolare, dichiararla all'interno di tale routine.  Per creare una costante che sia disponibile in tutta l'applicazione, dichiararla nella sezione dichiarazioni della classe utilizzando la parola chiave `Public`.  
  
> [!NOTE]
>  Sebbene siano simili alle variabili, non è possibile modificare o assegnare nuovi valori alle costanti.  
  
 Le costanti utilizzate nel codice possono essere definite dal modello a oggetti relativo ai controlli o ai componenti utilizzati oppure possono essere definite dall'utente, ovvero personalizzate.  
  
## Costanti in fase di compilazione e in fase di esecuzione  
 Una costante in fase di compilazione viene calcolata al momento della compilazione del codice, mentre una costante in fase di esecuzione può essere calcolata solo durante l'esecuzione dell'applicazione.  Nel primo caso il valore della costante rimarrà lo stesso per ogni esecuzione dell'applicazione, mentre nel secondo il valore potrà variare ogni volta.  Le costanti in fase di compilazione sono necessarie in determinati casi, ad esempio i limiti di matrice, le espressioni case o gli inizializzatori degli enumeratori.  
  
## Argomenti della sezione  
  
|||  
|-|-|  
|Definizione|Termine|  
|[How to: Declare A Constant](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)|Illustra come utilizzare l'istruzione `Const` per dichiarare una costante e impostarne il valore. Dichiarando una costante si assegna al valore un nome significativo.|  
|[User\-Defined Constants](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)|Viene illustrata la creazione di costanti personalizzate, incluse le informazioni sull'ambito di validità e come evitare i riferimenti circolari.|  
|[Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)|Vengono fornite informazioni sul modo in cui il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] inizializza le costanti quando si disattiva`Option Explicit`.|  
|[How to: Group Related Constant Values Together](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-group-related-constant-values-together.md)|Dimostra come raggruppare i valori costanti correlati.|  
  
## Riferimento  
  
|||  
|-|-|  
|Definizione|Termine|  
|[Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)|Sono illustrate le costanti predefinite di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].|  
|[Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md)|Viene descritta l'istruzione `Const` e ne viene illustrato l'utilizzo.|  
|[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)|Viene descritta l'istruzione `Option Strict` e ne viene illustrato l'utilizzo.|  
  
## Vedere anche  
 [Enumerations Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [How to: Initialize an Array Variable in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)