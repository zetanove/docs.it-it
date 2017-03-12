---
title: "A startup form has not been specified | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrAppModel_NoStartupForm"
dev_langs: 
  - "VB"
ms.assetid: 8e04af49-4bef-49de-a7ec-e407e9873da7
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# A startup form has not been specified
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'applicazione viene utilizzata la classe <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> ma non viene specificato il form di avvio.  
  
 Questa situazione può verificarsi se in Progettazione progetti è selezionata la casella di controllo **Attiva framework applicazione**, ma non è stato specificato il **Form di avvio**.  Per ulteriori informazioni, vedere [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic).  
  
### Per correggere l'errore  
  
1.  Specificare un oggetto di avvio per l'applicazione.  
  
     Per ulteriori informazioni, vedere [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic).  
  
2.  Eseguire l'override del metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> per impostare la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> al form di avvio.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>   
 [Overview of the Visual Basic Application Model](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)