---
title: Utilizzo efficiente dei tipi di dati (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- performance, data type efficiency
- data types [Visual Basic], weak typing
- AscW function, preferred to Asc
- data types [Visual Basic], using efficiently
- optimization, data types
- data types [Visual Basic], strong typing
- strong typing
- typing, strong
- data types [Visual Basic], optimizing
- ChrW function, preferred to Chr
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
caps.latest.revision: 16
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
ms.openlocfilehash: b81a1c81d970beee32925c3f2fe6ca3bcad79151
ms.lasthandoff: 03/13/2017

---
# <a name="efficient-use-of-data-types-visual-basic"></a>Utilizzo efficiente dei tipi di dati (Visual Basic)
Le variabili non dichiarate e le variabili dichiarate senza un tipo di dati vengono assegnate i `Object` tipo di dati. Questo facilita la scrittura di programmi rapidamente, ma è possibile che vengano eseguite più lentamente.  
  
## <a name="strong-typing"></a>Tipizzazione forte  
 Specifica dei tipi di dati per tutte le variabili è noto come *la tipizzazione forte*. Con la tipizzazione forte presenta diversi vantaggi:  
  
-   Consente il supporto IntelliSense per le variabili. Ciò consente di visualizzare le relative proprietà e gli altri membri durante la digitazione del codice.  
  
-   Consente di usufruire del controllo del tipo del compilatore. Questo memorizza nella cache le istruzioni che possono avere esito negativo in fase di esecuzione a causa di errori, ad esempio overflow. Inoltre, intercetta le chiamate ai metodi su oggetti che non li supportano.  
  
-   Comporta un'esecuzione più rapida del codice.  
  
## <a name="most-efficient-data-types"></a>Tipi di dati più efficienti  
 Per le variabili che non contengono mai frazioni, i tipi di dati integrali sono più efficienti rispetto ai tipi non integrali. In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], `Integer` e `UInteger` sono i tipi numerici più efficienti.  
  
 Per i numeri frazionari, `Double` è il tipo di dati più efficiente, perché i processori disponibili sulle attuali piattaforme eseguono operazioni a virgola mobile a precisione doppia. Tuttavia, le operazioni con `Double` non sono più veloci con i tipi integrali, ad esempio `Integer`.  
  
## <a name="specifying-data-type"></a>Specifica il tipo di dati  
 Utilizzare il [Dim (istruzione)](../../../../visual-basic/language-reference/statements/dim-statement.md) per dichiarare una variabile di un tipo specifico. È possibile specificare contemporaneamente il livello di accesso tramite il [pubblica](../../../../visual-basic/language-reference/modifiers/public.md), [protetti](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md), o [privata](../../../../visual-basic/language-reference/modifiers/private.md) (parola chiave), come nell'esempio seguente.  
  
```  
Private x As Double  
Protected s As String  
```  
  
## <a name="character-conversion"></a>Conversione di caratteri  
 Il `AscW` e `ChrW` funzioni operano in Unicode. È necessario utilizzarle in alternativa a `Asc` e `Chr`, che devono essere convertite in Unicode.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A></xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A></xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A></xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A></xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi di dati numerici](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [Dichiarazione di variabile](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Uso di IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense)
