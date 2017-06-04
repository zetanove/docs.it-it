---
title: "Windows Forms Security | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "designer access security"
  - "permissions, Windows Forms"
  - "Windows Forms, security"
  - "security [Windows Forms]"
  - "access control, Windows Forms"
  - "security policy, Windows Forms"
ms.assetid: 932d438a-5285-46d8-a958-8c93d0ad6cae
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Windows Forms Security
I Windows Form dispongono di un modello di sicurezza basato sul codice, in cui i livelli di sicurezza vengono impostati per il codice, indipendentemente dall'utente che esegue il codice.  Questo modello si aggiunge agli schemi di sicurezza eventualmente già presenti nel sistema informatico,  tra cui gli schemi nel browser, ad esempio la sicurezza basata sull'area in Internet Explorer, o nel sistema operativo, ad esempio la sicurezza basata su credenziali di Windows NT.  
  
## In questa sezione  
 [Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md)  
 Viene illustrato brevemente il modello di sicurezza di .NET Framework e i passaggi di base necessari per assicurare che i Windows Form nell'applicazione siano protetti.  
  
 [More Secure File and Data Access in Windows Forms](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)  
 Viene descritto come accedere a file e dati in un ambiente parzialmente attendibile.  
  
 [More Secure Printing in Windows Forms](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)  
 Viene descritto come accedere alle funzionalità di stampa in un ambiente parzialmente attendibile.  
  
 [Additional Security Considerations in Windows Forms](../../../docs/framework/winforms/additional-security-considerations-in-windows-forms.md)  
 Viene descritto come modificare le finestre, mediante gli Appunti, ed eseguire chiamate al codice non gestito in un ambiente parzialmente attendibile.  
  
## Sezioni correlate  
 [NIB: Default Security Policy](http://msdn.microsoft.com/it-it/2c086873-0894-4f4d-8f7e-47427c1a3b55)  
 Vengono elencate le autorizzazioni predefinite concesse negli insiemi di autorizzazioni Attendibilità totale, Intranet locale e Internet.  
  
 [NIB: General Security Policy Administration](http://msdn.microsoft.com/it-it/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)  
 Vengono fornite informazioni sull'amministrazione dei criteri di sicurezza di .NET Framework e sull'elevazione delle autorizzazioni.  
  
 [Dangerous Permissions and Policy Administration](../../../docs/framework/misc/dangerous-permissions-and-policy-administration.md)  
 Vengono illustrate alcune autorizzazioni di .NET Framework che potenzialmente possono provocare il superamento del sistema di sicurezza.  
  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)  
 Vengono forniti collegamenti ad argomenti che spiegano i modi ottimali per scrivere codice in modo sicuro in .NET Framework.  
  
 [NIB: Requesting Permissions](http://msdn.microsoft.com/it-it/0447c49d-8cba-45e4-862c-ff0b59bebdc2)  
 Viene descritto l'utilizzo degli attributi per segnalare al runtime quali autorizzazioni è necessario eseguire per il codice.  
  
 [Key Security Concepts](../../../docs/standard/security/key-security-concepts.md)  
 Vengono forniti collegamenti ad argomenti che trattano gli aspetti base della sicurezza del codice.  
  
 [Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md)  
 Vengono trattate le nozioni fondamentali dell'utilizzo dei criteri di sicurezza del runtime di .NET Framework.  
  
 [NIB: Determining When to Modify Security Policy](http://msdn.microsoft.com/it-it/af749b17-e461-409d-84b9-a3d44789db16)  
 Viene spiegato come determinare quando è opportuno differenziare le applicazioni dal criterio di sicurezza predefinito.  
  
 [NIB: Deploying Security Policy](http://msdn.microsoft.com/it-it/f936c1e5-033b-4bd9-a3bd-a39ba733a681)  
 Viene descritto il metodo migliore per distribuire le modifiche dei criteri di sicurezza.