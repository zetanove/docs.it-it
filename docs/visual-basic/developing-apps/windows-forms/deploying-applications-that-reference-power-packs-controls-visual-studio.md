---
title: "Deploying Applications That Reference Power Packs Controls (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Power Packs, deploying"
ms.assetid: f2230f53-a745-4731-89e6-033943faa209
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Deploying Applications That Reference Power Packs Controls (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per distribuire un'applicazione che fa riferimento ai controlli Power Pack <xref:Microsoft.VisualBasic.PowerPacks.LineShape>, <xref:Microsoft.VisualBasic.PowerPacks.OvalShape>, <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> o <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, questi devono essere installati nel computer di destinazione.  
  
## Installazione dei controlli Power Pack come prerequisito  
 Per distribuire correttamente un'applicazione, è necessario distribuire anche tutti i componenti a cui l'applicazione fa riferimento.  Il processo di installazione dei componenti necessari è noto come *avvio automatico*.  
  
 Quando [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] viene installato nel computer di sviluppo, alla directory del programma di avvio automatico di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] viene aggiunto un package del programma di avvio automatico di Power Pack.  Questo package è quindi disponibile durante l'esecuzione delle procedure per l'aggiunta di prerequisiti per la distribuzione di [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] o Windows Installer.  
  
 Per impostazione predefinita, i componenti ad avvio automatico vengono distribuiti dallo stesso percorso del pacchetto di installazione.  In alternativa, è possibile scegliere di distribuire i componenti da un URL o da un percorso di condivisione dei file da cui gli utenti possano scaricarli all'occorrenza.  
  
> [!NOTE]
>  Per installare i componenti ad avvio automatico, potrebbe essere necessario che l'utente disponga di autorizzazioni amministrative o simili sul computer.  Di conseguenza, per le applicazioni [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)], l'utente dovrà disporre di autorizzazioni amministrative per installare l'applicazione, indipendentemente dal livello di sicurezza specificato dall'applicazione stessa.  Dopo l'installazione, l'utente potrà eseguire l'applicazione senza autorizzazioni amministrative.  
  
 Durante l'installazione, verrà richiesto agli utenti di installare i controlli Power Pack eventualmente non presenti nel computer di destinazione.  
  
 In alternativa all'avvio automatico è possibile distribuire preventivamente i controlli Power Pack utilizzando un sistema elettronico di distribuzione del software quale Microsoft Systems Management Server \(SMS\).  
  
## Vedere anche  
 [How to: Install Prerequisites in Windows Installer Deployment](http://msdn.microsoft.com/it-it/653fc868-2486-429c-b75e-2f9d0c7f6619)   
 [How to: Install Prerequisites with a ClickOnce Application](../Topic/How%20to:%20Install%20Prerequisites%20with%20a%20ClickOnce%20Application.md)   
 [Not in Build: Choosing a Deployment Strategy](http://msdn.microsoft.com/it-it/ecd632d8-063c-4028-b785-81bba045107b)   
 [Visual Basic Power Packs Controls](../../../visual-basic/developing-apps/windows-forms/power-packs-controls.md)