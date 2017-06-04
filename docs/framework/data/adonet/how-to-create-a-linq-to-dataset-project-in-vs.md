---
title: "Procedura: creare un progetto LINQ to DataSet in Visual Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49ba6cb0-cdd2-4571-aeaa-25bf0f40e9b3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: creare un progetto LINQ to DataSet in Visual Studio
I tipi diversi di progetti [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] richiedono determinati spazi dei nomi importati \(Visual Basic\) o direttive `using` \(C\#\) e riferimenti.  Il requisito minimo è un riferimento a System.Core.dll e una direttiva `using` per <xref:System.Linq>.  Per impostazione predefinita, questi elementi vengono forniti se si crea un nuovo progetto di [!INCLUDE[csharp_orcas_long](../../../../includes/csharp-orcas-long-md.md)].  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] richiede anche un riferimento a System.Data.dll e System.Data.DataSetExtensions.dll e una direttiva `Imports` \(Visual Basic\) o `using` \(C\#\).  
  
 Se un progetto viene aggiornato da una versione precedente di Visual Studio, può essere necessario specificare manualmente questi riferimenti correlati a LINQ.  Può inoltre essere necessario impostare manualmente il progetto in modo che sia destinato a .NET Framework versione 3.5.  
  
> [!NOTE]
>  Se si sta compilando da un prompt dei comandi, è necessario fare manualmente riferimento alle DLL correlate a LINQ in `drive`**:**\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.5.  
  
### Per impostare .NET Framework 3.5 come destinazione  
  
1.  In [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] creare un nuovo progetto di Visual Basic o C\#. In alternativa, è possibile aprire un progetto di Visual Basic o C\# creato in Visual Studio 2005 e seguire le istruzioni per convertirlo in un progetto di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Per un progetto C\# scegliere **Proprietà** dal menu **Progetto**.  
  
    1.  Nella pagina delle proprietà **Applicazione** selezionare .NET Framework 3.5 nell'elenco a discesa **Framework di destinazione**.  
  
3.  Per un progetto di Visual Basic scegliere **Proprietà** dal menu **Progetto**.  
  
    1.  Nella pagina delle proprietà **Compilazione** fare clic su **Opzioni di compilazione avanzate**, quindi selezionare .NET Framework 3.5 nell'elenco a discesa **Framework di destinazione \(tutte le configurazioni\)**.  
  
4.  Scegliere **Aggiungi riferimento** dal menu **Progetto**, quindi nella scheda **.NET** scorrere fino a selezionare **System.Core** e fare clic su **OK**.  
  
5.  Aggiungere una direttiva `using` o uno spazio dei nomi importato per <xref:System.Linq> al progetto o al file del codice sorgente.  
  
     Per altre informazioni, vedere [Direttiva using](../Topic/using%20Directive%20\(C%23%20Reference\).md) o [Procedura: aggiungere o rimuovere spazi dei nomi importati \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md).  
  
### Per abilitare la funzionalità LINQ to DataSet  
  
1.  Se necessario, seguire i passaggi illustrati precedentemente in questo argomento per aggiungere un riferimento a System.Core.dll e una direttiva `using` o uno spazio dei nomi importato per System.Linq.  
  
2.  In un progetto di Visual Basic o C\# scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
3.  Nella finestra di dialogo **Aggiungi riferimento** fare clic sulla scheda **.NET**, se non è in primo piano.  Scorrere fino a selezionare **System.Data** e **System.Data.DataSetExtensions**.  Fare clic sul pulsante **OK**.  
  
4.  Aggiungere una direttiva `using` o uno spazio dei nomi importato per <xref:System.Data> al progetto o al file del codice sorgente.  Per altre informazioni, vedere [Direttiva using](../Topic/using%20Directive%20\(C%23%20Reference\).md) o [Procedura: aggiungere o rimuovere spazi dei nomi importati \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md).  
  
5.  Aggiungere un riferimento a System.Data.DataSetExtensions.dll per la funzionalità LINQ to DataSet.  Aggiungere un riferimento a System.Data.dll, se non è già presente.  
  
6.  Facoltativamente, aggiungere una direttiva `using` o uno spazio dei nomi importato per `System.Data.Common` o `System.Data.SqlClient`, a seconda della modalità di connessione al database.  
  
## Vedere anche  
 [Guida introduttiva](../../../../docs/framework/data/adonet/getting-started-linq-to-dataset.md)   
 [Getting Started with LINQ](http://msdn.microsoft.com/it-it/6cc9af04-950a-4cc3-83d4-2aeb4abe4de9)