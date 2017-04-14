---
title: "Procedura: firmare un assembly con un nome sicuro | Microsoft Docs"
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
  - "assembly [.NET Framework], firma"
  - "assembly [.NET Framework], con nome sicuro"
  - "firma di assembly"
  - "assembly con nome sicuro, firma con nomi sicuri"
ms.assetid: 2c30799a-a826-46b4-a25d-c584027a6c67
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Procedura: firmare un assembly con un nome sicuro
Sono disponibili diversi modi per firmare un assembly con un nome sicuro:  
  
-   Utilizzando la scheda di **Firma** nella finestra di dialogo **Proprietà** di un progetto in Visual Studio. Questo è il modo più semplice e più pratico per firmare un assembly con un nome sicuro.  
  
-   Usando [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) per collegare un modulo di codice di .NET Framework \(un file con estensione netmodule\) con un file di chiave.  
  
-   Utilizzando attributi dell'assembly per inserire le informazioni relative al nome sicuro nel codice. È possibile utilizzare l'attributo <xref:System.Reflection.AssemblyKeyFileAttribute> o <xref:System.Reflection.AssemblyKeyNameAttribute>, a seconda della posizione del file di chiave da utilizzare.  
  
-   Utilizzando le opzioni del compilatore.  
  
 Per firmare un assembly con un nome sicuro, è necessario disporre di una coppia di chiavi crittografiche. Per altre informazioni sulla creazione di una coppia di chiavi, vedere [Procedura: creare una coppia di chiavi pubblica\/privata](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md).  
  
### Per creare e firmare un assembly con un nome sicuro utilizzando Visual Studio  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per il progetto, quindi scegliere **Proprietà**.  
  
2.  Scegliere la scheda **Firma**.  
  
3.  Selezionare la casella **Firma assembly**.  
  
4.  Nella casella **Scegli un file chiave con nome sicuro** scegliere **\<Sfoglia...\>**quindi passare al file di chiave. Per creare un nuovo file di chiave, scegliere **\<Nuovo...\>** e immettere il nome nella finestra di dialogo **Crea chiave con nome sicuro**.  
  
### Per creare e firmare un assembly con un nome sicuro utilizzando Assembly Linker  
  
-   Al [prompt dei comandi di Visual Studio](../../../docs/framework/tools/developer-command-prompt-for-vs.md) digitare il comando seguente:  
  
     **al** **\/out:**\<*assemblyName*\> *\<moduleName\>* **\/keyfile:**\<*keyfileName*\>  
  
     dove:  
  
     *assemblyName*  
     Nome sicuro di assembly con firma \(file .dll o .exe\) che verrà generato da Assembly Linker.  
  
     *moduleName*  
     Nome di un modulo di codice di .NET Framework \(file con estensione netmodule\) che include uno o più tipi. È possibile creare un file .netmodule durante la compilazione del codice con l'opzione `/target:module` in C\# o Visual Basic.  
  
     *keyfileName*  
     Nome del contenitore o del file che contiene la coppia di chiavi. Assembly Linker interpreta un percorso relativo in relazione alla directory corrente.  
  
 L'esempio seguente consente di firmare l'assembly `MyAssembly.dll` con un nome sicuro utilizzando il file di chiave `sgKey.snk`.  
  
```  
al /out:MyAssembly.dll MyModule.netmodule /keyfile:sgKey.snk  
```  
  
 Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [Assembly Linker](../../../docs/framework/tools/al-exe-assembly-linker.md).  
  
#### Per firmare un assembly con un nome sicuro utilizzando attributi  
  
1.  Aggiungere l'attributo <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> o <xref:System.Reflection.AssemblyKeyNameAttribute> al file del codice sorgente, specificando il nome del file o del contenitore contenente la coppia di chiavi da utilizzare per la firma dell'assembly con un nome sicuro.  
  
2.  Compilare normalmente il file del codice sorgente.  
  
> [!NOTE]
>  Nei compilatori C\# e Visual Basic vengono pubblicati avvisi del compilatore \(rispettivamente CS1699 e BC41008\) quando viene rilevato l'attributo <xref:System.Reflection.AssemblyKeyFileAttribute> o <xref:System.Reflection.AssemblyKeyNameAttribute> nel codice sorgente. È possibile ignorare gli avvisi.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato l'attributo <xref:System.Reflection.AssemblyKeyFileAttribute> con un file di chiave denominato `keyfile.snk`, che si trova nella directory in cui viene compilato l'assembly.  
  
 [!code-cpp[AssemblyName_KeyPair#21](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyName_KeyPair/CPP/keyfileattrib.cpp#21)]
 [!code-csharp[AssemblyName_KeyPair#21](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyName_KeyPair/CS/keyfileattrib.cs#21)]
 [!code-vb[AssemblyName_KeyPair#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyName_KeyPair/VB/keyfileattrib.vb#21)]  
  
 È inoltre possibile ritardare la firma di un assembly durante la compilazione del file del codice sorgente. Per ulteriori informazioni, vedere [Ritardo della firma di un assembly](../../../docs/framework/app-domains/delay-sign-assembly.md).  
  
### Per firmare un assembly con un nome sicuro utilizzando il compilatore  
  
-   Compilare il file o i file del codice sorgente con l'opzione del compilatore `/keyfile` o `/delaysign` in C\# e Visual Basic o con l'opzione del linker `/KEYFILE` o `/DELAYSIGN` in C\+\+. Dopo il nome di opzione, aggiungere due punti e il nome del file di chiave. Se si utilizzano compilatori della riga di comando, è possibile copiare il file di chiave nella directory contenente i file del codice sorgente.  
  
     Per informazioni sulla firma ritardata, vedere [Ritardo della firma di un assembly](../../../docs/framework/app-domains/delay-sign-assembly.md).  
  
     Nell'esempio riportato di seguito viene utilizzato il compilatore C\# e viene firmato l'assembly `UtilityLibrary.dll` con un nome sicuro, utilizzando il file di chiave `sgKey.snk`.  
  
    ```  
    csc /t:library UtilityLibrary.cs /keyfile:sgKey.snk  
    ```  
  
## Vedere anche  
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)   
 [Procedura: creare una coppia di chiavi pubblica\/privata](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)   
 [Al.exe \(Assembly Linker\)](../../../docs/framework/tools/al-exe-assembly-linker.md)   
 [Ritardo della firma di un assembly](../../../docs/framework/app-domains/delay-sign-assembly.md)   
 [Gestione delle firme di assembly e manifesti](../Topic/Managing%20Assembly%20and%20Manifest%20Signing.md)   
 [Pagina Firma, Progettazione progetti](../Topic/Signing%20Page,%20Project%20Designer.md)