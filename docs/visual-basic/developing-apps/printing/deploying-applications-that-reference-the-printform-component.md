---
title: "Deploying Applications That Reference the PrintForm Component (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "PrintForm component [Visual Basic], deploying"
ms.assetid: b595ea44-a712-4625-a761-190c64f59bbe
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Deploying Applications That Reference the PrintForm Component (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se si vuole distribuire un'applicazione che fa riferimento al componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>, il componente deve essere installato nel computer di destinazione.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall'[Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
## Installazione di PrintForm come prerequisito  
 Per distribuire correttamente un'applicazione, è necessario distribuire anche tutti i componenti a cui viene fatto riferimento dall'applicazione. Il processo di installazione dei componenti prerequisiti è noto come *bootstrap*.  
  
 Quando il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> è installato nel computer di sviluppo, viene aggiunto un pacchetto bootstrapper di Microsoft Visual Basic PowerPacks alla directory bootstrapper [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)]. Questo pacchetto sarà quindi disponibile quando si eseguono le procedure per l'aggiunta dei prerequisiti per la distribuzione tramite [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] o Windows Installer.  
  
 Per impostazione predefinita, i componenti con bootstrap vengono distribuiti dallo stesso percorso del pacchetto di installazione. In alternativa, è possibile scegliere di distribuire i componenti da un URL o un percorso di condivisione file, da cui gli utenti possono scaricarli in base alle esigenze.  
  
> [!NOTE]
>  Per installare i componenti con bootstrap, l'utente può richiedere autorizzazioni amministrative o di tipo simile per il computer. Per le applicazioni [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)], questo significa che l'utente dovrà disporre di autorizzazioni amministrative per installare l'applicazione, indipendentemente dal livello di sicurezza specificato dall'applicazione. Dopo l'installazione dell'applicazione, l'utente può eseguire l'applicazione senza autorizzazioni amministrative.  
  
 Durante l'installazione, verrà richiesto agli utenti di installare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>, se non è presente nel computer di destinazione.  
  
 In alternativa al bootstrap, è possibile pre\-distribuire il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> mediante un sistema elettronico di distribuzione del software come Microsoft Systems Management Server.  
  
## Vedere anche  
 [How to: Install Prerequisites with a ClickOnce Application](../Topic/How%20to:%20Install%20Prerequisites%20with%20a%20ClickOnce%20Application.md)   
 [Not in Build: Scelta di una strategia di distribuzione](http://msdn.microsoft.com/it-it/ecd632d8-063c-4028-b785-81bba045107b)   
 [PrintForm Component](../../../visual-basic/developing-apps/printing/printform-component.md)