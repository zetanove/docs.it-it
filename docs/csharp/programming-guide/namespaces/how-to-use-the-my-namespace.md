---
title: "Procedura: utilizzare lo spazio dei nomi My (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, accesso agli spazi dei nomi My"
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# Procedura: utilizzare lo spazio dei nomi My (Guida per programmatori C#)
Lo spazio dei nomi <xref:Microsoft.VisualBasic.MyServices> \(`My` in Visual Basic\) consente di accedere in modo semplice e intuitivo a numerose classi di .NET Framework, permettendo in tal modo di scrivere codice che interagisce con il computer, l'applicazione, le impostazioni, le risorse e così via.  Sebbene originariamente progettato per l'uso con Visual Basic, lo spazio dei nomi `MyServices` può essere utilizzato anche in applicazioni scritte in C\#.  
  
 Per ulteriori informazioni sull'utilizzo dello spazio dei nomi `MyServices` da Visual Basic, vedere [Development with My](../../../visual-basic/developing-apps/development-with-my/index.md).  
  
## Aggiunta di un riferimento  
 Prima di poter utilizzare le classi `MyServices` nella soluzione, è necessario aggiungere un riferimento alla libreria di Visual Basic.  
  
#### Per aggiungere un riferimento alla libreria di Visual Basic  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Riferimenti** e scegliere **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo **Riferimenti** visualizzata scorrere l'elenco e selezionare Microsoft.VisualBasic.dll.  
  
     È inoltre possibile includere la seguente riga nella sezione `using` all'inizio del programma.  
  
     [!code-cs[csProgGuideNamespaces#18](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_1.cs)]  
  
## Esempio  
 In questo esempio vengono chiamati diversi metodi statici contenuti nello spazio dei nomi `MyServices`.  Per compilare questo codice, è necessario aggiungere al progetto un riferimento a Microsoft.VisualBasic.DLL.  
  
 [!code-cs[csProgGuideNamespaces#19](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_2.cs)]  
  
 In un 'applicazione C\# non è possibile chiamare tutte le classi incluse nello spazio dei nomi `MyServices`. La classe <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy>, ad esempio, non è compatibile.  In questo caso specifico, in sostituzione di questa classe è possibile utilizzare i metodi statici inclusi in <xref:Microsoft.VisualBasic.FileIO.FileSystem> e contenuti anche nel file VisualBasic.dll.  Nell'esempio di codice riportato di seguito viene illustrato come utilizzare uno di questi metodi per duplicare una directory:  
  
 [!code-cs[csProgGuideNamespaces#20](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-my-namespace_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   
 [Utilizzo degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)