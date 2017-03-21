---
title: Dichiarare i nomi degli elementi (Visual Basic) | Documenti di Microsoft
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
- declared elements, case sensitivity
- names, Visual Basic rules
- naming conventions
- element names
- declared elements, identifiers
- declarations, elements
- declared elements, valid names
- '[] escape characters [Visual Basic]'
- names, elements
- declaration statements, declared elements
- declaring elements
- identifiers, declared elements
- case sensitivity, declared element names
- escape characters
- names, declared elements
- declared elements, about declared elements
- escaped names
- declared elements, names
- names, naming conventions
- identifiers, elements
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
caps.latest.revision: 27
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
ms.openlocfilehash: 56ac0684e5176f33aa6f9600f20d9fe3fcf09416
ms.lasthandoff: 03/13/2017

---
# <a name="declared-element-names-visual-basic"></a>Nomi di elementi dichiarati (Visual Basic)
Ogni elemento dichiarato è un nome, detto anche un *identificatore*, il codice utilizzato per fare riferimento a esso.  
  
## <a name="rules"></a>Regole  
 Nome dell'elemento in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] deve rispettare le regole seguenti:  
  
-   Deve iniziare con un carattere alfabetico o un carattere di sottolineatura (`_`).  
  
-   Deve contenere solo caratteri alfabetici, cifre e caratteri di sottolineatura.  
  
-   Deve contenere almeno un carattere alfabetico o cifra decimale che inizia con un carattere di sottolineatura.  
  
-   Non è necessario più di 1023 caratteri.  
  
 La lunghezza massima di 1023 caratteri si applica anche all'intera stringa di un nome completo, ad esempio `outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement`.  
  
 L'esempio seguente mostra alcuni nomi di elemento valido.  
  
 `aB123__45`  
  
 `_567`  
  
 L'esempio seguente mostra alcuni nomi di elemento non valido. Il primo contiene solo un carattere di sottolineatura, il secondo inizia con una cifra decimale e il terzo contiene un carattere non valido ($).  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
>  I nomi degli elementi a partire da un carattere di sottolineatura (`_`) non fanno parte del [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), pertanto il codice conforme a CLS non può utilizzare un componente che definisce tali nomi. Tuttavia, un carattere di sottolineatura in qualsiasi altra posizione nel nome di un elemento è conforme a CLS.  
  
### <a name="name-length-guidelines"></a>Linee guida per la lunghezza nome  
 In pratica, il nome deve essere il più breve possibile durante identificare chiaramente la natura dell'elemento. Ciò migliora la leggibilità del codice e si riduce la dimensione della linea di lunghezza e file di origine.  
  
 D'altra parte, il nome non deve essere troppo breve che non adeguatamente descrive ciò che rappresenta l'elemento e come utilizzato dal codice. Ciò è importante per la leggibilità del codice. Se qualcun altro sta tentando di capire, o dall'utente sono guardando molto tempo dopo che è stato scritto, nomi di elemento appropriato possono salvare una notevole quantità di tempo.  
  
## <a name="escaped-names"></a>Nomi in sequenza escape  
 In genere, un nome di elemento non deve corrispondere alle parole chiave riservate dal [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], ad esempio `Case` o `Friend`. Tuttavia, è possibile definire un *nome forzato*, che è racchiuso tra parentesi quadre (`[ ]`). Un nome forzato può corrispondere a qualsiasi [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] (parola chiave), poiché le parentesi quadre rimuovere qualsiasi ambiguità. È inoltre possibile utilizzare le parentesi quando si fa riferimento al nome nel codice.  
  
 In generale, è necessario utilizzare nomi in sequenza escape solo quando:  
  
-   Il codice è stata eseguita la migrazione da una versione precedente di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] che non era riservata la parola chiave viene utilizzata come un nome; o  
  
-   Si lavora con il codice scritto in un'altra lingua in cui non è riservata alla parola chiave specificata.  
  
 In caso contrario, è consigliabile rinominare l'elemento se il relativo nome in conflitto con una parola chiave. Ambiente di sviluppo integrato (IDE) fornisce un modo semplice per eseguire questa operazione. Per ulteriori informazioni, vedere [Refactoring](https://docs.microsoft.com/visualstudio/vb-ide/refactoring-vb).  
  
## <a name="case-sensitivity-in-names"></a>Distinzione maiuscole/minuscole nei nomi  
 I nomi di elemento in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tra maiuscole e minuscole. Ciò significa che quando il compilatore confronta due nomi che differiscono solo nelle maiuscole, li interpreta come lo stesso nome. Ad esempio, se si ha `ABC` e `abc` , il compilatore li interpreta come se facessero riferimento allo stesso elemento dichiarato.  
  
 Tuttavia, common language runtime (CLR) utilizza l'associazione tra maiuscole e minuscole. Perciò, quando si genera un assembly o una DLL e la si rende disponibile ad altri assembly, i nomi distinguono fra maiuscole e minuscole. Se ad esempio si definisce una classe con un elemento denominato `ABC`e altri assembly usano la classe mediante il Common Language Runtime, devono fare riferimento all'elemento come `ABC`. Se si successivamente ricompilare la classe e modificare il nome dell'elemento per `abc`, gli altri assembly che utilizzano la classe non è più possano accedere all'elemento. Pertanto, quando si rilascia una versione aggiornata di un assembly, non si devono modificare le maiuscole e le minuscole degli elementi pubblici.  
  
## <a name="names-and-locales"></a>I nomi e le impostazioni locali  
 Confronto dei nomi è indipendente dalle impostazioni locali. Se due nomi corrispondono in una lingua, è possibile garantirne la corrispondenza in tutte le impostazioni locali.  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [Caratteristiche di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Istruzioni](../../../../visual-basic/language-reference/statements/index.md)
