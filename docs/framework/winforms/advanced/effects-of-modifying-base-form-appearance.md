---
title: "Effetti della modifica dell&#39;aspetto di un form di base | Microsoft Docs"
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
  - "form di base"
  - "ereditarietà, form"
  - "form ereditati, modifiche al form di base"
  - "form padre"
  - "Windows Form, aspetto del form di base"
ms.assetid: 1c3f2b29-a05c-4c6f-aa1a-4e66b94f343a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Effetti della modifica dell&#39;aspetto di un form di base
Durante lo sviluppo dell'applicazione si rende spesso necessario modificare l'aspetto del form di base da cui  ereditano altri form nello stesso progetto o in altri progetti.  
  
 In fase di progettazione le modifiche all'aspetto del form di base, sia per quanto riguarda l'impostazione di proprietà che l'aggiunta o l'eliminazione di controlli, vengono applicate ai form ereditati quando viene compilato il progetto contente il form di base.  Il semplice salvataggio delle modifiche nel form di base non è sufficiente.  Per compilare un progetto, scegliere **Compila** dal menu **Compila**.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Le modifiche apportate al form di base in fase di esecuzione non hanno alcun effetto sui form ereditati di cui esiste già un'istanza.  
  
## Vedere anche  
 [base](../Topic/base%20\(C%23%20Reference\).md)   
 [Procedura: ereditare Windows Form](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)   
 [Ereditarietà visiva di Windows Form](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)