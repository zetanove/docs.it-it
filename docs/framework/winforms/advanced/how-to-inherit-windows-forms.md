---
title: "Procedura: ereditare Windows Form | Microsoft Docs"
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
  - "ereditarietà, form"
  - "form ereditati, creazione in fase di esecuzione"
  - "Windows Form, ereditarietà"
ms.assetid: cb3e1c0f-3d2a-4cdc-b0d1-c92eae567ffb
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ereditare Windows Form
La creazione di nuovi Windows Form mediante l'ereditarietà da form di base è un modo semplice di duplicare ciò che è stato creato senza ripetere ogni volta il medesimo processo di creazione di un form.  
  
 Per altre informazioni sull'ereditarietà di form in fase di progettazione tramite la finestra di dialogo **Selezione ereditarietà** e su come distinguere visivamente i livelli di sicurezza dei controlli ereditati, vedere [Procedura: Ereditare form mediante la finestra di dialogo Selezione ereditarietà](../../../../docs/framework/winforms/advanced/how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md).  
  
 **Nota**: per ereditare da un form, il file o lo spazio dei nomi contenente tale form deve essere incorporato in un file eseguibile o DLL.  Per compilare il progetto, scegliere **Compila** dal menu **Compila**.  È necessario aggiungere un riferimento allo spazio dei nomi anche alla classe che eredita il form.  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per ereditare un form a livello di codice  
  
1.  All'interno della classe aggiungere un riferimento allo spazio dei nomi che contiene il form da cui si vuole ereditare.  
  
2.  Nella definizione della classe aggiungere un riferimento al form da cui ereditare.  Il riferimento deve includere lo spazio dei nomi che contiene il form, seguito da un punto, quindi il nome del form di base.  
  
    ```vb  
    Public Class Form2  
        Inherits Namespace1.Form1  
  
    ```  
  
    ```csharp  
    public class Form2 : Namespace1.Form1  
  
    ```  
  
 Quando si ereditano i form, tenere presente che possono insorgere problemi relativi alla doppia chiamata a gestori eventi, perché ogni evento viene gestito sia dalla classe di base che dalla classe ereditata.  Per informazioni su come evitare questo problema, vedere [Risoluzione dei problemi relativi ai gestori eventi ereditati in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md).  
  
## Vedere anche  
 [Inherits Statement](../../../../ocs/visual-basic/language-reference/statements/inherits-statement.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../../ocs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [utilizzo](../Topic/using%20\(C%23%20Reference\).md)   
 [Effetti della modifica dell'aspetto di un form di base](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)   
 [Ereditarietà visiva di Windows Form](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)