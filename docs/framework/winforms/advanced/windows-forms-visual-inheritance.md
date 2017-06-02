---
title: "Ereditariet&#224; visiva di Windows Form | Microsoft Docs"
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
  - "ereditarietà di form"
  - "ereditarietà"
  - "ereditarietà, form"
  - "form ereditati"
  - "form ereditati, Windows Form"
  - "Windows Form, ereditarietà"
ms.assetid: 857eb737-3602-4d49-bd8b-f70d33ace345
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Ereditariet&#224; visiva di Windows Form
In alcuni casi è possibile impostare un progetto in modo che richiami un form simile a uno creato in precedenza.  In altri casi, invece, può rivelarsi utile creare un form di base con impostazioni quali un elemento di sfondo o il layout di un determinato controllo da utilizzare successivamente all'interno di un progetto, con modifiche al modello del form originale contenute in ogni iterazione.  L'ereditarietà dei form consente di creare un form di base e di ereditare da tale form, quindi di apportare modifiche conservando le impostazioni originali necessarie.  
  
 È possibile creare form che derivano da classi a livello di codice oppure mediante la finestra di selezione dell'ereditarietà visiva.  
  
## In questa sezione  
 [Procedura: ereditare Windows Form](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)  
 Vengono fornite indicazioni per creare nel codice form ereditati.  
  
 [Procedura: ereditare form mediante la finestra di dialogo Selezione ereditarietà](../../../../docs/framework/winforms/advanced/how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md)  
 Vengono fornite indicazioni per creare form ereditati mediante la finestra di selezione dell'ereditarietà.  
  
 [Effetti della modifica dell'aspetto di un form di base](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)  
 Vengono fornite indicazioni per modificare i controlli di un form di base e le relative proprietà.  
  
 [Procedura dettagliata: dimostrazione dell'ereditarietà visiva](../../../../docs/framework/winforms/advanced/walkthrough-demonstrating-visual-inheritance.md)  
 Vengono descritte la creazione di un Windows Form di base e la relativa compilazione in una libreria di classi.  L'utente viene guidato nel processo di importazione di tale libreria di classi in un altro processo e di creazione di un nuovo form che eredita dal form di base.  
  
 [Procedura: utilizzare modificatori e proprietà GenerateMember](../../../../docs/framework/winforms/advanced/how-to-use-the-modifiers-and-generatemember-properties.md)  
 Vengono fornite indicazioni per l'utilizzo delle proprietà `GenerateMember` e `Modifiers`, che sono rilevanti quando in Progettazione Windows Form viene generata una variabile membro per un componente.  
  
## Sezioni correlate  
 [NOT IN BUILD: Inheritance in Visual Basic](http://msdn.microsoft.com/it-it/e5e6e240-ed31-4657-820c-079b7c79313c)  
 Vengono descritte le modalità di definizione delle classi Visual Basic che fungono da base per altre classi.  
  
 [classe](../Topic/class%20\(C%23%20Reference\).md)  
 Viene descritto l'approccio di C\# alle classi in cui è consentita l'ereditarietà singola.  
  
 [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)  
 Vengono elencati problemi comuni relativi ai gestori eventi nei componenti ereditati.