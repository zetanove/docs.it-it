---
title: Tipi di dati vari (Visual Basic) | Documenti di Microsoft
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
- Object data type, data types
- data types [Visual Basic], choosing
ms.assetid: 64c71a12-9057-4dbf-baca-7379c4aada69
caps.latest.revision: 22
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
ms.openlocfilehash: 2de377fa9dfd7ec13cdbb9b700f8485b0c0e2106
ms.lasthandoff: 03/13/2017

---
# <a name="miscellaneous-data-types-visual-basic"></a>Tipi di dati vari (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce diversi tipi di dati che non sono riconducibili a numeri o caratteri. Al contrario, gestiscano dati specializzati, ad esempio Sì/no valori, valori data/ora e gli indirizzi di oggetto.  
  
 Per una tabella che mostra un confronto side-by-side di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tipi di dati, vedere [tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## <a name="boolean-type"></a>Tipo booleano  
 Il [tipo di dati Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) è un valore senza segno viene interpretato come `True` o `False`. Ampiezza dei relativi dati dipende dalla piattaforma di implementazione. Se una variabile può contenere solo i valori di due stati, ad esempio true/false, sì/no o on/off, dichiararla come `Boolean`.  
  
## <a name="date-type"></a>Date (tipo)  
 Il [tipo di dati Date](../../../../visual-basic/language-reference/data-types/date-data-type.md) è un valore a 64 bit che contiene informazioni sia data e ora. Ogni incremento rappresenta 100 nanosecondi di tempo trascorso dall'inizio (12:00 AM) del 1 ° gennaio dell'anno 1 nel calendario gregoriano. Se una variabile può contenere un valore di data, un valore di ora o entrambi, dichiararla come `Date`.  
  
## <a name="object-type"></a>Tipo di oggetto  
 Il [tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md) è un indirizzo a 32 bit che punta a un'istanza dell'oggetto all'interno dell'applicazione o in un'altra applicazione. Un `Object` variabile può fare riferimento a qualsiasi oggetto riconosciuto dall'applicazione o ai dati di qualsiasi tipo di dati. Sono inclusi sia *i tipi di valore*, ad esempio `Integer`, `Boolean`e le istanze della struttura, e *tipi di riferimento*, che sono istanze degli oggetti creati dalle classi, ad esempio `String` e <xref:System.Windows.Forms.Form>e le istanze di matrici.</xref:System.Windows.Forms.Form>  
  
 Se una variabile archivia un puntatore a un'istanza di una classe che non si conosce in fase di compilazione o se può puntare a vari tipi di dati, dichiararla come `Object`.  
  
 Il vantaggio di `Object` è di tipo di dati che è possibile utilizzare per archiviare i dati di qualsiasi tipo di dati. Lo svantaggio è che sono necessarie operazioni aggiuntive che richiedono più tempo di esecuzione e rendere l'applicazione calo delle prestazioni. Se si utilizza un `Object` variabili per i tipi di valore, si incorre in *boxing* e *unboxing*. Se è utilizzata per i tipi di riferimento, sono necessarie *l'associazione tardiva*.  
  
## <a name="see-also"></a>Vedere anche  
 [Caratteri tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi di dati numerici](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [Tipi di dati carattere](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Associazione anticipata e tardiva](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
