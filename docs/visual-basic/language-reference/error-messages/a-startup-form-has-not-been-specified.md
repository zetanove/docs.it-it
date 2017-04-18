---
title: "Non è stato specificato un form di avvio | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrAppModel_NoStartupForm
dev_langs:
- VB
ms.assetid: 8e04af49-4bef-49de-a7ec-e407e9873da7
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
ms.openlocfilehash: 598bbdb7e2269f568a0dcf120cb2e8c5c8bc6812
ms.lasthandoff: 03/13/2017

---
# <a name="a-startup-form-has-not-been-specified"></a>Non è stato specificato un form di avvio
L'applicazione utilizza la <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>classe ma non viene specificato il form di avvio.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>  
  
 Questa situazione può verificarsi se il **Attiva framework applicazione** casella di controllo è selezionata in Progettazione progetti, ma il **form di avvio** non è specificato. Per ulteriori informazioni, vedere [pagina applicazione, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Specificare un oggetto di avvio per l'applicazione.  
  
     Per ulteriori informazioni, vedere [pagina applicazione, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
2.  Eseguire l'override di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>per impostare il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>proprietà al form di avvio.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>   
 [Cenni preliminari sul modello di applicazione Visual Basic](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)
