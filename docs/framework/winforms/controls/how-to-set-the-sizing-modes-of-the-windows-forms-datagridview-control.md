---
title: "Procedura: impostare le modalit&#224; dimensionamento del controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, impostazione delle modalità di ridimensionamento"
  - "DataGridView (controllo) [Windows Form], modalità di ridimensionamento"
ms.assetid: e9ad15e6-b4bb-44aa-a767-3738e9db1651
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: impostare le modalit&#224; dimensionamento del controllo DataGridView di Windows Form
Le seguenti procedure illustrano alcuni scenari comuni in cui vengono personalizzate o combinate le opzioni di ridimensionamento disponibili per il controllo <xref:System.Windows.Forms.DataGridView> e per colonne specifiche di un controllo.  
  
### Per creare una colonna a larghezza fissa  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>, la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> su <xref:System.Windows.Forms.DataGridViewTriState>, la proprietà <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A> su `true` e la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> su un valore appropriato.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#10)]  
  
### Per creare una colonna con le dimensioni che si adattano al contenuto  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> su una modalità di ridimensionamento basata sul contenuto.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#20)]  
  
### Per creare colonne in modalità di riempimento per valori di dimensioni e importanza diverse  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=fullName> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode> per impostare la modalità di ridimensionamento per tutte le colonne che non eseguono l'override di questo valore.  Impostare le proprietà <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> delle colonne su valori proporzionali alla larghezza media del contenuto.  Impostare le proprietà <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> di colonne importanti per garantire la visualizzazione parziale del contenuto.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#30)]  
  
## Esempio  
 L'esempio di codice completo riportato di seguito illustra un'applicazione di prova che permette di comprendere meglio le opzioni di ridimensionamento descritte in questo argomento.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#00)]  
  
 Per usare questa applicazione di esempio:  
  
-   Modificare le dimensioni del form.  Osservare il modo in cui cambia la larghezza delle colonne in modalità di riempimento mantenendo le proporzioni indicate dai valori della proprietà <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>.  Osservare il modo in cui la proprietà <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> di una colonna le impedisce di cambiare quando il form è troppo piccolo.  
  
-   Modificare le dimensioni delle colonne trascinando i separatori di colonna con il mouse.  Osservare il modo in cui alcune colonne non possono essere ridimensionate e il modo in cui le colonne ridimensionabili non possono essere ristrette oltre la larghezza minima.  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A?displayProperty=fullName>