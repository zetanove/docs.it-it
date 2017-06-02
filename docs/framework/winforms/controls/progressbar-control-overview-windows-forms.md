---
title: "Cenni preliminari sul controllo ProgressBar (Windows Form) | Microsoft Docs"
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
  - "ProgressBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "stato (controlli), informazioni sui controllo stato"
  - "ProgressBar (controllo) [Windows Form], informazioni sul controllo ProgressBar"
ms.assetid: a05d9cba-3a6a-4f8f-94b8-8ec12799fb80
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sul controllo ProgressBar (Windows Form)
> [!IMPORTANT]
>  Benché il controllo <xref:System.Windows.Forms.ToolStripProgressBar> sostituisca il controllo <xref:System.Windows.Forms.ProgressBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ProgressBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Il controllo <xref:System.Windows.Forms.ProgressBar> Windows Form indica lo stato di avanzamento di un processo visualizzando un numero appropriato di rettangoli in una barra orizzontale.  Quando l'operazione è stata completata, la barra appare piena.  Gli indicatori di stato sono in genere utilizzati per dare all'utente l'idea del tempo necessario per il completamento di un processo, ad esempio il caricamento di un file di grandi dimensioni.  
  
> [!NOTE]
>  Il controllo <xref:System.Windows.Forms.ProgressBar> può essere orientato solo in orizzontale sul form.  
  
## Proprietà e metodi principali  
 Le proprietà principali del controllo <xref:System.Windows.Forms.ProgressBar> sono <xref:System.Windows.Forms.ProgressBar.Value%2A>, <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A>.  Le proprietà <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A> consentono di impostare i valori massimo e minimo visualizzabili sull'indicatore di stato.  La proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> rappresenta l'avanzamento compiuto verso il completamento dell'operazione.  Poiché la barra visualizzata nel controllo è composta da blocchi, il valore visualizzato dal controllo <xref:System.Windows.Forms.ProgressBar> rappresenta solo un'approssimazione del valore corrente della proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>.  In base alle dimensioni del controllo <xref:System.Windows.Forms.ProgressBar>, la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> determina quando visualizzare il blocco successivo.  
  
 Il metodo più comune per aggiornare il valore corrente dell'avanzamento prevede la creazione di codice per impostare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>.  Nell'esempio del caricamento di un file di grandi dimensioni, si potrebbe impostare il valore massimo sulle dimensioni del file in kilobyte.  Se ad esempio la proprietà <xref:System.Windows.Forms.ProgressBar.Maximum%2A> è impostata su 100, la proprietà <xref:System.Windows.Forms.ProgressBar.Minimum%2A> su 10 e la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> su 50, verranno visualizzati 5 rettangoli,  ovvero la metà del numero di rettangoli visualizzabili.  
  
 Esistono tuttavia altri modi per modificare il valore visualizzato dal controllo <xref:System.Windows.Forms.ProgressBar>, oltre all'impostazione diretta della proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>.  È infatti possibile utilizzare la proprietà <xref:System.Windows.Forms.ProgressBar.Step%2A> per specificare il valore di cui incrementare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>,  quindi incrementare il valore chiamando il metodo <xref:System.Windows.Forms.ProgressBar.PerformStep%2A>.  Per modificare il valore dell'incremento, è possibile utilizzare il metodo <xref:System.Windows.Forms.ProgressBar.Increment%2A> e specificare il valore di cui incrementare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>.  
  
 Un altro controllo che informa graficamente l'utente su un'operazione in corso è il controllo <xref:System.Windows.Forms.StatusBar>.  
  
> [!IMPORTANT]
>  Benché i controlli <xref:System.Windows.Forms.StatusStrip> e <xref:System.Windows.Forms.ToolStripStatusLabel> sostituiscano i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> delle versioni precedenti aggiungendo funzionalità, i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> vengono mantenuti per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ProgressBar>   
 [Controllo ProgressBar](../../../../docs/framework/winforms/controls/progressbar-control-windows-forms.md)