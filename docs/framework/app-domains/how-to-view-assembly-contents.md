---
title: "Procedura: Visualizzare il contenuto dell&#39;assembly | Microsoft Docs"
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
  - "manifesto dell'assembly, visualizzazione delle informazioni"
  - "Ildasm.exe"
  - "Disassembler MSIL"
  - "assembly [.NET Framework], visualizzazione dei contenuti"
  - "visualizzazione di informazioni sull'assembly"
  - "MSIL"
  - "visualizzazione di informazioni MSIL"
ms.assetid: fb7baaab-4c0d-47ad-8fd3-4591cf834709
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: Visualizzare il contenuto dell&#39;assembly
È possibile utilizzare [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per visualizzare informazioni sul linguaggio MILS \(Microsoft Intermediate Language\) in un file.  Se il file esaminato è un assembly, è possibile che tali informazioni includano gli attributi dell'assembly, oltre a riferimenti ad altri moduli ed assembly.  Queste informazioni possono risultare utili nel determinare se un file è un assembly o se fa parte di un assembly e se tale file contiene riferimenti ad altri moduli o assembly.  
  
### Per visualizzare il contenuto di un assembly mediante Ildasm.exe  
  
1.  Digitare **ildasm** \<*nome assembly*\> dal prompt dei comandi.  Il comando riportato di seguito, ad esempio, esegue il disassemblaggio dell'assembly `Hello.exe`.  
  
    ```  
    ildasm Hello.exe  
    ```  
  
### Per visualizzare informazioni sul manifesto dell'assembly  
  
1.  Fare doppio clic sull'icona del manifesto nella finestra di MSIL Disassembler.  
  
## Esempio  
 Nell'esempio riportato di seguito viene avviato un programma "Hello, World" di base.  Dopo aver compilato il programma, utilizzare Ildasm.exe per disassemblare l'assembly Hello.exe e visualizzarne il manifesto.  
  
 [!code-cpp[Conceptual.Assembly.Contents#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.contents/cpp/source.cpp#1)]
 [!code-csharp[Conceptual.Assembly.Contents#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.contents/cs/source.cs#1)]
 [!code-vb[Conceptual.Assembly.Contents#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.contents/vb/source.vb#1)]  
  
 Se si esegue il comando ildasm.exe nell'assembly Hello.exe e si fa doppio clic sull'icona del manifesto nella finestra IL DASM, verrà prodotto l'output seguente:  
  
```  
  
// Metadata version: v4.0.30319  
.assembly extern mscorlib  
{  
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..  
  .ver 4:0:0:0  
}  
.assembly Hello  
{  
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )   
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx  
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.  
  .hash algorithm 0x00008004  
  .ver 0:0:0:0  
}  
.module Hello.exe  
// MVID: {7C2770DB-1594-438D-BAE5-98764C39CCCA}  
.imagebase 0x00400000  
.file alignment 0x00000200  
.stackreserve 0x00100000  
.subsystem 0x0003       // WINDOWS_CUI  
.corflags 0x00000001    //  ILONLY  
// Image base: 0x00600000  
  
```  
  
 Nella tabella riportata di seguito viene descritta ogni direttiva del manifesto dell'assembly relativo all'assembly Hello.exe utilizzato nell'esempio.  
  
|Direttiva|Descrizione|  
|---------------|-----------------|  
|**.assembly extern \<** *nome assembly* **\>**|Consente di specificare un altro assembly contenente elementi a cui il modulo corrente fa riferimento \(in questo esempio, `mscorlib`\).|  
|**.publickeytoken \<** *token* **\>**|Consente di specificare il token della chiave effettiva dell'assembly a cui si fa riferimento.|  
|**.ver \<** *numero versione* **\>**|Consente di specificare il numero di versione dell'assembly a cui si fa riferimento.|  
|**.assembly \<** *nome assembly* **\>**|Consente di specificare il nome dell'assembly.|  
|**.hash algorithm \<** *valore int32* **\>**|Consente di specificare l'algoritmo hash utilizzato.|  
|**.ver \<** *numero versione* **\>**|Consente di specificare il numero di versione dell'assembly.|  
|**.module \<** *nome file* **\>**|Consente di specificare il nome dei moduli che costituiscono l'assembly.  In questo esempio l'assembly è costituito da un unico file.|  
|**.subsystem \<** *valore* **\>**|Consente di specificare l'ambiente di applicazione necessario per il programma.  In questo esempio il valore 3 indica che il file eseguibile viene eseguito da una console.|  
|**.corflags**|Campo correntemente riservato nei metadati.|  
  
 In un manifesto dell'assembly possono essere contenute svariate direttive diverse, a seconda dei contenuti dell'assembly.  Per un elenco completo delle direttive del manifesto dell'assembly, vedere la documentazione ECMA, in modo particolare "Partition II: Metadata Definition and Semantics" e "Partition III: CIL Instruction Set".  La documentazione è disponibile online; vedere [ECMA C\# e Standard di Common Language Infrastructure](http://go.microsoft.com/fwlink/?LinkID=99212) su MSDN e [Standard ECMA\-335 \- Common Language Infrastructure \(CLI\)](http://go.microsoft.com/fwlink/?LinkID=65552) nel sito Web internazionale di ECMA.  
  
## Vedere anche  
 [Application Domains and Assemblies](http://msdn.microsoft.com/it-it/433b04ae-4ba8-4849-9dbd-79194f240346)   
 [Argomenti relativi alle procedure per domini applicazione e assembly](../../../docs/framework/app-domains/application-domains-and-assemblies-how-to-topics.md)   
 [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)