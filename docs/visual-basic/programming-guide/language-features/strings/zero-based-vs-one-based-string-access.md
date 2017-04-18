---
title: Visual Studio in base zero. Accesso basato su una stringa in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
caps.latest.revision: 11
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
ms.openlocfilehash: 6cd2cab888bf336151ed26968119431f4ffc75f4
ms.lasthandoff: 03/13/2017

---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a>Visual Studio in base zero. Accesso basato su una stringa in Visual Basic
Questo argomento vengono confrontate come [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] e [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] forniscono l'accesso ai caratteri in una stringa. Il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] fornisce sempre l'accesso in base zero per i caratteri in una stringa, mentre [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce l'accesso in base zero e in base uno, a seconda della funzione.  
  
## <a name="one-based"></a>In base uno  
 Per un esempio di base uno [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] funzione, prendere in considerazione il `Mid` (funzione). Accetta un argomento che indica la posizione del carattere in cui inizia la sottostringa, a partire dalla posizione 1. Il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Substring%2A?displayProperty=fullName>metodo accetta un indice del carattere nella stringa in cui iniziare la sottostringa a partire dalla posizione 0.</xref:System.String.Substring%2A?displayProperty=fullName> Pertanto, se si dispone di una stringa "ABCDE", i singoli caratteri sono numerati 1,2,3,4,5 per l'utilizzo con il `Mid` funzione, ma 0,1,2,3,4 per l'utilizzo con il <xref:System.String.Substring%2A?displayProperty=fullName>(metodo).</xref:System.String.Substring%2A?displayProperty=fullName>  
  
## <a name="zero-based"></a>In base zero  
 Per un esempio di oggetto in base zero [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] funzione, prendere in considerazione il `Split` (funzione). Suddivide una stringa e restituisce una matrice contenente le sottostringhe. Il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Split%2A?displayProperty=fullName>metodo inoltre suddivide una stringa e restituisce una matrice contenente le sottostringhe.</xref:System.String.Split%2A?displayProperty=fullName> Poiché il `Split` funzione e <xref:System.String.Split%2A>metodo restituiscono [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] matrici, devono essere in base zero.</xref:System.String.Split%2A>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A></xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A></xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:System.String.Substring%2A></xref:System.String.Substring%2A>   
 <xref:System.String.Split%2A></xref:System.String.Split%2A>   
 [Introduzione alle stringhe in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
