---
title: "Procedura: compilare un assembly su singolo file | Microsoft Docs"
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
  - "assembly [.NET Framework], singolo file"
  - "manifesto assembly, assembly su file singolo"
  - "moduli di codice"
  - "riga di comando (compilatori)"
  - "assembly di libreria"
  - "nome file di output per assembly"
  - "assembly su file singolo"
ms.assetid: a6063221-43a5-4d3e-814c-288a4ec69aec
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: compilare un assembly su singolo file
In un assembly su singolo file, ovvero il tipo più semplice di assembly, sono contenute le informazioni e l'implementazione relative al tipo, oltre al [manifesto dell'assembly](../../../docs/framework/app-domains/assembly-manifest.md).  Per creare un assembly su singolo file, è possibile utilizzare i compilatori della riga di comando o [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)].  Per impostazione predefinita, il file di assembly creato dal compilatore avrà estensione EXE.  
  
> [!NOTE]
>  È possibile utilizzare [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] per C\# e Visual Basic solo per la creazione di assembly su singolo file.  Per creare assembly su più file, è necessario utilizzare i compilatori della riga di comando o [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] per Visual C\+\+.  
  
 Nelle procedure seguenti viene mostrato come creare assembly su singolo file utilizzando i compilatori della riga di comando.  
  
### Per creare un assembly con estensione EXE  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     \<*comando compilatore*\> \<*nome modulo*\>  
  
     In questo comando, *comando compilatore* corrisponde al comando del compilatore per il linguaggio utilizzato nel modulo di codice e *nome modulo* indica il nome del modulo di codice da compilare nell'assembly.  
  
 L'esempio riportato di seguito consente di creare un assembly denominato `myCode.exe` da un modulo di codice chiamato `myCode`.  
  
```csharp  
csc myCode.cs  
```  
  
```vb  
vbc myCode.vb  
```  
  
#### Per creare un assembly con estensione exe e specificare il nome del file di output  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     \<*comando compilatore*\> **\/out:**\<*nome file*\> \<*nome modulo*\>  
  
     In questo comando, *comando compilatore* corrisponde al comando del compilatore per il linguaggio utilizzato nel modulo di codice, *nome file* corrisponde al nome del file di output e *nome modulo* indica il nome del modulo di codice da compilare nell'assembly.  
  
 L'esempio riportato di seguito consente di creare un assembly denominato `myAssembly.exe` da un modulo di codice chiamato `myCode`.  
  
```csharp  
csc /out:myAssembly.exe myCode.cs  
```  
  
```vb  
vbc /out:myAssembly.exe myCode.vb  
```  
  
## Creazione degli assembly di librerie  
 Un assembly di libreria è simile ad una libreria di classi.  Tale assembly contiene tipi a cui altri assembly faranno riferimento, ma non dispone di alcun punto di ingresso per avviare l'esecuzione.  
  
#### Per creare un assembly di libreria  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     \<*comando compilatore*\> **\/t:library** \<*nome modulo*\>  
  
     In questo comando, *comando compilatore* corrisponde al comando del compilatore per il linguaggio utilizzato nel modulo di codice e *nome modulo* indica il nome del modulo di codice da compilare nell'assembly.  È possibile utilizzare anche altre opzioni del compilatore, ad esempio l'opzione **\/out:**.  
  
 L'esempio seguente consente di creare un assembly di libreria con nome `myCodeAssembly.dll` da un modulo di codice con nome `myCode`.  
  
```csharp  
csc /out:myCodeLibrary.dll /t:library myCode.cs  
```  
  
```vb  
vbc /out:myCodeLibrary.dll /t:library myCode.vb  
```  
  
## Vedere anche  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Assembly su più file](../../../docs/framework/app-domains/multifile-assemblies.md)   
 [Procedura: Compilare un assembly su più file](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)