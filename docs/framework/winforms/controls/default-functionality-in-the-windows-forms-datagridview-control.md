---
title: "Funzionalit&#224; predefinite nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "griglie dei dati, funzionalità predefinite nel controllo DataGridView"
  - "DataGridView (controllo) [Windows Form], funzionalità predefinite"
ms.assetid: 4405f697-cad1-4839-9bcd-8ddb09d9f00e
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Funzionalit&#224; predefinite nel controllo DataGridView Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> Windows Form fornisce agli utenti numerose funzionalità predefinite.  
  
## Funzionalità predefinite  
 Per impostazione predefinita, un controllo <xref:System.Windows.Forms.DataGridView>:  
  
-   Visualizza automaticamente le intestazioni di colonna e di riga che restano visibili anche quando la tabella viene fatta scorrere verticalmente.  
  
-   Dispone di un'intestazione di riga contenente un indicatore di selezione per la riga corrente.  
  
-   Dispone di una rettangolo di selezione nella prima cella.  
  
-   Contiene alcune colonne che possono essere ridimensionate automaticamente facendo doppio clic sui divisori di colonna.  
  
-   Supporta automaticamente gli stili visivi in Windows XP e nei sistemi della famiglia di prodotti Windows Server 2003 quando il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> viene chiamato dal metodo `Main` dell'applicazione.  
  
 Inoltre, per impostazione predefinita il contenuto di un controllo <xref:System.Windows.Forms.DataGridView> può essere modificato:  
  
-   Se l'utente fa doppio clic o preme F2 in una cella, il controllo imposta automaticamente la cella in modalità di modifica e aggiorna il contenuto della cella durante la digitazione dell'utente.  
  
-   Se si scorre la griglia fino in fondo, sarà possibile notare che è presente una riga per l'aggiunta di nuovi record.  Quando l'utente fa clic su questa riga, viene aggiunta una nuova riga al controllo <xref:System.Windows.Forms.DataGridView>, con i valori predefiniti.  Quando si preme ESC, la nuova riga viene rimossa.  
  
-   Se l'utente fa clic su un'intestazione di riga, l'intera riga verrà selezionata.  
  
 Quando si associa un controllo <xref:System.Windows.Forms.DataGridView> a un'origine dati impostando la corrispondente proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A>, il controllo:  
  
-   Utilizza automaticamente i nomi delle colonne dell'origine dati come testo dell'intestazione di colonna.  
  
-   Viene popolato con il contenuto dell'origine dati.  Le colonne <xref:System.Windows.Forms.DataGridView> vengono create automaticamente per ciascuna colonna nell'origine dati.  
  
-   Crea una riga per ciascuna riga visibile nella tabella.  
  
-   Ordina automaticamente le righe in base ai dati sottostanti quando l'utente fa clic su un'intestazione di colonna.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)