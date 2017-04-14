---
title: "Procedura: enumerare un sottoinsieme di code di stampa | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "enumerazione, sottoinsieme di code di stampa"
  - "code di stampa, enumerazione di sottoinsiemi"
ms.assetid: cc4a1b5b-d46f-4c5e-bc26-22c226e4bee0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: enumerare un sottoinsieme di code di stampa
Una situazione che spesso i professionisti del settore IT \(Information Technology\) che gestiscono una serie di stampanti a livello aziendale devono affrontare riguarda la creazione di un elenco di stampanti con determinate caratteristiche.  Tale funzionalità viene fornita dal metodo <xref:System.Printing.PrintServer.GetPrintQueues%2A> di un oggetto <xref:System.Printing.PrintServer> e dall'enumerazione <xref:System.Printing.EnumeratedPrintQueueTypes>.  
  
## Esempio  
 Nell'esempio riportato di seguito, nella parte iniziale del codice viene creata una matrice di flag che specificano le caratteristiche delle code di stampa che si desidera elencare.  In questo esempio, si ricercano le code di stampa installate localmente sul server di stampa e condivise.  L'enumerazione <xref:System.Printing.EnumeratedPrintQueueTypes> offre molte altre possibilità.  
  
 Il codice crea quindi un oggetto <xref:System.Printing.LocalPrintServer>, una classe derivata da <xref:System.Printing.PrintServer>.  Il server di stampa locale è il computer in cui l'applicazione è in esecuzione.  
  
 L'ultimo passaggio significativo consiste nel passare la matrice al metodo <xref:System.Printing.PrintServer.GetPrintQueues%2A>.  
  
 I risultati vengono infine presentati all'utente.  
  
 [!code-cpp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CPP/Program.cpp#listsubsetofprintqueues)]
 [!code-csharp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CSharp/Program.cs#listsubsetofprintqueues)]
 [!code-vb[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/visualbasic/program.vb#listsubsetofprintqueues)]  
  
 È possibile estendere questo esempio mediante un ulteriore screening eseguito nel ciclo `foreach` che scorre tutte le code di stampa.  Ad esempio, è possibile escludere le stampanti che non supportano la stampa fronte retro chiamando il metodo <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> di ogni coda di stampa all'interno del ciclo e verificando la presenza di stampe fronte retro nel valore restituito.  
  
## Vedere anche  
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319)