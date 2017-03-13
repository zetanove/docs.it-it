---
title: "User-Defined Constants (Visual Basic) | Microsoft Docs"
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
  - "constants, circular references"
  - "Const statement [Visual Basic], user-defined constants"
  - "user-defined constants"
  - "scope, constants"
  - "constants, user-defined"
  - "circular references between constants"
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# User-Defined Constants (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una costante è un nome significativo non soggetto a modifiche utilizzato in sostituzione di un numero o di una stringa.  Nelle costanti sono memorizzati valori che, come suggerisce il nome, rimangono costanti durante l'esecuzione di un'applicazione.  È possibile utilizzare costanti definite dai controlli o dai componenti in uso oppure crearne versioni personalizzate.  Le costanti personalizzate sono descritte come *definite dall'utente*.  
  
 L'istruzione `Const` consente di dichiarare una costante, utilizzando le stesse regole adottate per la creazione di un nome di variabile.  Se `Option Strict` è `On`, è necessario dichiarare il tipo di costante in modo esplicito.  
  
## Utilizzo dell'istruzione Const  
 Un'istruzione `Const` può rappresentare una quantità matematica o data\/ora:  
  
 [!code-vb[VbEnumsTask#10](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_1.vb)]  
  
 È inoltre in grado di definire costanti `String`:  
  
 [!code-vb[VbEnumsTask#13](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_2.vb)]  
  
 L'espressione a destra del segno di uguale \( `=` \) è spesso un numero o una stringa letterale, ma può essere anche un'espressione che restituisce un numero o una stringa, purché non contenga chiamate di funzioni.  È possibile persino definire costanti in termini di costanti definite in precedenza:  
  
 [!code-vb[VbEnumsTask#15](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_3.vb)]  
  
## Ambito delle costanti definite dall'utente  
 L'ambito di un'istruzione `Const` corrisponde all'ambito di una variabile dichiarata nella stessa posizione.  È possibile specificare l'ambito in uno dei seguenti modi:  
  
-   Per creare una costante che esista all'interno di una routine, dichiararla all'interno di tale routine.  
  
-   Per creare una costante che sia disponibile a tutte le routine di una classe, ma non al codice all'esterno di quel modulo, dichiararla nella sezione dichiarazioni della classe.  
  
-   Per creare una costante che sia disponibile a tutti i membri di un assembly, ma non ai client all'esterno dell'assembly, dichiararla nella sezione delle dichiarazioni della classe utilizzando la parola chiave `Friend`.  
  
-   Per creare una costante che sia disponibile in tutta l'applicazione, dichiararla nella sezione dichiarazioni della classe utilizzando la parola chiave `Public`.  
  
 Per ulteriori informazioni, vedere [How to: Declare A Constant](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md).  
  
### Riferimenti circolari  
 Poiché le costanti possono essere definite in termini di altre costanti, è possibile che si crei inavvertitamente un *ciclo*, o riferimento circolare, tra due o più costanti.  Un ciclo si verifica quando esistono due o più costanti pubbliche, ciascuna delle quali è definita nei termini dell'altra, come nell'esempio seguente:  
  
 [!code-vb[VbEnumsTask#16](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_4.vb)]  
[!code-vb[VbEnumsTask#17](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_5.vb)]  
  
 Se si verifica un ciclo, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]viene generato un errore di compilazione.  
  
## Vedere anche  
 [Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Constants and Enumerations](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [Enumerations Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [Constants Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)