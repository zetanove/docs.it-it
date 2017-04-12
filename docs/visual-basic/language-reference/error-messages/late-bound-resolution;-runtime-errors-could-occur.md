---
title: Risoluzione con associazione tardiva; potrebbero verificarsi degli errori di runtime | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42017
- BC42017
dev_langs:
- VB
helpviewer_keywords:
- BC42017
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
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
ms.openlocfilehash: 3ac885b0de2c4f44d4323487fc55cde9b23defa4
ms.lasthandoff: 03/13/2017

---
# <a name="late-bound-resolution-runtime-errors-could-occur"></a>Risoluzione ad associazione tardiva; potrebbero verificarsi degli errori in fase di esecuzione
Un oggetto viene assegnato a una variabile dichiarata di tipo di [tipo di dati Object](../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 Quando si dichiara una variabile come `Object`, il compilatore deve eseguire *l'associazione tardiva*, che determina operazioni supplementari in fase di esecuzione. Espone inoltre l'applicazione a possibili errori di runtime. Ad esempio, se si assegna un <xref:System.Windows.Forms.Form>per il `Object` variabile e si tenta di accedere il <xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName>proprietà, il runtime genera un <xref:System.MemberAccessException>perché la <xref:System.Windows.Forms.Form>classe non espone un `NameTable` proprietà.</xref:System.Windows.Forms.Form> </xref:System.MemberAccessException> </xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName> </xref:System.Windows.Forms.Form>  
  
 Se si dichiara la variabile di un tipo specifico, il compilatore può eseguire *associazione anticipata* in fase di compilazione. Ciò comporta un miglioramento delle prestazioni, controllo dell'accesso ai membri del tipo specifico e una migliore leggibilità del codice.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42017  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se possibile, dichiarare la variabile di un tipo specifico.  
  
## <a name="see-also"></a>Vedere anche  
 [Associazione anticipata e tardiva](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [Dichiarazione di variabili oggetto](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
