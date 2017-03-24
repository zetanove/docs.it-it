---
title: /langversion (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
caps.latest.revision: 8
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9970df0c9babc368210169fae0490b423d77f40d
ms.lasthandoff: 03/13/2017

---
# <a name="langversion-visual-basic"></a>/langversion (Visual Basic)
Indica al compilatore di accettare solo la sintassi che è incluso nella versione specificata del linguaggio Visual Basic.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/langversion:version  
```  
  
## <a name="arguments"></a>Argomenti  
 `version`  
 Obbligatorio. La versione della lingua da utilizzare durante la compilazione. Valori accettati sono `9`, `9.0`, `10`, e `10.0`.  
  
## <a name="remarks"></a>Note  
 Il `/langversion` opzione specifica quale il compilatore accetta una sintassi. Ad esempio, se si specifica che la versione in lingua è 9.0, il compilatore genera errori di sintassi che è valida solo nella versione 10.0 e versioni successive.  
  
 È possibile utilizzare questa opzione quando si sviluppano applicazioni che diverse versioni di .NET Framework. Ad esempio, se la destinazione è .NET Framework 3.5, è possibile utilizzare questa opzione per garantire che non si utilizza la sintassi di linguaggio versione 10.0.  
  
 È possibile impostare `/langversion` direttamente solo utilizzando la riga di comando. Per altre informazioni, vedere [Sviluppo per una versione specifica di .NET Framework](https://docs.microsoft.com/visualstudio/ide/targeting-a-specific-dotnet-framework-version).  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `sample.vb` per Visual Basic 9.0.  
  
```  
vbc /langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sviluppo per una versione specifica di .NET Framework](https://docs.microsoft.com/visualstudio/ide/targeting-a-specific-dotnet-framework-version)
