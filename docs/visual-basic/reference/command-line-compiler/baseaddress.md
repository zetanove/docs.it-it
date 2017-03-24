---
title: /baseaddress | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /baseaddress
- baseaddress
dev_langs:
- VB
helpviewer_keywords:
- -baseaddress compiler option [Visual Basic]
- /baseaddress compiler option [Visual Basic]
- baseaddress compiler option [Visual Basic]
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
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
ms.openlocfilehash: 527a7c348583498f46ee094ef9b9eec9abf1bcd0
ms.lasthandoff: 03/13/2017

---
# <a name="baseaddress"></a>/baseaddress
Specifica un indirizzo di base predefinito durante la creazione di una DLL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/baseaddress:address  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`address`|Obbligatorio. L'indirizzo di base per la DLL. Questo indirizzo deve essere specificato come numero esadecimale.|  
  
## <a name="remarks"></a>Note  
 L'indirizzo di base predefinito per una DLL è impostato il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 Tenere presente che la parola di ordine inferiore in questo indirizzo viene arrotondata. Ad esempio, se si specifica 0x11110001, verrà arrotondato a 0x11110000.  
  
 Per completare il processo di firma di una DLL, utilizzare il `–R` opzione dello strumento nome sicuro (Sn.exe).  
  
 Questa opzione viene ignorata se la destinazione non è una DLL.  
  
|Per impostare /baseaddress nell'IDE di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Scegliere **Avanzate**.<br />4.  Modificare il valore di **indirizzo di base DLL:** casella. **Nota:** il **indirizzo di base DLL:** casella è di sola lettura, a meno che la destinazione è una DLL.|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sn.exe (strumento nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23)
