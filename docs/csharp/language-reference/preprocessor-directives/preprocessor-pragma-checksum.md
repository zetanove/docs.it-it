---
title: "#pragma checksum (Riferimenti per C#) | Microsoft Docs"
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
  - "#pragma checksum"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#pragma checksum [C#]"
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #pragma checksum (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di generare i checksum per i file di origine facilitando in tal modo le operazioni di debug delle pagine [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
## Sintassi  
  
```  
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### Parametri  
 `"filename"`  
 Nome del file che richiede il monitoraggio per modifiche o aggiornamenti.  
  
 `"{guid}"`  
 Identificatore univoco globale \(GUID, Globally Unique Identifier\) del file.  
  
 `"checksum_bytes"`  
 Stringa di cifre esadecimali che rappresenta i byte del checksum.  Deve essere un numero pari di cifre esadecimali.  Un numero dispari di cifre genera un avviso in fase di compilazione, pertanto la direttiva viene ignorata.  
  
## Note  
 Il debugger di Visual Studio utilizza un checksum per trovare sempre l'origine corretta.  Il compilatore calcola il checksum di un file di origine, quindi genera l'output nel file del database di programma \(PDB\).  Il PDB viene quindi utilizzato dal debugger per eseguire il confronto con il checksum calcolato per il file di origine.  
  
 Questa soluzione non funziona per i progetti [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)], poiché il checksum calcolato si riferisce al file di origine generato piuttosto che al file ASPX.  Per risolvere questo problema, `#pragma checksum` fornisce supporto per il checksum nelle pagine [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
 Quando si crea un progetto [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] in [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)], il file di origine generato contiene un checksum per il file ASPX, dal quale viene generata l'origine.  Queste informazioni vengono quindi scritte dal compilatore nel file PDB.  
  
 Se il compilatore non rileva alcuna direttiva `#pragma checksum` nel file, calcola il checksum e scrive il valore nel file PDB.  
  
## Esempio  
  
```  
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{3673e4ca-6098-4ec1-890f-8fceb2a794a2}" "{012345678AB}" // New checksum  
    }  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)