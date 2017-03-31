---
title: '#pragma checksum (Riferimento C#) | Documentazione Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#pragma checksum'
dev_langs:
- CSharp
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
caps.latest.revision: 11
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5daf71faea5736036e9e3e0178e84ea03c314ff6
ms.lasthandoff: 03/13/2017

---
# <a name="pragma-checksum-c-reference"></a>#pragma checksum (Riferimenti per C#)
Consente di generare i checksum per i file di origine facilitando in tal modo le operazioni di debug delle pagine [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### <a name="parameters"></a>Parametri  
 `"filename"`  
 Nome del file che richiede il monitoraggio per modifiche o aggiornamenti.  
  
 `"{guid}"`  
 Identificatore univoco globale (GUID, Globally Unique Identifier) del file.  
  
 `"checksum_bytes"`  
 Stringa di cifre esadecimali che rappresenta i byte del checksum. Deve essere un numero pari di cifre esadecimali. Un numero dispari di cifre genera un avviso in fase di compilazione, pertanto la direttiva viene ignorata.  
  
## <a name="remarks"></a>Note  
 Il debugger di Visual Studio usa un checksum per trovare sempre l'origine corretta. Il compilatore calcola il checksum di un file di origine, quindi genera l'output nel file del database di programma (PDB). Il PDB viene quindi usato dal debugger per eseguire il confronto con il checksum calcolato per il file di origine.  
  
 Questa soluzione non funziona per i progetti [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] ASP.NET, poiché il checksum calcolato si riferisce al file di origine generato piuttosto che al file ASPX. Per risolvere questo problema, `#pragma checksum` fornisce supporto per il checksum nelle pagine [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
 Quando si crea un progetto [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] in [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)], il file di origine generato contiene un checksum per il file ASPX, dal quale viene generata l'origine. Queste informazioni vengono quindi scritte dal compilatore nel file PDB.  
  
 Se il compilatore non rileva alcuna direttiva `#pragma checksum` nel file, calcola il checksum e scrive il valore nel file PDB.  
  
## <a name="example"></a>Esempio  
  
```  
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{3673e4ca-6098-4ec1-890f-8fceb2a794a2}" "{012345678AB}" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C#](../../../csharp/language-reference/preprocessor-directives/index.md)
