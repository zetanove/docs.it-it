---
title: "Procedura: scorrere una struttura ad albero di directory (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "iterazione di file [C#]"
  - "iterazione in cartelle [C#]"
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# Procedura: scorrere una struttura ad albero di directory (Guida per programmatori C#)
Per "scorrere una struttura ad albero di directory" si intende accedere a ogni file in ogni sottodirectory annidata sotto una specifica cartella radice, a qualsiasi profondità.  Non si deve necessariamente aprire ogni file.  È possibile recuperare solo il nome del file o della sottodirectory come `string` o recuperare informazioni aggiuntive nella forma di oggetto <xref:System.IO.FileInfo?displayProperty=fullName> o <xref:System.IO.DirectoryInfo?displayProperty=fullName>.  
  
> [!NOTE]
>  In Windows, i termini "directory" e "cartella" sono utilizzati indifferentemente.  Nella maggior parte della documentazione e del testo dell'interfaccia utente si utilizza il termine "cartella", ma nella libreria di classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] si utilizza il termine "directory".  
  
 Nel caso più semplice, nel quale si è certi di disporre delle autorizzazioni di accesso per tutte le directory sotto una radice specificata, è possibile utilizzare il flag `System.IO.SearchOption.AllDirectories`.  Questo flag restituisce tutte le sottodirectory annidate che corrispondono al modello specificato.  Nell'esempio seguente viene illustrato come utilizzare questo flag.  
  
```c#  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 La debolezza di questo approccio sta nel fatto che, se una delle sottodirectory sotto la radice specificata provoca <xref:System.IO.DirectoryNotFoundException> o <xref:System.UnauthorizedAccessException>, l'esecuzione dell'intero metodo ha esito negativo e non viene restituita alcuna directory.  La stessa situazione può verificarsi quando si utilizza il metodo <xref:System.IO.DirectoryInfo.GetFiles%2A>.  Se è necessario gestire queste eccezioni sulle sottocartelle specifiche, occorre procedere manualmente nella struttura ad albero di directory, come mostrato negli esempi seguenti.  
  
 Quando si procede manualmente in una struttura ad albero di directory, è possibile gestire prima le sottodirectory \(*attraversamento pre\-ordine*\) o prima i file \(*attraversamento post\-ordine*\).  Se si esegue un attraversamento pre\-ordine, si procede lungo l'intera struttura ad albero sotto la cartella corrente prima di scorrere i file che sono direttamente in quella cartella.  Negli esempi disponibili più avanti in questo documento viene eseguito l'attraversamento post\-ordine, ma è possibile modificare tali esempi facilmente per eseguire l'attraversamento pre\-ordine.  
  
 Un'altra opzione consiste nel decidere se utilizzare un attraversamento ricorsivo o basato su stack.  Negli esempi disponibili più avanti in questo documento sono mostrati entrambi gli approcci.  
  
 Se è necessario eseguire svariate operazioni su file e cartelle, è possibile modularizzare questi esempi effettuando il refactoring dell'operazione in funzioni separate che è possibile richiamare tramite un solo delegato.  
  
> [!NOTE]
>  I file system NTFS possono contenere *punti di analisi* nella forma di  *punti di giunzione*, *collegamenti simbolici* e *collegamenti reali*.  I metodi .NET Framework come <xref:System.IO.DirectoryInfo.GetFiles%2A> e <xref:System.IO.DirectoryInfo.GetDirectories%2A> non restituiranno le sottodirectory sotto un punto di analisi.  Questo comportamento protegge dal rischio di entrare in un ciclo infinito quando due punti di analisi si riferiscono l'uno all'altro.  In generale, è necessario prestare estrema attenzione nella gestione dei punti di analisi per assicurarsi di non modificare o eliminare file in modo accidentale.  Se si richiede un controllo preciso sui punti di analisi, utilizzare pInvoke o codice nativo per chiamare direttamente i metodi appropriati del file system Win32.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come procedere in una struttura ad albero di directory tramite ricorsione.  L'approccio ricorsivo è elegante ma può potenzialmente provocare un'eccezione di overflow dello stack se la struttura ad albero di directory è ampia e annidata in modo profondo.  
  
 Le specifiche eccezioni gestite e le specifiche azioni eseguite su ogni file o cartella vengono fornite solo come esempi.  Questo codice va modificato per soddisfare requisiti specifici.  Per ulteriori informazioni, vedere i commenti nel codice.  
  
 [!code-cs[csFilesandFolders#1](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come scorrere file e cartelle in una struttura ad albero di directory senza utilizzare la ricorsione.  Questa tecnica utilizza il tipo di raccolta <xref:System.Collections.Generic.Stack%601> generica, che è uno stack LIFO \(Last In, First Out\).  
  
 Le specifiche eccezioni gestite e le specifiche azioni eseguite su ogni file o cartella vengono fornite solo come esempi.  Questo codice va modificato per soddisfare requisiti specifici.  Per ulteriori informazioni, vedere i commenti nel codice.  
  
 [!code-cs[csFilesandFolders#2](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_2.cs)]  
  
 L'operazione di verifica su ogni cartella per determinare se l'applicazione dispone dell'autorizzazione ad aprirla richiede in genere troppo tempo.  L'esempio di codice, pertanto, include solo quella parte dell'operazione in un blocco `try/catch`.  È possibile modificare il blocco `catch` in modo da tentare di elevare le autorizzazioni e provare nuovamente l'accesso in caso di accesso negato a una cartella.  Di regola, rilevare solo le eccezioni che è possibile gestire senza lasciare l'applicazione in stato sconosciuto.  
  
 Se è necessario archiviare il contenuto di una struttura ad albero di directory, in memoria o su disco, la migliore opzione è archiviare solo la proprietà <xref:System.IO.FileSystemInfo.FullName%2A> \(di tipo `string`\) per ogni file.  È possibile utilizzare quindi questa stringa per creare un nuovo oggetto <xref:System.IO.FileInfo> o <xref:System.IO.DirectoryInfo>, in base alle esigenze, o aprire i file che richiedono ulteriore elaborazione.  
  
## Programmazione efficiente  
 Un codice di iterazione di file efficiente deve tenere in considerazione le molte complessità del file system.  Per ulteriori informazioni, vedere [NTFS Technical Reference](http://go.microsoft.com/fwlink/?LinkId=79488) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 <xref:System.IO>   
 [LINQ and File Directories](../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)