---
title: "Cenni preliminari sul componente HelpProvider (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "HelpProvider"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "finestre di dialogo, Guida sensibile al contesto"
  - "F1 (Guida), aggiunta a Windows Form"
  - "Guida, aggiunta alle applicazioni Windows"
  - "HelpProvider (componente) [Windows Form], informazioni sul componente HelpProvider"
  - "Windows Form, Guida sensibile al contesto"
ms.assetid: 6b10c2cc-c577-4cb5-9669-e37b33416af9
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Cenni preliminari sul componente HelpProvider (Windows Form)
Il componente Windows Form [HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md) viene utilizzato per associare un file della Guida HTML Help 1.x all'applicazione Windows personalizzata, vale a dire un file CHM creato con HTML Help Workshop o un file HTM.  Le informazioni che è possibile fornire sono di diversi tipi:  
  
-   La Guida sensibile al contesto per i controlli in Windows Form.  
  
-   La Guida sensibile al contesto relativa a una particolare finestra di dialogo o a controlli specifici in una finestra di dialogo.  
  
-   Un file della Guida per aree specifiche, come la pagina principale di un sommario, un indice o una funzione di ricerca.  
  
## Utilizzo del provider della Guida  
 L'aggiunta di un componente <xref:System.Windows.Forms.HelpProvider> al Windows Form consente agli altri controlli del form di esporre le proprietà della Guida del componente <xref:System.Windows.Forms.HelpProvider> consentendo in tal modo di fornire informazioni della Guida per i controlli in Windows Form.  È possibile associare un file della Guida al componente <xref:System.Windows.Forms.HelpProvider> utilizzando la proprietà <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>.  Specificare il tipo di Guida fornito chiamando il metodo <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> e fornendo un valore dall'enumerazione <xref:System.Windows.Forms.HelpNavigator> per il controllo specificato.  Fornire la parola chiave o l'argomento per la Guida chiamando il metodo <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A>.  
  
 È inoltre possibile associare una specifica stringa della Guida a un altro controllo, utilizzando il metodo <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A>.  La stringa associata al controllo con tale metodo verrà visualizzata in una finestra popup quando l'utente preme il tasto F1 mentre il controllo è attivo.  
  
 Se la proprietà <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> non è stata impostata, è necessario utilizzare <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A> per specificare il testo della Guida.  Se si è impostato sia <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> che la stringa della Guida, avranno la precedenza le informazioni della Guida basate su <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>.  
  
> [!NOTE]
>  Si possono verificare problemi di utilizzo del percorso relativo, quando si specifica il percorso per il file della Guida nel metodo <xref:System.Windows.Forms.Help.ShowHelp%2A> o nella proprietà <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> del controllo <xref:System.Windows.Forms.HelpProvider>.  Pertanto accertarsi di utilizzare il percorso assoluto per specificare il file della Guida.  
  
## Vedere anche  
 [Help Systems in Windows Forms Applications](../../../../docs/framework/winforms/advanced/help-systems-in-windows-forms-applications.md)