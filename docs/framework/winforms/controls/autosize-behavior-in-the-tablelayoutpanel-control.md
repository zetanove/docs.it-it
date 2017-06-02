---
title: "Comportamento di AutoSize nel controllo TableLayoutPanel | Microsoft Docs"
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
  - "ridimensionamento automatico"
  - "AutoSize (proprietà), TableLayoutPanel (controllo)"
  - "AutoSizeMode (proprietà)"
  - "controlli [Windows Form], ridimensionamento"
  - "layout [Windows Form], AutoSize"
  - "localizzazione di form"
  - "ridimensionamento, automatico"
  - "TableLayoutPanel (controllo) [Windows Form], AutoSize (comportamento)"
ms.assetid: 9233e0c3-2fa6-405e-8701-959479b1250e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Comportamento di AutoSize nel controllo TableLayoutPanel
## Diversi comportamenti di AutoSize  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> supporta il ridimensionamento automatico nei modi seguenti:  
  
-   Mediante la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.  
  
-   Mediante la proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> degli stili di riga e di colonna del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
### La proprietà AutoSize con stili di riga e colonna  
 Nella tabella riportata di seguito viene descritta l'interazione tra la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> e gli stili di colonna e riga del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
|Impostazione di AutoSize|Interazione con lo stile|  
|------------------------------|------------------------------|  
|`false`|Il controllo <xref:System.Windows.Forms.TableLayoutPanel> alloca spazio alla colonna o alla riga da sinistra a destra come descritto di seguito.<br /><br /> 1.  Se la proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> è impostata su <xref:System.Windows.Forms.SizeType>, verrà allocato il numero di pixel specificato da <xref:System.Windows.Forms.ColumnStyle.Width%2A> o <xref:System.Windows.Forms.RowStyle.Height%2A>.<br />2.  Se la proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> è impostata su <xref:System.Windows.Forms.SizeType>, verrà allocato il numero di pixel restituito dal metodo <xref:System.Windows.Forms.Control.GetPreferredSize%2A> del controllo figlio.<br />3.  Una volta allocato lo spazio per tutte le colonne o righe <xref:System.Windows.Forms.SizeType> e <xref:System.Windows.Forms.SizeType>, le eventuali colonne o righe con la proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> impostata su <xref:System.Windows.Forms.SizeType> verranno utilizzate per allocare in proporzione lo spazio libero rimanente.|  
|`true`|Simile all'interazione precedente, tranne per il fatto che le colonne o le righe con stile <xref:System.Windows.Forms.SizeType> vengono ridimensionate automaticamente.<br /><br /> Il controllo <xref:System.Windows.Forms.TableLayoutPanel> espande la colonna o la riga per creare lo spazio libero necessario a non troncare il contenuto delle colonne o righe con stile <xref:System.Windows.Forms.SizeType>.  Il controllo <xref:System.Windows.Forms.TableLayoutPanel> alloca il nuovo spazio proporzionalmente, in base alla proprietà <xref:System.Windows.Forms.ColumnStyle.Width%2A> o <xref:System.Windows.Forms.RowStyle.Height%2A>.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [Cenni preliminari sul controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-overview.md)