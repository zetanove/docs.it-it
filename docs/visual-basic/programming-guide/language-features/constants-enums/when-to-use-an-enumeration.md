---
title: Quando utilizzare un&quot;enumerazione (Visual Basic) | Documenti di Microsoft
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
- enumerations [Visual Basic]
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
caps.latest.revision: 12
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
ms.openlocfilehash: f22102a2e1e7eafd7fcf4db1f46af2cc622eba70
ms.lasthandoff: 03/13/2017

---
# <a name="when-to-use-an-enumeration-visual-basic"></a>Quando utilizzare un'enumerazione (Visual Basic)
Enumerazioni offrono un modo semplice per l'utilizzo di set di costanti correlate. Un'enumerazione, o `Enum`, è un nome simbolico per un set di valori. Le enumerazioni sono considerate come tipi di dati e utilizzarli per creare set di costanti per l'utilizzo con variabili e proprietà.  
  
## <a name="when-to-use-an-enumeration"></a>Quando utilizzare un'enumerazione  
 Ogni volta che una routine accetta un numero limitato di variabili, è consigliabile utilizzare un'enumerazione. Le enumerazioni rendono il codice più chiaro e più leggibile, soprattutto quando vengono utilizzati nomi significativi.  
  
 I vantaggi dell'utilizzo di enumerazioni includono:  
  
-   Per ridurre gli errori causati dalla trasposizione o digitazione di numeri.  
  
-   Consente di modificare i valori in futuro.  
  
-   Rende il codice più leggibile, ciò significa che è meno probabile che gli errori al suo interno.  
  
-   Garantisce la compatibilità. Con enumerazioni, il codice è meno probabile che non venga completata se in futuro un utente modifica i valori corrispondenti ai nomi dei membri.  
  
## <a name="naming-enumerations"></a>Denominazione delle enumerazioni  
 Utilizzare una convenzione di denominazione per i membri di enumerazione. Quando [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] viene rilevato un nome di membro di enumerazione, potrebbe essere generata un'eccezione se altre librerie dei tipi di riferimento contengono lo stesso nome. Utilizzare un prefisso univoco che identifica i valori di un'applicazione o componente.  
  
 Quando si fa riferimento a un membro di enumerazione, è necessario qualificare il nome del membro con il nome di enumerazione o utilizzare il `Imports` istruzione. Per ulteriori informazioni, vedere [qualifica di nomi ed enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md).  
  
## <a name="predefined-enumerations"></a>Enumerazioni predefinite  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un numero di enumerazioni predefinite, ad esempio `FirstDayOfWeek` e `MsgBoxResul`t, per semplificare il codice. Per un elenco di questi vedere [costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: dichiarare un'enumerazione](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Procedura: fare riferimento a un membro di enumerazione](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [Qualifica di nomi ed enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Procedura: scorrere un'enumerazione in Visual Basic](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [Procedura: determinare la stringa associata a un valore di enumerazione](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [Istruzione Enum](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md)
