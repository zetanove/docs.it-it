---
title: Distribuzione di applicazioni che fanno riferimento al componente PrintForm (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- PrintForm component [Visual Basic], deploying
ms.assetid: b595ea44-a712-4625-a761-190c64f59bbe
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 016643329d2ee66ca5a32f155cf91e0ee137f38f
ms.lasthandoff: 03/13/2017

---
# <a name="deploying-applications-that-reference-the-printform-component-visual-basic"></a>Distribuzione di applicazioni che fanno riferimento al componente PrintForm (Visual Basic)
Se si desidera distribuire un'applicazione che fa riferimento il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente, il componente deve essere installato nel computer di destinazione.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall' [Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
## <a name="installing-the-printform-as-a-prerequisite"></a>Installazione di PrintForm come prerequisito  
 Per distribuire correttamente un'applicazione, è necessario distribuire anche tutti i componenti a cui viene fatto riferimento dall'applicazione. Il processo di installazione dei componenti prerequisiti è noto come *bootstrap*.  
  
 Quando il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente è installato nel computer di sviluppo, viene aggiunto un pacchetto di programma di avvio automatico di Microsoft Visual Basic Power Pack per il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] directory bootstrapper.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> Questo pacchetto sarà disponibile quando si seguono le procedure per l'aggiunta di prerequisiti per la [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] o distribuzione di Windows Installer.  
  
 Per impostazione predefinita, i componenti con bootstrap vengono distribuiti dallo stesso percorso del pacchetto di installazione. In alternativa, è possibile scegliere di distribuire i componenti da un URL o un percorso di condivisione file, da cui gli utenti possono scaricarli in base alle esigenze.  
  
> [!NOTE]
>  Per installare i componenti con bootstrap, l'utente può richiedere autorizzazioni amministrative o di tipo simile per il computer. Per [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] applicazioni, ciò significa che l'utente dovrà disporre di autorizzazioni amministrative per installare l'applicazione, indipendentemente dal livello di sicurezza specificato dall'applicazione. Dopo l'installazione dell'applicazione, l'utente può eseguire l'applicazione senza autorizzazioni amministrative.  
  
 Durante l'installazione, verranno richiesto agli utenti di installare il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente se non è presente nel computer di destinazione.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 In alternativa al bootstrap, è possibile distribuire il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente tramite un sistema electronic software distribution come Microsoft Systems Management Server.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: installare i prerequisiti con un'applicazione ClickOnce](http://msdn.microsoft.com/library/e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5)   
 [Componente PrintForm](../../../visual-basic/developing-apps/printing/printform-component.md)
