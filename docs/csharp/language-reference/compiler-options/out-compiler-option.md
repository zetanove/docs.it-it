---
title: "/out (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/out"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/out compiler option [C#]"
  - "out compiler option [C#]"
  - "-out compiler option [C#]"
ms.assetid: 70d91d01-7bd2-4aea-ba8b-4e9807e9caa5
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /out (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/out** specifica il nome del file di output.  
  
## Sintassi  
  
```  
/out:filename  
```  
  
## Argomenti  
 `filename`  
 Rappresenta il nome del file di output creato dal compilatore.  
  
## Note  
 Alla riga di comando è possibile specificare più file di output per la compilazione.  Dopo l'opzione **\/out** è prevista la presenza di uno o più file di codice sorgente.  Tali file vengono quindi compilati nel file di output specificato con l'opzione **\/out**.  
  
 Specificare il nome completo e l'estensione del file che si desidera creare.  
  
 Se non si specifica alcun nome per il file di output:  
  
-   Il nome di un file EXE corrisponderà al nome del primo file di codice sorgente che contiene il metodo **Main**.  
  
-   Il nome assegnato al file .dll o .netmodule corrisponderà al nome del primo file di codice sorgente.  
  
 Non è possibile utilizzare per la compilazione di un file di output un file di codice sorgente già utilizzato per compilare un altro file di output nella stessa compilazione.  
  
 Quando si generano più file di output in una compilazione dalla riga di comando, tenere presente che solo uno dei file di output può rappresentare un assembly e che solo il primo file di output specificato \(in modo implicito o esplicito con l'opzione **\/out**\) può rappresentare l'assembly.  
  
 I moduli prodotti durante la compilazione diventano file associati a un assembly prodotto anch'esso in fase di compilazione.  Per visualizzare il manifesto assembly e quindi i file associati, utilizzare il file [ildasm.exe](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md).  
  
 L'opzione del compilatore \/out è necessaria affinché un file eseguibile sia la destinazione di un assembly friend.  Per ulteriori informazioni, vedere [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Nome assembly**.  
  
     Per impostare questa opzione del compilatore a livello di codice: <xref:VSLangProj80.ProjectProperties3.OutputFileName%2A> è una proprietà di sola lettura caratterizzata da una combinazione del tipo di progetto \(file eseguibile, libreria e così via\) e del nome dell'assembly.  Per impostare il nome del file di output, sarà necessario modificare una o entrambe queste proprietà.  
  
## Esempio  
 Per compilare `t.cs` e creare il file di output `t.exe`, nonché per generare `t2.cs` e creare il file di output del modulo `mymodule.netmodule`:  
  
```  
csc t.cs /out:mymodule.netmodule /target:module t2.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)