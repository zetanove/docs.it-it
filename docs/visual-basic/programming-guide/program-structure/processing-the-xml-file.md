---
title: Elaborazione del File XML (Visual Basic) | Documenti di Microsoft
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
- XML comments, parsing [Visual Basic]
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
caps.latest.revision: 16
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
ms.openlocfilehash: 72b2832d0131adf39a37ebd9297b43fb34ea49ba
ms.lasthandoff: 03/13/2017

---
# <a name="processing-the-xml-file-visual-basic"></a>Elaborazione del file XML (Visual Basic)
Il compilatore genera una stringa ID per ogni costrutto nel codice che contiene tag per generare la documentazione. (Per informazioni su come contrassegnare il codice, vedere [tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md).) Stringa ID identifica in modo univoco il costrutto. I programmi che elaborano il file XML è possono utilizzare la stringa di ID per identificare il corrispondente [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] elemento metadati/reflection.  
  
 Il file XML non è una rappresentazione gerarchica del codice. è un elenco semplice con un ID generato per ogni elemento.  
  
 Quando genera le stringhe di ID, il compilatore applica le regole seguenti:  
  
-   Gli spazi vuoti non viene inserito nella stringa.  
  
-   La prima parte della stringa di ID identifica il tipo di membro identificato, con un singolo carattere seguito da due punti. Vengono utilizzati i seguenti tipi di membro.  
  
|Carattere|Descrizione|  
|---|---|  
|N|namespace<br /><br /> È possibile aggiungere commenti sulla documentazione a uno spazio dei nomi, ma è possibile creare riferimenti CREF ad essi, in cui è supportata.|  
|T|type: `Class`, `Module`, `Interface`, `Structure`, `Enum`,`Delegate`|  
|F|campo:`Dim`|  
|P|proprietà: `Property` (incluse le proprietà predefinite)|  
|M|method: `Sub`, `Function`, `Declare`,`Operator`|  
|E|evento:`Event`|  
|!|stringa di errore<br /><br /> Il resto della stringa vengono fornite informazioni sull'errore. Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] il compilatore genera informazioni di errore per i collegamenti che non possono essere risolti.|  
  
-   La seconda parte di `String` è il nome completo dell'elemento, iniziando dalla radice dello spazio dei nomi. Il nome dell'elemento, il relativo tipo contenitore e lo spazio dei nomi sono separati da punti. Se il nome dell'elemento stesso contiene punti, vengono sostituiti con il simbolo di cancelletto (#). Si presuppone che nessun elemento è un simbolo di cancelletto direttamente nel relativo nome. Ad esempio, il nome completo di `String` costruttore sarebbe `System.String.#ctor`.  
  
-   Per le proprietà e metodi, se sono presenti argomenti del metodo, l'elenco di argomenti racchiuso tra parentesi. Se non sono presenti argomenti, le parentesi non sono presenti. Gli argomenti sono separati da virgole. La codifica di ciascun argomento simile alla modalità di codifica un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] firma.  
  
## <a name="example"></a>Esempio  
 Nel codice seguente viene illustrato come le stringhe di ID per una classe e i relativi membri vengono generati.  
  
 [!code-vb[VbVbcnXmlDocComments&#10;](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/processing-the-xml-file_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [Procedura: Creare documentazione XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
