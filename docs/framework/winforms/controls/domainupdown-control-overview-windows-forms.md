---
title: "Cenni preliminari sul controllo DomainUpDown (Windows Form) | Microsoft Docs"
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
  - "DomainUpDown"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DomainUpDown (controllo) [Windows Form], informazioni sul controllo DomainUpDown"
  - "controllo pulsante di selezione, informazioni"
ms.assetid: 3f40f9c1-20ad-4331-b9b5-b0127eb36eb3
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo DomainUpDown (Windows Form)
Il controllo <xref:System.Windows.Forms.DomainUpDown> Windows Form si presenta essenzialmente come una casella di testo abbinata a una coppia di frecce per lo spostamento verso l'alto o verso il basso in un elenco.  Nel controllo viene visualizzata e impostata una stringa di testo da un elenco di scelte.  L'utente può selezionare la stringa facendo clic sui pulsanti di scorrimento verso l'alto e verso il basso per spostarsi all'interno dell'elenco, premendo i tasti FRECCIA SU e FRECCIA GIÙ oppure digitando una stringa che corrisponda a una voce dell'elenco.  Un possibile utilizzo di tale controllo è la selezione di voci da un elenco di nomi in ordine alfabetico.  
  
> [!NOTE]
>  Per ordinare l'elenco, impostare la proprietà <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> su `true`.  
  
 La funzione di questo controllo è molto simile a quella di una casella di riepilogo o di una casella combinata, ma occupa uno spazio minimo.  
  
## Proprietà principali  
 Le proprietà principali del controllo sono <xref:System.Windows.Forms.DomainUpDown.Items%2A>, <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> e <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>.  La proprietà <xref:System.Windows.Forms.DomainUpDown.Items%2A> contiene l'elenco di oggetti i cui valori di testo sono visualizzati nel controllo.  Se <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> è impostata su `false`, il controllo completa automaticamente il testo digitato dall'utente e lo fa corrispondere a un valore nell'elenco.  Se <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> è impostata su `true`, scorrendo oltre l'ultima voce si tornerà alla prima voce dell'elenco e viceversa.  I metodi principali del controllo sono <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> e <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>.  
  
 Questo controllo visualizza solo stringhe di testo.  Se si desidera un controllo che visualizzi valori numerici, utilizzare il controllo <xref:System.Windows.Forms.NumericUpDown>.  Per ulteriori informazioni, vedere [Cenni preliminari sul controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DomainUpDown>   
 [Controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)