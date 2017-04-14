---
title: "Procedura: condividere dati associati tra form tramite il componente BindingSource | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form], esempi"
  - "BindingSource, utilizzo con più form"
  - "associazione dati, condivisione di dati tra form"
  - "esempi [Windows Form], BindingSource (componente)"
ms.assetid: a1a49630-db9c-4485-b888-1f62a373a4f7
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: condividere dati associati tra form tramite il componente BindingSource
È possibile condividere facilmente i dati tra i form con il componente <xref:System.Windows.Forms.BindingSource>.  Ad esempio, è possibile visualizzare un form di sola lettura che riepiloga i dati dell'origine dati e un altro form modificabile che contiene informazioni dettagliate sull'elemento attualmente selezionato nell'origine dati.  L'esempio illustra questo scenario.  
  
## Esempio  
 L'esempio di codice seguente illustra come condividere un oggetto <xref:System.Windows.Forms.BindingSource> e i dati associati tra i form.  In questo esempio, l'oggetto <xref:System.Windows.Forms.BindingSource> condiviso viene passato al costruttore del form figlio.  Il form figlio consente all'utente di modificare i dati per l'elemento attualmente selezionato nel form principale.  
  
> [!NOTE]
>  Nell'esempio viene gestito l'evento <xref:System.Windows.Forms.BindingSource.BindingComplete> del componente <xref:System.Windows.Forms.BindingSource> per essere certi che i due form rimangano sincronizzati  Per altre informazioni sul motivo per cui questa operazione viene eseguita, vedere [Procedura: garantire la sincronizzazione di più controlli associati alla stessa origine dati](../../../../docs/framework/winforms/multiple-controls-bound-to-data-source-synchronized.md).  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleForms#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleForms#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Windows.Forms, System.Drawing, System.Data e System.Xml.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Procedura: gestire gli errori e le eccezioni che si verificano con l'associazione dati](../../../../docs/framework/winforms/controls/how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)