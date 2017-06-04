---
title: "Controllo DomainUpDown (Windows Form) | Microsoft Docs"
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
  - "DomainUpDown (controllo) [Windows Form]"
  - "controllo pulsante di selezione"
  - "controllo pulsante di selezione, controlli di scorrimento"
  - "controlli di scorrimento"
  - "controlli di scorrimento, controlli pulsante di selezione"
ms.assetid: fb7cf017-e931-4a95-9d21-8caee4ee122a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Controllo DomainUpDown (Windows Form)
Il controllo <xref:System.Windows.Forms.DomainUpDown> di Windows Form ha l'aspetto di una casella di testo abbinata a una coppia di frecce per lo spostamento verso l'alto o verso il basso in un elenco.  Nel controllo viene visualizzata e impostata una stringa di testo da un elenco di scelte.  L'utente può selezionare la stringa facendo clic sui pulsanti di scorrimento verso l'alto e verso il basso per spostarsi all'interno dell'elenco, premendo i tasti FRECCIA SU e FRECCIA GIÙ oppure digitando una stringa che corrisponda a una voce dell'elenco.  Un possibile utilizzo di tale controllo è la selezione di voci da un elenco di nomi in ordine alfabetico.  Per ordinare l'elenco, impostare la proprietà <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> su `true`. La funzione di questo controllo è molto simile a quella di una casella di riepilogo o di una casella combinata, ma occupa uno spazio minimo.  
  
 Le proprietà principali del controllo sono <xref:System.Windows.Forms.DomainUpDown.Items%2A>, <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> e <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>.  La proprietà <xref:System.Windows.Forms.DomainUpDown.Items%2A> contiene l'elenco di oggetti i cui valori di testo sono visualizzati nel controllo.  Se <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> è impostata su `false`, il controllo completa automaticamente il testo digitato dall'utente e lo fa corrispondere a un valore nell'elenco.  Se <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> è impostata su `true`, scorrendo oltre l'ultima voce si tornerà alla prima voce dell'elenco e viceversa.  I metodi principali del controllo sono <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> e <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>.  
  
 Questo controllo visualizza solo stringhe di testo.  Se si desidera un controllo che visualizzi valori numerici, utilizzare il controllo <xref:System.Windows.Forms.NumericUpDown>.  Per ulteriori informazioni, vedere [Controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md).  
  
## In questa sezione  
 [Cenni preliminari sul controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-overview-windows-forms.md)  
 Vengono presentati i concetti generali relativi al controllo <xref:System.Windows.Forms.DomainUpDown>, che consente agli utenti di scorrere un elenco di stringhe di testo ed effettuarvi una selezione.  
  
 [Procedura: aggiungere elementi ai controlli DomainUpDown Windows Form a livello di codice](../../../../docs/framework/winforms/controls/how-to-add-items-to-windows-forms-domainupdown-controls-programmatically.md)  
 Viene descritto come specificare le stringhe di testo che dovranno essere visualizzate dal controllo <xref:System.Windows.Forms.DomainUpDown>.  
  
 [Procedura: rimuovere elementi dai controlli DomainUpDown Windows Form](../../../../docs/framework/winforms/controls/how-to-remove-items-from-windows-forms-domainupdown-controls.md)  
 Viene descritto come eliminare elementi dal controllo <xref:System.Windows.Forms.DomainUpDown> nel codice.  
  
## Riferimenti  
 <xref:System.Windows.Forms.DomainUpDown>  
 Viene descritta la classe e forniti i collegamenti a tutti i relativi membri.  
  
 <xref:System.Windows.Forms.NumericUpDown>  
 Viene descritta la classe e vengono forniti i collegamenti a tutti i relativi membri.  
  
## Sezioni correlate  
 [Controlli utilizzabili in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)  
 Viene fornito un elenco completo dei controlli Windows Form, con l'indicazione dei collegamenti alle informazioni sul relativo utilizzo.