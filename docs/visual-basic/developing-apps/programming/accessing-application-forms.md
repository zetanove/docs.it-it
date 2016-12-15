---
title: "Accessing Application Forms (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "forms, communicating between"
  - "application forms, accessing"
  - "forms, accessing one from another"
  - "My.Forms object"
  - "forms, accessing all open"
ms.assetid: 9aaf5aaf-2012-4f97-89c7-6e62b9d17863
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Accessing Application Forms (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'oggetto `My.Forms` fornisce un modo semplice per l'accesso all'istanza di ciascun Windows Form dichiarato nel progetto dell'applicazione.  È possibile utilizzare le proprietà dell'oggetto `My.Application` per accedere alla schermata iniziale e al form principale e ottenere un elenco dei form aperti dell'applicazione.  
  
## Attività  
 Nella tabella riportata di seguito sono elencati esempi che illustrano le modalità di accesso ai form di un'applicazione.  
  
|||  
|-|-|  
|Per|Vedere|  
|Accedere a un form da un altro form in un'applicazione.|[My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)|  
|Visualizzare i titoli di tutti i form aperti dell'applicazione.|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>|  
|Aggiornare la schermata iniziale con informazioni sullo stato all'avvio dell'applicazione.|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>   
 [My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)