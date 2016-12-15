---
title: "Security and the Registry (Visual Basic) | Microsoft Docs"
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
  - "security [Visual Basic], registry"
  - "registry, security issues"
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Security and the Registry (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento vengono illustrate le implicazioni in termini di sicurezza della memorizzazione dei dati nel Registro di sistema.  
  
## Autorizzazioni  
 Memorizzare come testo nel Registro di sistema informazioni riservate, quali le password, può presentare dei rischi, anche se la chiave del Registro di sistema è protetta da elenchi di controllo di accesso \(ACL, Access Control List\).  
  
 L'utilizzo del Registro di sistema potrebbe comportare problemi di sicurezza, consentendo accesso non appropriato a risorse di sistema o informazioni protette.  Per utilizzare tali proprietà, è necessario disporre di autorizzazioni di lettura e scrittura derivanti dall'enumerazione <xref:System.Security.Permissions.RegistryPermissionAccess>, che controlla l'accesso alle variabili del Registro di sistema.  Qualsiasi codice eseguito con attendibilità completa, che in base ai criteri di sicurezza predefiniti corrisponde al codice installato nel disco rigido locale dell'utente, dispone delle autorizzazioni necessarie per accedere al Registro di sistema.  Per ulteriori informazioni, vedere la classe <xref:System.Security.Permissions.RegistryPermission>.  
  
 Le variabili del Registro di sistema non devono essere memorizzate in posizioni di memoria accessibili da codice senza <xref:System.Security.Permissions.RegistryPermission>.  Analogamente, concedere i privilegi minimi necessari a eseguire il lavoro.  
  
 I valori delle autorizzazioni di accesso al Registro di sistema sono definite dall'enumerazione <xref:System.Security.Permissions.RegistryPermissionAccess>.  Nella tabella riportata di seguito sono illustrati i dettagli dei membri.  
  
|Valore|Accesso alle variabili del Registro di sistema|  
|------------|----------------------------------------------------|  
|`AllAccess`|Creazione, lettura e scrittura|  
|`Create`|Create|  
|`NoAccess`|Nessun accesso|  
|`Read`|Lettura|  
|`Write`|Write|  
  
## Verifica dei valori nelle chiavi del Registro di sistema  
 Quando si crea un valore del Registro di sistema, è necessario decidere come procedere nel caso in cui tale valore esista già.  È possibile che un altro processo, forse dannoso, abbia già creato il valore e possa accedervi.  I dati collocati nel valore del Registro di sistema sono disponibili per altri processi.  Per evitare che ciò accada, utilizzare il metodo `GetValue` che restituisce `Nothing` se la chiave non esiste già.  
  
> [!IMPORTANT]
>  Durante la lettura del Registro di sistema da un'applicazione Web, l'identità dell'utente corrente dipende dall'autenticazione e dalla rappresentazione implementate nell'applicazione Web.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 [Reading from and Writing to the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)