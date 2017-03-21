---
title: Distribuzione di applicazioni che fanno riferimento a controlli Power Pack (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Power Packs, deploying
ms.assetid: f2230f53-a745-4731-89e6-033943faa209
caps.latest.revision: 9
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
ms.openlocfilehash: 4d342e655dcfe18ed3b5fc1d2710571ed8e3369e
ms.lasthandoff: 03/13/2017

---
# <a name="deploying-applications-that-reference-power-packs-controls-visual-studio"></a>Distribuzione di applicazioni che fanno riferimento a controlli Power Pack (Visual Studio)
Se si desidera distribuire un'applicazione che fa riferimento a controlli Power Pack (<xref:Microsoft.VisualBasic.PowerPacks.LineShape>, <xref:Microsoft.VisualBasic.PowerPacks.OvalShape>, <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape>, o <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>), i controlli devono essere installati nel computer di destinazione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> </xref:Microsoft.VisualBasic.PowerPacks.OvalShape> </xref:Microsoft.VisualBasic.PowerPacks.LineShape>  
  
## <a name="installing-the-power-packs-controls-as-a-prerequisite"></a>Installare i controlli Power Pack come prerequisito  
 Per distribuire correttamente un'applicazione, è necessario distribuire anche tutti i componenti a cui viene fatto riferimento dall'applicazione. Il processo di installazione dei componenti prerequisiti è noto come *bootstrap*.  
  
 Quando [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] è installato nel computer di sviluppo, un Power Pack di avvio automatico viene aggiunto per il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] directory di avvio automatico. Questo pacchetto sarà disponibile quando si seguono le procedure per l'aggiunta di prerequisiti per la [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] o distribuzione di Windows Installer.  
  
 Per impostazione predefinita, i componenti con bootstrap vengono distribuiti dallo stesso percorso del pacchetto di installazione. In alternativa, è possibile scegliere di distribuire i componenti da un URL o un percorso di condivisione file, da cui gli utenti possono scaricarli in base alle esigenze.  
  
> [!NOTE]
>  Per installare i componenti con bootstrap, l'utente può richiedere autorizzazioni amministrative o di tipo simile per il computer. Per [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] applicazioni, ciò significa che l'utente dovrà disporre di autorizzazioni amministrative per installare l'applicazione, indipendentemente dal livello di sicurezza specificato dall'applicazione. Dopo l'installazione dell'applicazione, l'utente può eseguire l'applicazione senza autorizzazioni amministrative.  
  
 Durante l'installazione, agli utenti verranno richiesto di installare i controlli Power Pack se non sono presenti nel computer di destinazione.  
  
 In alternativa al bootstrap, è possibile distribuire preventivamente i controlli Power Pack utilizzando un sistema di distribuzione software elettronico, ad esempio Microsoft Systems Management Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: installare i prerequisiti con un'applicazione ClickOnce](http://msdn.microsoft.com/library/e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5)   
 [Controlli Visual Basic Power Pack](../../../visual-basic/developing-apps/windows-forms/power-packs-controls.md)
