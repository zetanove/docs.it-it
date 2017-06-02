---
title: "Considerazioni sull&#39;inserimento di controlli ActiveX in Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli ActiveX [Windows Form], aggiunta"
  - "controlli ActiveX [Windows Form], hosting"
  - "controlli Windows Form, controlli ActiveX"
  - "Windows Form, controlli ActiveX"
  - "Windows Form, hosting di controlli ActiveX"
ms.assetid: 2509302d-a74e-484f-9890-2acdbfa67a68
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Considerazioni sull&#39;inserimento di controlli ActiveX in Windows Form
Sebbene i Windows Form siano stati ottimizzati per contenere i controlli Windows Form, è comunque possibile utilizzare controlli ActiveX.  Di seguito sono elencati alcuni elementi di cui tenere conto durante la pianificazione di un'applicazione che utilizzi i controlli ActiveX:  
  
-   **Sicurezza** In Common Language Runtime le funzionalità di sicurezza dall'accesso di codice sono state potenziate.  Le applicazioni che utilizzano Windows Form possono essere eseguite in un ambiente completamente attendibile senza alcun problema e in un ambiente parzialmente attendibile con la possibilità di accedere alla maggior parte delle funzionalità.  I controlli dei Windows Form inoltre possono essere facilmente memorizzati in un browser.  Con i controlli ActiveX dei Windows Form tuttavia non è possibile sfruttare i miglioramenti della sicurezza.  L'esecuzione di un controllo ActiveX richiede l'autorizzazione per il codice non gestito. Tale autorizzazione viene impostata tramite la proprietà <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A?displayProperty=fullName>.  Per ulteriori informazioni sulla sicurezza e sull'autorizzazione per il codice non gestito, vedere la [classe SecurityPermissionAttribute](frlrfSystemSecurityPermissionsSecurityPermissionAttributeClassTopic).  
  
-   **Costo di proprietà complessivo \(TCO, Total Cost of Ownership\)**  Eventuali controlli ActiveX aggiunti a Windows Form vengono distribuiti per intero con lo specifico Windows Form, il che può comportare un significativo aumento delle dimensioni dei file creati.  Per consentire l'uso dei controlli ActiveX nei Windows Form, inoltre, è necessaria una scrittura sul Registro di sistema.  Per questa ragione i controlli ActiveX si rivelano particolarmente invasivi per i computer degli utenti rispetto ai controlli dei Windows Form, per i quali tale operazione non viene richiesta.  
  
    > [!NOTE]
    >  L'utilizzo di un controllo ActiveX richiede l'utilizzo di un wrapper di interoperabilità COM.  Per ulteriori informazioni, vedere [Interoperabilità COM in Visual Basic e in Visual C\#](../Topic/COM%20Interoperability%20in%20.NET%20Framework%20Applications%20\(Visual%20Basic\).md).  
  
    > [!NOTE]
    >  Se il nome di un membro del controllo ActiveX corrisponde a un nome definito in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], l'utilità di importazione di controlli ActiveX aggiunge al nome del membro il prefisso **Ctl** quando crea la classe derivata da <xref:System.Windows.Forms.AxHost>.  Se ad esempio il controllo ActiveX presenta un membro denominato **Layout**, tale membro viene rinominato **CtlLayout** nella classe derivata da AxHost poiché l'evento **Layout** è definito in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
## Vedere anche  
 [Procedura: aggiungere i controlli ActiveX a Windows Form](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md)   
 [Code Access Security](../../../../docs/framework/misc/code-access-security.md)   
 [Controls and Programmable Objects Compared in Various Languages and Libraries](http://msdn.microsoft.com/it-it/021f2a1b-8247-4348-a5ad-e1d9ab23004b)   
 [Inserimento di controlli in Windows Form](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)   
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)