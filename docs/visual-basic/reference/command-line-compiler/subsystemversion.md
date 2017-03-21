---
title: /subsystemversion (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /subsystemversion compiler option [Visual Basic]
- -subsystemversion compiler option [Visual Basic]
- subsystemversion compiler option [Visual Basic]
ms.assetid: 08be22b2-f447-4cd3-8203-120b1b920b54
caps.latest.revision: 9
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
ms.openlocfilehash: bc9ea6a844fae7f98315e5d3557fdf306f467dd5
ms.lasthandoff: 03/13/2017

---
# <a name="subsystemversion-visual-basic"></a>/subsystemversion (Visual Basic)
Specifica la versione minima del sottosistema in cui è possibile eseguire il file eseguibile generato, in modo da determinare le versioni di Windows in cui è possibile eseguire il file eseguibile. In genere, questa opzione assicura che il file eseguibile può sfruttare le funzionalità di protezione che non sono disponibili con le versioni precedenti di Windows.  
  
> [!NOTE]
>  Per specificare il sottosistema di se stesso, utilizzare il [/destinazione](../../../csharp/language-reference/compiler-options/target-compiler-option.md) l'opzione del compilatore.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
/subsystemversion:major.minor  
```  
  
#### <a name="parameters"></a>Parametri  
 `major.minor`  
 La versione minima del sottosistema, espresso in una notazione del punto per le versioni principali e secondarie. Ad esempio, è possibile specificare che un'applicazione non può eseguire su un sistema operativo precedente a Windows 7 Se si imposta il valore di questa opzione su 6.01, come descritto nella tabella più avanti in questo argomento. È necessario specificare i valori per `major` e `minor` come numeri interi.  
  
 Gli zero iniziali di `minor` versione non modifica la versione, ma si gli zeri finali. Ad esempio, 6.1 e 6.01 si riferiscono alla stessa versione, ma 6.10 fa riferimento a una versione diversa. È consigliabile esprimere la versione secondaria con due cifre per evitare confusione.  
  
## <a name="remarks"></a>Note  
 Nella tabella seguente sono elencate le versioni di sottosistema comune di Windows.  
  
|Versione di Windows|Versione del sottosistema|  
|---------------------|-----------------------|  
|Windows 2000|5.00|  
|Windows XP|5.01|  
|Windows Server 2003|5.02|  
|Windows Vista|6.00|  
|Windows 7|6.01|  
|Windows Server 2008|6.01|  
|[!INCLUDE[win8](../../../csharp/language-reference/compiler-options/includes/win8_md.md)]|6.02|  
  
## <a name="default-values"></a>Valori predefiniti  
 Il valore predefinito di **/subsystemversion** l'opzione del compilatore dipende dalle condizioni elencate di seguito:  
  
-   Il valore predefinito è 6.02 se è impostata un'opzione del compilatore nell'elenco seguente:  
  
    -   [/target: appcontainerexe](../../../visual-basic/reference/command-line-compiler/target.md)  
  
    -   [/target: winmdobj](../../../visual-basic/reference/command-line-compiler/target.md)  
  
    -   [/platform:ARM](../../../visual-basic/reference/command-line-compiler/platform.md)  
  
-   Il valore predefinito è 6.00 se si utilizza MSBuild, destinazione [!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net_v45_md.md)], e non è stata impostata una delle opzioni del compilatore che sono state specificate in precedenza in questo elenco.  
  
-   Il valore predefinito è 4.00 se nessuna di queste condizioni è vera.  
  
## <a name="setting-this-option"></a>Impostazione di questa opzione  
 Per impostare il **/subsystemversion** l'opzione del compilatore in Visual Studio, è necessario aprire il file VBPROJ e specificare un valore per la `SubsystemVersion` proprietà nel codice XML di MSBuild. È possibile impostare questa opzione nell'IDE di Visual Studio. Per ulteriori informazioni, vedere "Valori predefiniti" più indietro in questo argomento o [proprietà di progetto MSBuild comuni](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties).  
  

  
## <a name="see-also"></a>Vedere anche  
[Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)

[Proprietà di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-properties)

