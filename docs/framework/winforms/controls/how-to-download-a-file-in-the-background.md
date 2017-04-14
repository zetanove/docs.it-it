---
title: "Procedura: scaricare file in background | Microsoft Docs"
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
  - "Modello asincrono"
  - "operazioni in background"
  - "attività in background"
  - "BackgroundWorker (componente)"
  - "componenti [Windows Form], asincrono"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
ms.assetid: 9b7bc5ae-051c-4904-9720-18f6667388bd
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: scaricare file in background
Il download di file è un'attività comune. Spesso è utile eseguire questa operazione potenzialmente dispendiosa in termini di tempo in un thread separato.  Usare il componente <xref:System.ComponentModel.BackgroundWorker> per eseguire questa attività con una quantità di codice molto ridotta.  
  
## Esempio  
 L'esempio di codice seguente illustra come usare un componente <xref:System.ComponentModel.BackgroundWorker> per caricare un file XML da un URL.  Quando l'utente sceglie il pulsante **Download**, il gestore eventi <xref:System.Windows.Forms.Control.Click> chiama il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> di un componente <xref:System.ComponentModel.BackgroundWorker> per avviare l'operazione di download.  Il pulsante è disattivato per la durata del download e quindi abilitato una volta che il download è completato.  Un oggetto <xref:System.Windows.Forms.MessageBox> visualizza i contenuti del file.  
  
 [!code-csharp[System.ComponentModel.BackgroundWorker.IsBusy#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.BackgroundWorker.IsBusy#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/VB/Form1.vb#1)]  
  
 **Download del file**  
  
 Il file viene scaricato nel thread di lavoro <xref:System.ComponentModel.BackgroundWorker> del componente, che esegue il gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  Questo thread inizia nel momento in cui il codice chiama il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>.  
  
 [!code-csharp[System.ComponentModel.BackgroundWorker.IsBusy#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/CS/Form1.cs#3)]
 [!code-vb[System.ComponentModel.BackgroundWorker.IsBusy#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/VB/Form1.vb#3)]  
  
 **Attesa della fine di un BackgroundWorker**  
  
 Il gestore eventi `downloadButton_Click` illustra come attendere il completamento di un'attività asincrona da parte di un componente <xref:System.ComponentModel.BackgroundWorker>.  
  
 Se si vuole solo che l'applicazione risponda ad eventi e non si vuole eseguire lavoro nel thread principale durante l'attesa del completamento del thread in background, è sufficiente uscire dal gestore.  
  
 Se si vuole continuare a lavorare nel thread principale, usare la proprietà <xref:System.ComponentModel.BackgroundWorker.IsBusy%2A> per determinare se il thread <xref:System.ComponentModel.BackgroundWorker> è ancora in esecuzione.  In questo esempio viene aggiornato un indicatore di stato durante l'elaborazione del download.  Assicurarsi di chiamare il metodo <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName> per mantenere reattiva l'interfaccia utente.  
  
 [!code-csharp[System.ComponentModel.BackgroundWorker.IsBusy#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/CS/Form1.cs#2)]
 [!code-vb[System.ComponentModel.BackgroundWorker.IsBusy#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/VB/Form1.vb#2)]  
  
 **Visualizzazione del risultato**  
  
 Il metodo `backgroundWorker1_RunWorkerCompleted` gestisce l'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> e viene chiamato quando l'operazione in background viene completata.  Questo metodo verifica prima di tutto la proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A?displayProperty=fullName>.  Se <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A?displayProperty=fullName> è `null`, il metodo visualizza il contenuto del file,  quindi abilita il pulsante di download, disabilitato all'inizio del download, e reimposta l'indicatore di stato.  
  
 [!code-csharp[System.ComponentModel.BackgroundWorker.IsBusy#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/CS/Form1.cs#4)]
 [!code-vb[System.ComponentModel.BackgroundWorker.IsBusy#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.IsBusy/VB/Form1.vb#4)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System.Drawing, System.Windows.Forms e System.Xml.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Programmazione efficiente  
 Verificare sempre la presenza della proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A?displayProperty=fullName> nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> prima di tentare di accedere alla proprietà <xref:System.ComponentModel.RunWorkerCompletedEventArgs.Result%2A?displayProperty=fullName> o ad eventuali altri oggetti che possano essere influenzati dal gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  
  
## Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>   
 [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)