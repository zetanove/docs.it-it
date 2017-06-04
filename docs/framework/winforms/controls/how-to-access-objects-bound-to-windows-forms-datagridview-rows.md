---
title: "Procedura: accedere a oggetti associati a righe DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, accesso a oggetti associati"
  - "DataGridView (controllo) [Windows Form], accesso ad oggetti associati a righe"
  - "associazione oggetto, accesso a oggetti associati"
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: accedere a oggetti associati a righe DataGridView di Windows Form
A volte è utile visualizzare una tabella di informazioni archiviate in una raccolta di oggetti business.  Quando si associa un controllo <xref:System.Windows.Forms.DataGridView> a una raccolta di questo tipo, ogni proprietà pubblica viene visualizzata nella rispettiva colonna, a meno che la proprietà non sia stata contrassegnata come non visualizzabile con <xref:System.ComponentModel.BrowsableAttribute>.  Ad esempio, una raccolta di oggetti `Customer` avrebbe colonne come **Nome** e **Indirizzo**.  
  
 Se questi oggetti contengono informazioni aggiuntive e codice a cui si desidera accedere, è possibile raggiungerli tramite gli oggetti riga.  Nell'esempio di codice riportato di seguito, gli utenti possono selezionare più righe e fare clic su un pulsante per inviare una fattura a ogni cliente corrispondente.  
  
### Per accedere agli oggetti associati a righe  
  
-   Usare la proprietà <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## Esempio  
 L'esempio di codice completo include una semplice implementazione `Customer` e associa <xref:System.Windows.Forms.DataGridView> a un oggetto <xref:System.Collections.ArrayList> contenente alcuni oggetti `Customer`.  Il gestore dell'evento <xref:System.Windows.Forms.Control.Click> di <xref:System.Windows.Forms.Button?displayProperty=fullName> deve accedere agli oggetti `Customer` tramite le righe, perché la raccolta di clienti non è accessibile al di fuori del gestore dell'evento <xref:System.Windows.Forms.Form.Load?displayProperty=fullName>.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewRow>   
 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: associare oggetti ai controlli DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-objects-to-windows-forms-datagridview-controls.md)