---
title: "Rapid Application Development with My.Resources and My.Settings (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Settings object, developing applications"
  - "rapid application development (RAD), My.Resources"
  - "rapid application development (RAD), My.Settings"
  - "My.Resources object, developing applications"
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Rapid Application Development with My.Resources and My.Settings (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'oggetto `My.Resources` fornisce accesso alle risorse dell'applicazione e consente di recuperarle dinamicamente.  
  
## Recupero risorse  
 Diverse risorse quali file audio, icone, immagini e stringhe possono essere recuperate mediante l'oggetto `My.Resources`.  È possibile accedere, ad esempio, ai file di risorse specifici delle impostazioni cultura dell'applicazione.  Nell'esempio riportato di seguito l'icona del form viene impostata sull'icona denominata `Form1Icon` memorizzata nel file di risorse dell'applicazione.  
  
 [!code-vb[VbVbcnMy#7](../../../visual-basic/developing-apps/development-with-my/codesnippet/visualbasic/rapid-application-develo_1.vb)]  
  
 L'oggetto `My.Resources` espone soltanto risorse globali.  Non consente di accedere ai file di risorse associati ai form.  È necessario accedere alle risorse del form dal form stesso.  Per ulteriori informazioni, vedere [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/it-it/9a96220d-a19b-4de0-9f48-01e5d82679e5).  
  
 Analogamente, l'oggetto `My.Settings` fornisce accesso alle impostazioni dell'applicazione e consente di memorizzare e recuperare dinamicamente le impostazioni delle proprietà e altre informazioni per l'applicazione.  Per ulteriori informazioni, vedere [My.Resources Object](../../../visual-basic/language-reference/objects/my-resources-object.md) e [My.Settings Object](../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
## Vedere anche  
 [My.Resources Object](../../../visual-basic/language-reference/objects/my-resources-object.md)   
 [My.Settings Object](../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [Accessing Application Settings](../../../visual-basic/developing-apps/programming/app-settings/accessing-application-settings.md)