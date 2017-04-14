---
title: "Procedura: eseguire un&#39;operazione in background | Microsoft Docs"
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
  - "operazioni in background"
  - "attività in background"
  - "thread in background"
  - "BackgroundWorker (classe), esempi"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
ms.assetid: 5b56e2aa-dc05-444f-930c-2d7b23f9ad5b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: eseguire un&#39;operazione in background
Se l'esecuzione di un'operazione richiede molto tempo e si vogliono evitare ritardi nella risposta dell'interfaccia utente, è possibile usare la classe <xref:System.ComponentModel.BackgroundWorker> per eseguire l'operazione in un altro thread.  
  
 L'esempio di codice seguente illustra come eseguire in background un'operazione che richiede molto tempo.  Nel form sono presenti i pulsanti **Start** e **Cancel**.  Fare clic sul pulsante **Start** per eseguire un'operazione asincrona.   Fare clic sul pulsante **Cancel** per interrompere l'esecuzione dell'operazione asincrona.  Il risultato di ciascuna operazione viene visualizzato in una finestra di messaggio <xref:System.Windows.Forms.MessageBox>.  
  
 In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] è disponibile supporto completo per questa attività.  
  
 Vedere anche [Procedura dettagliata: Esecuzione di un'operazione in background](http://msdn.microsoft.com/library/ms233672%20\(v=vs.110\)).  
  
## Esempio  
 [!code-csharp[System.ComponentModel.BackgroundWorker.Example#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.BackgroundWorker.Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>   
 <xref:System.ComponentModel.DoWorkEventArgs>   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component.md)