---
title: "Procedura: creare una coppia di chiavi pubblica/privata | Microsoft Docs"
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
  - "coppie di chiavi per assembly con nome sicuro"
  - "firma di assembly"
  - "assembly [.NET Framework], firma"
  - "coppie di chiavi crittografiche"
  - "file snk (file delle coppie di chiavi)"
  - "coppie di chiavi pubbliche/private"
  - "file con estensione snk"
  - "assembly con nome sicuro, coppie di chiavi"
ms.assetid: 05026813-f3bd-4d7c-9e0b-fc588eb3d114
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: creare una coppia di chiavi pubblica/privata
Per firmare un assembly con un nome sicuro, è necessario disporre di una coppia di chiavi, pubblica e privata.  Tale coppia di chiavi crittografiche, pubblica e privata, viene utilizzata durante la compilazione per creare un assembly con nome sicuro.  È possibile creare una coppia di chiavi utilizzando lo [strumento Nome sicuro \(Sn.exe\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md).  Ai file di coppie di chiavi è solitamente associata l'estensione file SNK.  
  
> [!NOTE]
>  In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] le pagine delle proprietà del progetto C\# e Visual Basic includono una scheda **Firma** che consente di selezionare i file di chiave esistenti o di generare i nuovi file di chiave senza utilizzare Sn.exe.  In Visual C\+\+ è possibile specificare il percorso di un file di chiave esistente nella pagina delle proprietà **Avanzate** nella sezione **Linker** della sezione **Proprietà di configurazione** della finestra **Pagine delle proprietà**.  L'utilizzo dell'attributo <xref:System.Reflection.AssemblyKeyFileAttribute> per identificare le coppie di file di chiave è diventato obsoleto a partire da [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)].  
  
### Per creare una coppia di chiavi  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     **sn –k** \<*nome file*\>  
  
     In questo comando, *nome file* corrisponde al nome del file di output contenente la coppia di chiavi.  
  
 L'esempio seguente consente di creare una coppia di chiavi denominata `sgKey.snk`.  
  
```  
sn -k sgKey.snk  
```  
  
 Se si desidera ritardare la firma di un assembly e si controlla l'intera coppia di chiavi \(evento improbabile al di fuori degli scenari di testing\), è possibile utilizzare i comandi seguenti per generare una coppia di chiavi ed estrarre da tale coppia una chiave pubblica, che viene salvata in un file distinto.  Creare prima di tutto la coppia di chiavi:  
  
```  
sn -k keypair.snk  
```  
  
-   Estrarre quindi la chiave pubblica dalla coppia di chiavi e copiarla in un file distinto:  
  
```  
sn -p keypair.snk public.snk  
```  
  
-   Dopo aver creato la coppia di chiavi, è necessario salvare il file in una posizione accessibile allo strumento di firma con nome sicuro.  
  
 Quando firma un assembly con un nome sicuro, [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) cerca il file della chiave relativo alla directory corrente e alla directory di output.  Se si utilizzano i compilatori della riga di comando, è sufficiente copiare la chiave nella directory corrente contenente i moduli di codice.  
  
 Se si utilizza una versione precedente di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] in cui non è disponibile una scheda **Firma** nelle proprietà del progetto, è consigliabile utilizzare come percorso del file di chiave la directory del progetto con l'attributo di file specificato come segue:  
  
 [!code-cpp[AssemblyName_KeyPair#21](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyName_KeyPair/CPP/keyfileattrib.cpp#21)]
 [!code-csharp[AssemblyName_KeyPair#21](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyName_KeyPair/CS/keyfileattrib.cs#21)]
 [!code-vb[AssemblyName_KeyPair#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyName_KeyPair/VB/keyfileattrib.vb#21)]  
  
## Vedere anche  
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)