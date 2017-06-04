---
title: "Cenni preliminari sul controllo NumericUpDown (Windows Form) | Microsoft Docs"
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
  - "NumericUpDown"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controllo pulsante di selezione numerico, Windows Form"
  - "NumericUpDown (controllo) [Windows Form], informazioni sul controllo NumericUpDown"
  - "controllo pulsante di selezione, Windows Form"
ms.assetid: cff3cf30-4d46-4381-87df-37bfe83c71c5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul controllo NumericUpDown (Windows Form)
Il controllo <xref:System.Windows.Forms.NumericUpDown> ha l'aspetto di una casella di testo abbinata a una coppia di frecce che l'utente può utilizzare per modificare un valore.  Nel controllo viene visualizzato e impostato un singolo valore numerico da un elenco di scelte di valori numerici fissi.  L'utente può aumentare e diminuire il valore del numero facendo clic sulle frecce su e giù, premendo i tasti FRECCIA SU e FRECCIA GIÙ oppure digitando un numero nella parte della casella di testo del controllo.  Se si utilizzano i tasti FRECCIA SU o FRECCIA GIÙ, si sposta il numero verso il valore massimo o minimo.  
  
 Grazie alla sua versatilità questo controllo è una scelta ovvia, ad esempio, se si desidera creare un controllo del volume per l'applicazione di un riproduttore musicale.  Il controllo <xref:System.Windows.Forms.NumericUpDown> viene usato in molte applicazioni del Pannello di controllo di Windows.  
  
## Proprietà e metodi principali  
 I numeri nella casella di testo del controllo possono essere visualizzati in formati diversi, compreso nel formato esadecimale.  Per ulteriori informazioni, vedere [Procedura: impostare il formato per il controllo NumericUpDown Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-format-for-the-windows-forms-numericupdown-control.md).  Le proprietà principali del controllo sono <xref:System.Windows.Forms.NumericUpDown.Value%2A>, <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> \(valore predefinito: 100\), <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> \(valore predefinito: 0\) e <xref:System.Windows.Forms.NumericUpDown.Increment%2A> \(valore predefinito: 1\).  La proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A> consente di impostare il numero corrente selezionato nel controllo.  La proprietà <xref:System.Windows.Forms.NumericUpDown.Increment%2A> consente di impostare la quantità in base alla quale il numero viene modificato quando l'utente seleziona una delle frecce.  Quando il controllo non è attivo, qualsiasi valore immesso viene convalidato in base ai valori numerici massimo e minimo.  È possibile aumentare la velocità a cui il controllo si sposta tra i numeri, quando l'utente preme continuamente la freccia su o giù, con la proprietà <xref:System.Windows.Forms.NumericUpDown.Accelerations%2A>.  I metodi principali del controllo sono <xref:System.Windows.Forms.NumericUpDown.UpButton%2A> e <xref:System.Windows.Forms.NumericUpDown.DownButton%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.NumericUpDown>   
 [Controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)   
 [Procedura: impostare il formato per il controllo NumericUpDown Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-format-for-the-windows-forms-numericupdown-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)