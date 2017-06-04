---
title: "Procedura: Recuperare archivi per lo spazio di memorizzazione isolato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "archivi, recupero"
  - "archiviazione di dati usando lo spazio di memorizzazione isolato, recupero di archivi"
  - "spazio di memorizzazione isolato, recupero di archivi"
  - "archivi dati, recupero"
  - "archivio dati usando lo spazio di memorizzazione isolato, recupero di archivi"
ms.assetid: fcb6b178-d526-47c4-b029-e946f880f9db
caps.latest.revision: 19
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: Recuperare archivi per lo spazio di memorizzazione isolato
Un archivio isolato espone un file system virtuale all'interno di un raggruppamento dati.  La classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> fornisce diversi metodi per l'interazione con un archivio isolato.  Per creare e recuperare archivi, <xref:System.IO.IsolatedStorage.IsolatedStorageFile> fornisce tre metodi statici:  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A> restituisce uno spazio di memorizzazione isolato in base ad utente e assembly.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> restituisce uno spazio di memorizzazione isolato in base a dominio e assembly.  
  
     Questi due metodi recuperano un archivio che appartiene al codice da cui vengono chiamati.  
  
-   Il metodo statico <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> restituisce uno spazio di memorizzazione isolato che viene specificato tramite il passaggio di una combinazione di parametri di ambito.  
  
 Nell'esempio di codice che segue viene recuperato un archivio isolato in base all'utente, al dominio e all'assembly.  
  
 [!code-cpp[Conceptual.IsolatedStorage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#6)]
 [!code-csharp[Conceptual.IsolatedStorage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#6)]
 [!code-vb[Conceptual.IsolatedStorage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#6)]  
  
 È possibile utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> per specificare che un archivio deve effettuare il roaming con un profilo di utente roaming.  Per ulteriori informazioni su come effettuare questa operazione, vedere [Tipi di isolamento](../../../docs/standard/io/types-of-isolation.md).  
  
 Per impostazione predefinita, gli archivi isolati ottenuti da assembly diversi sono archivi diversi.  È possibile accedere all'archivio di un dominio o di un assembly diverso specificando un'evidenza di dominio nei parametri del metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>.  L'esecuzione di questa operazione richiede l'autorizzazione per accedere all'archiviazione isolata tramite l'identità del dominio applicazione.  Per ulteriori informazioni, vedere l'overload del metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>.  
  
 I metodi <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A>, e <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> restituiscono un oggetto <xref:System.IO.IsolatedStorage.IsolatedStorageFile>.  Per individuare il tipo di isolamento più adatto alle proprie esigenze, vedere [Tipi di isolamento](../../../docs/standard/io/types-of-isolation.md).  Una volta ottenuto un oggetto file di archiviazione isolata, è possibile utilizzare i metodi dell'archiviazione isolata per leggere, scrivere, creare ed eliminare file e directory di file.  
  
 Non esistono meccanismi che impediscono al codice di passare un oggetto <xref:System.IO.IsolatedStorage.IsolatedStorageFile> a un codice che non dispone di autorizzazioni sufficienti a ottenere l'archivio autonomamente.  Le identità di dominio e assembly e le autorizzazioni dello spazio di memorizzazione isolato vengono controllate solo quando si ottiene un riferimento a un oggetto <xref:System.IO.IsolatedStorage.IsolatedStorage>, in genere tramite il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> o <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>.  La protezione dei riferimenti agli oggetti <xref:System.IO.IsolatedStorage.IsolatedStorageFile> è pertanto responsabilità del codice che utilizza tali riferimenti.  
  
## Esempio  
 Il codice che segue fornisce un esempio molto semplice di una classe che ottiene un archivio isolato in base all'utente e all'assembly.  È possibile modificare il codice in modo da recuperare un archivio isolato in base a utente, dominio e assembly aggiungendo <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=fullName> agli argomenti passati dal metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>.  
  
 Una volta eseguito il codice, è possibile verificare che l'archivio sia stato creato digitando **StoreAdm \/LIST** nella riga di comando.  Questo esegue [Isolated Storage tool \(Storeadm.exe\)](../../../docs/framework/tools/storeadm-exe-isolated-storage-tool.md) ed elenca tutti gli archivi isolati correnti dell'utente.  
  
 [!code-cpp[Conceptual.IsolatedStorage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#7)]
 [!code-csharp[Conceptual.IsolatedStorage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#7)]
 [!code-vb[Conceptual.IsolatedStorage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#7)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)   
 [Tipi di isolamento](../../../docs/standard/io/types-of-isolation.md)   
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)