---
title: "Aggiunta di informazioni per l&#39;Accesso facilitato ai controlli in un Windows Form | Microsoft Docs"
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
  - "controlli Windows Form, accessibilità"
  - "controlli [Windows Form], accessibilità"
  - "accessibilità, controlli Windows Form"
ms.assetid: 887dee6f-5059-4d57-957d-7c6fcd4acb10
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Aggiunta di informazioni per l&#39;Accesso facilitato ai controlli in un Windows Form
Gli strumenti per l'accessibilità sono dispositivi e programmi specializzati che consentono agli utenti con disabilità di usare i computer in modo più efficace. Sono incluse, ad esempio, le utilità per la lettura dello schermo per gli utenti non vedenti e le utilità di input vocale per le persone che usano i comandi vocali anziché il mouse o la tastiera. Gli strumenti per l'accessibilità interagiscono con le proprietà di accessibilità esposte dai controlli Windows Form. Le proprietà sono riportate di seguito:  
  
-   **AccessibilityObject**  
  
-   **AccessibleDefaultActionDescription**  
  
-   **AccessibleDescription**  
  
-   **AccessibleName**  
  
-   **AccessibleRole**  
  
## Proprietà AccessibilityObject  
 Questa proprietà di sola lettura contiene un'istanza della [classe AccessibleObject](frlrfSystemWindowsFormsAccessibleObjectClassTopic).**AccessibleObject** implementa l'interfaccia <xref:Accessibility.IAccessible>, che fornisce informazioni sulla descrizione del controllo, la posizione sullo schermo, le capacità di spostamento e il valore. La finestra di progettazione imposta questo valore quando il controllo viene aggiunto al form.  
  
## Proprietà AccessibleDefaultActionDescription  
 Questa stringa descrive l'azione del controllo. Non è visualizzata nella finestra Proprietà e può essere impostata solo nel codice. L'esempio seguente mostra come impostare questa proprietà per un pulsante:  
  
```  
' Visual Basic  
Button1.AccessibleDefaultActionDescription = _  
   "Closes the application."  
  
// C#  
Button1.AccessibleDefaultActionDescription =   
   "Closes the application.";  
  
// C++  
button1->AccessibleDefaultActionDescription =  
   "Closes the application.";  
```  
  
## Proprietà AccessibleDescription  
 Questa stringa descrive il controllo. Può essere impostata nella finestra Proprietà o nel codice, come illustrato di seguito:  
  
```  
' Visual Basic  
Button1.AccessibleDescription = "A button with text 'Exit'."  
  
// C#  
Button1.AccessibleDescription = "A button with text 'Exit'";  
  
// C++  
button1->AccessibleDescription = "A button with text 'Exit'";  
```  
  
## Proprietà AccessibleName  
 Questa stringa rappresenta il nome di un controllo segnalato agli strumenti di accessibilità. Può essere impostata nella finestra Proprietà o nel codice, come illustrato di seguito:  
  
```  
' Visual Basic  
Button1.AccessibleName = "Order"  
  
// C#  
Button1.AccessibleName = "Order";  
  
// C++  
button1->AccessibleName = "Order";  
```  
  
## Proprietà AccessibleRole  
 Questa proprietà, che contiene una [enumerazione AccessibleRole](frlrfSystemWindowsFormsAccessibleRoleClassTopic) descrive il ruolo di interfaccia utente del controllo. Per un nuovo controllo il valore è impostato su `Default`. Ciò significa che, per impostazione predefinita, un controllo **Button** si comporta come un **pulsante**. È consigliabile reimpostare questa proprietà se il controllo ha un altro ruolo. Se, ad esempio, si usa un controllo **PictureBox** come un **grafico**, è possibile fare in modo che il ruolo venga segnalato come **Chart** anziché come **PictureBox**. È anche consigliabile specificare questa proprietà per eventuali controlli personalizzati sviluppati. La proprietà può essere impostata nella finestra Proprietà o nel codice, come illustrato di seguito:  
  
```  
' Visual Basic  
PictureBox1.AccessibleRole = AccessibleRole.Chart  
  
// C#  
PictureBox1.AccessibleRole = AccessibleRole.Chart;  
  
// C++  
pictureBox1->AccessibleRole = AccessibleRole::Chart;  
```  
  
## Vedere anche  
 <xref:System.Windows.Forms.AccessibleObject>   
 <xref:System.Windows.Forms.Control.AccessibilityObject%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.AccessibleDefaultActionDescription%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.AccessibleDescription%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.AccessibleName%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.AccessibleRole%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.AccessibleRole>