---
title: "Cenni preliminari sul componente OpenFileDialog (Windows Form) | Microsoft Docs"
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
  - "OpenFileDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Apri file (finestra di dialogo), visualizzazione in Windows Form"
  - "OpenFileDialog (componente), informazioni"
ms.assetid: cd717300-46b6-4f82-8207-b218fa7fa407
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul componente OpenFileDialog (Windows Form)
Il componente <xref:System.Windows.Forms.OpenFileDialog> di Windows Form è una finestra di dialogo preconfigurata.  È la stessa finestra di apertura file esposta dal sistema operativo Windows  ed eredita dalla classe <xref:System.Windows.Forms.CommonDialog>.  
  
## Utilizzo del componente  
 Utilizzare questo componente nell'applicazione Windows creata come semplice soluzione per la selezione di file, anziché configurare una propria finestra di dialogo.  Basandosi sulle finestre di dialogo standard di Windows è quindi possibile creare applicazioni le cui funzionalità di base sono immediatamente familiari agli utenti.  Quando si utilizza il componente <xref:System.Windows.Forms.OpenFileDialog>, è necessario scrivere una propria logica per l'apertura del file.  
  
 Utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo in fase di esecuzione.  È possibile consentire agli utenti di selezionare più file da aprire con la proprietà <xref:System.Windows.Forms.OpenFileDialog.Multiselect%2A>.  È inoltre possibile utilizzare la proprietà <xref:System.Windows.Forms.OpenFileDialog.ShowReadOnly%2A> per determinare se una casella di controllo di sola lettura debba essere visualizzata nella finestra di dialogo.  La proprietà <xref:System.Windows.Forms.OpenFileDialog.ReadOnlyChecked%2A> indica se è selezionata la casella di controllo di sola lettura.  Infine la proprietà <xref:System.Windows.Forms.FileDialog.Filter%2A> imposta la stringa di filtro del nome file corrente che determina le scelte visualizzate nella casella "Tipo file" della finestra di dialogo.  
  
 Quando viene aggiunto a un form, il componente <xref:System.Windows.Forms.OpenFileDialog> è visualizzato nella barra delle applicazioni nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.OpenFileDialog>   
 [Componente OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md)