---
title: "Uso dei file RESX a livello di codice | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "file di risorse, RESX"
  - "RESX (file)"
ms.assetid: 168f941a-2b84-43f8-933f-cf4a8548d824
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Uso dei file RESX a livello di codice
Poiché i file di risorse XML \(con estensione resx\) devono essere costituiti da codice XML ben definito, comprensivo di un'intestazione che deve seguire uno schema specifico, seguita da dati in coppie nome\/valore, la creazione manuale di questi file è soggetta a errori. In alternativa, è possibile creare file con estensione resx a livello di codice usando tipi e membri inclusi nella libreria di classi .NET Framework. La libreria di classi .NET Framework può essere usata anche per recuperare risorse archiviate in file con estensione resx. Questo argomento illustra come usare i tipi e i membri nello spazio dei nomi <xref:System.Resources> per i file RESX.  
  
 Tenere presente che questo articolo descrive solo l'uso di file XML \(con estensione resx\) che contengono risorse. Per informazioni sull'uso dei file di risorse binari che sono stati incorporati negli assembly, vedere l'argomento <xref:System.Resources.ResourceManager>.  
  
> [!WARNING]
>  Esistono anche modi per usare i file RESX, oltre all'uso a livello di codice. Quando si aggiunge un file di risorse a un progetto di Visual Studio, Visual Studio fornisce un'interfaccia per la creazione e la gestione di un file RESX e converte automaticamente il file RESX in un file con estensione resources in fase di compilazione. È anche possibile usare un editor di testo per modificare direttamente un file RESX. Prestare comunque attenzione a non modificare le eventuali informazioni binarie archiviate nel file, per evitare di danneggiarlo.  
  
## Creazione di un file RESX  
 È possibile usare la classe <xref:System.Resources.ResXResourceWriter?displayProperty=fullName> per creare un file RESX a livello di codice seguendo questa procedura:  
  
1.  Creare un'istanza di un oggetto <xref:System.Resources.ResXResourceWriter> chiamando il metodo <xref:System.Resources.ResXResourceWriter.%23ctor%28System.String%29?displayProperty=fullName> e specificando il nome del file RESX. Il nome del file deve includere l'estensione resx. Se si crea un'istanza dell'oggetto <xref:System.Resources.ResXResourceWriter> in un blocco `using`, non è necessario chiamare esplicitamente il metodo <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=fullName> nel passaggio 3.  
  
2.  Chiamare il metodo <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=fullName> per ogni risorsa da aggiungere al file. Usare l'overload di questo metodo per aggiungere dati stringa, oggetto e binari \(matrice di byte\). Se la risorsa è un oggetto, deve essere serializzabile.  
  
3.  Chiamare il metodo <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=fullName> per generare il file di risorse e per rilasciare tutte le risorse. Se l'oggetto <xref:System.Resources.ResXResourceWriter> è stato creato all'interno di un blocco `using`, le risorse vengono scritte nel file RESX e le risorse usate dall'oggetto <xref:System.Resources.ResXResourceWriter> vengono rilasciate alla fine del blocco `using`.  
  
 Il file RESX risultante ha l'intestazione appropriata e un tag `data` per ogni risorsa aggiunta dal metodo <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=fullName>.  
  
> [!WARNING]
>  Non usare file di risorse per archiviare password, informazioni sensibili per la sicurezza o dati personali.  
  
 Nell'esempio seguente viene creato un file con estensione resx denominato CarResources.resx che archivia sei stringhe, un'icona e due oggetti definiti dall'applicazione, ovvero due oggetti `Automobile`. Si noti che la classe `Automobile`, che viene definita e di cui viene creata un'istanza nell'esempio, è contrassegnata con l'attributo <xref:System.SerializableAttribute>.  
  
 [!code-csharp[Conceptual.Resources.ResX#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/create1.cs#1)]
 [!code-vb[Conceptual.Resources.ResX#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/create1.vb#1)]  
  
> [!IMPORTANT]
>  Si può anche usare Visual Studio per creare file RESX. In fase di compilazione Visual Studio usa il [generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per convertire il file RESX in una risorsa binaria \(con estensione resources\) e lo incorpora anche nell'assembly dell'applicazione o in un assembly satellite.  
  
 Non è possibile incorporare un file RESX in un eseguibile di runtime o compilarlo in un assembly satellite. Il file RESX deve essere convertito in un file di risorse binario \(con estensione resources\) usando il [generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md). Successivamente, il file con estensione resources risultante può essere incorporato in un assembly dell'applicazione o in un assembly satellite. Per altre informazioni, vedere [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md).  
  
## Enumerazione delle risorse  
 In alcuni casi può essere necessario recuperare tutte le risorse anziché una risorsa specifica da un file RESX. A questo scopo, si può usare la classe <xref:System.Resources.ResXResourceReader?displayProperty=fullName>, che fornisce un enumeratore per tutte le risorse nel file RESX. La classe <xref:System.Resources.ResXResourceReader?displayProperty=fullName> implementa <xref:System.Collections.IDictionaryEnumerator>, che restituisce un oggetto <xref:System.Collections.DictionaryEntry> che rappresenta una risorsa specifica per ogni iterazione del ciclo. La relativa proprietà <xref:System.Collections.DictionaryEntry.Key%2A?displayProperty=fullName> restituisce la chiave della risorsa e la proprietà <xref:System.Collections.DictionaryEntry.Value%2A?displayProperty=fullName> restituisce il valore della risorsa.  
  
 L'esempio seguente consente di creare un oggetto <xref:System.Resources.ResXResourceReader> per il file CarResources.resx creato nell'esempio precedente e di scorrere il file di risorse. Aggiunge i due oggetti `Automobile` definiti nel file di risorse a un oggetto <xref:System.Collections.Generic.List%601?displayProperty=fullName> e aggiunge cinque delle sei stringhe a un oggetto <xref:System.Collections.SortedList>. I valori nell'oggetto <xref:System.Collections.SortedList> vengono convertiti in una matrice di parametri, usata per visualizzare le intestazioni di colonna nella console. Nella console vengono visualizzati anche i valori della proprietà `Automobile`.  
  
 [!code-csharp[Conceptual.Resources.ResX#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/enumerate1.cs#2)]
 [!code-vb[Conceptual.Resources.ResX#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/enumerate1.vb#2)]  
  
## Recupero di una risorsa specifica  
 Oltre a enumerare gli elementi in un file RESX, è possibile recuperare una risorsa specifica in base al nome tramite la classe <xref:System.Resources.ResXResourceSet?displayProperty=fullName>. Il metodo <xref:System.Resources.ResourceSet.GetString%28System.String%29?displayProperty=fullName> recupera il valore di una risorsa di tipo stringa denominata. Il metodo <xref:System.Resources.ResourceSet.GetObject%28System.String%29?displayProperty=fullName> recupera il valore di un oggetto denominato o di dati binari. Il metodo restituisce un oggetto di cui deve essere eseguito il cast \(in C\#\) o da convertire \(in Visual Basic\) in un oggetto del tipo appropriato.  
  
 L'esempio seguente recupera l'icona e la stringa della didascalia di un form in base ai nomi delle risorse corrispondenti. Recupera anche gli oggetti `Automobile` definiti dall'applicazione usati nell'esempio precedente e li visualizza in un controllo <xref:System.Windows.Forms.DataGridView>.  
  
 [!code-csharp[Conceptual.Resources.ResX#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/retrieve1.cs#3)]
 [!code-vb[Conceptual.Resources.ResX#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/retrieve1.vb#3)]  
  
## Conversione dei file RESX in file binari con estensione resources  
 La conversione dei file RESX in file di risorse binari incorporati \(con estensione resources\) presenta vantaggi significativi. Sebbene i file RESX siano facili da leggere e gestire durante lo sviluppo di applicazioni, è raro che siano inclusi nelle applicazioni finite. Se vengono distribuiti con un'applicazione, sono costituiti da file separati indipendenti dall'eseguibile dell'applicazione e dalle librerie associate. Al contrario, i file con estensione resources sono incorporati nell'eseguibile dell'applicazione o negli assembly associati. Inoltre, per le applicazioni localizzate, se si basano su file RESX in fase di esecuzione la responsabilità della gestione del fallback delle risorse ricade sullo sviluppatore. Se invece è stato creato un set di assembly satellite che contengono i file con estensione resources incorporati, il processo di fallback delle risorse viene gestito da Common Language Runtime.  
  
 Per convertire un file con estensione resx in un file con estensione resources, usare il [generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md), con la seguente sintassi di base:  
  
 **Resgen.exe** *.resxNomeFile*  
  
 Il risultato è un file di risorse binario con lo stesso nome file radice del file RESX e l'estensione resources. Questo file può quindi essere compilato in un file eseguibile o una libreria in fase di compilazione. Se si usa il compilatore Visual Basic, usare la sintassi seguente per incorporare un file con estensione resources nell'eseguibile di un'applicazione:  
  
 **vbc** *filename* **.vb \/resource:** *.resourcesFilename*  
  
 Se si usa C\#, la sintassi è la seguente:  
  
 **csc** *filename* **.cs \/resource:** *.resourcesFilename*  
  
 Il file con estensione resources può essere incorporato in un assembly satellite anche tramite [Assembly Linker \(AL.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md), che ha la seguente sintassi di base:  
  
 **al** *resourcesFilename* **\/out:** *assemblyFilename*  
  
## Vedere anche  
 [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [Resgen.exe \(Resource File Generator\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)   
 [Al.exe \(Assembly Linker\)](../../../docs/framework/tools/al-exe-assembly-linker.md)