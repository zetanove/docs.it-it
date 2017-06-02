---
title: "Procedura: personalizzare l&#39;ordinamento nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, ordinamento personalizzato"
  - "DataGridView (controllo) [Windows Form], ordinamento"
  - "ordinamento, DataGridView (controllo)"
ms.assetid: 92fb5c14-afab-4cf5-a97e-924fd9cb99f5
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: personalizzare l&#39;ordinamento nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> fornisce l'ordinamento automatico, tuttavia le operazioni di ordinamento possono essere personalizzate secondo le proprie esigenze.  Ad esempio, è possibile usare l'ordinamento a livello di codice per creare un'interfaccia utente alternativa.  È anche possibile gestire l'evento <xref:System.Windows.Forms.DataGridView.SortCompare> o chiamare l'overload `Sort(IComparer)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A> per una maggiore flessibilità, ad esempio per l'ordinamento di più colonne.  
  
 Gli esempi di codice seguenti illustrano questi tre approcci all'ordinamento personalizzato.  Per altre informazioni, vedere [Modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md).  
  
## Ordinamento a livello di codice  
 L'esempio di codice seguente illustra un ordinamento a livello di codice che usa le proprietà <xref:System.Windows.Forms.DataGridView.SortOrder%2A> e <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> per determinare la direzione dell'ordinamento e la proprietà <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A> per impostare manualmente il glifo di ordinamento.  L'overload `Sort(DataGridViewColumn,ListSortDirection)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A> viene usato per ordinare i dati solo in una singola colonna.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewProgrammaticSort#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewProgrammaticSort/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewProgrammaticSort#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewProgrammaticSort/VB/form1.vb#00)]  
  
## Ordinamento personalizzato tramite l'evento SortCompare  
 L'esempio di codice seguente illustra un ordinamento personalizzato tramite un gestore dell'evento <xref:System.Windows.Forms.DataGridView.SortCompare>.  L'oggetto <xref:System.Windows.Forms.DataGridViewColumn> selezionato viene ordinato e, se esistono valori duplicati nella colonna, per determinare l'ordine finale viene usata la colonna ID.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.SortCompare#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.SortCompare/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridView.SortCompare#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.SortCompare/VB/form1.vb#00)]  
  
## Ordinamento personalizzato tramite l'interfaccia IComparer  
 L'esempio di codice seguente illustra  l'ordinamento personalizzato tramite l'overload `Sort(IComparer)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A>, che usa un'implementazione dell'interfaccia <xref:System.Collections.IComparer> per eseguire un ordinamento di più colonne.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewIComparerSort#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewIComparerSort/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewIComparerSort#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewIComparerSort/VB/form1.vb#00)]  
  
## Compilazione del codice  
 Gli esempi presentano i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questi esempi dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Ordinamento dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)   
 [Modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare le modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/set-the-sort-modes-for-columns-wf-datagridview-control.md)