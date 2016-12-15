---
title: "-subsystemversion (opzioni del compilatore c#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: a99fce81-9d92-4813-9874-bee777041445
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /subsystemversion (opzioni del compilatore C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica la versione minima del sottosistema in cui è possibile eseguire il file eseguibile generato, in modo da determinare le versioni di Windows in cui è possibile eseguire il file eseguibile. In genere, questa opzione assicura che il file eseguibile può sfruttare le funzionalità di protezione che non sono disponibili con le versioni precedenti di Windows.  
  
> [!NOTE]
>  Per specificare il sottosistema di se stesso, utilizzare il [/destinazione](../../../csharp/language-reference/compiler-options/target-compiler-option.md) l'opzione del compilatore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
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
  
    -   [/target: appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)  
  
    -   [/target: winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)  
  
    -   [/platform:ARM](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)  
  
-   Il valore predefinito è 6.00 se si utilizza MSBuild, destinazione [!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net_v45_md.md)], e non è stata impostata una delle opzioni del compilatore che sono state specificate in precedenza in questo elenco.  
  
-   Il valore predefinito è 4.00 se nessuna di queste condizioni è vera.  
  
## <a name="setting-this-option"></a>Impostazione di questa opzione  
 Per impostare il **/subsystemversion** l'opzione del compilatore in Visual Studio, è necessario aprire il file con estensione csproj e specificare un valore per la `SubsystemVersion` proprietà nel codice XML di MSBuild. È possibile impostare questa opzione nell'IDE di Visual Studio. Per ulteriori informazioni, vedere "Valori predefiniti" più indietro in questo argomento o [proprietà di progetto MSBuild comuni](/visual-studio/msbuild/common-msbuild-project-properties).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni del compilatore c#](../../../csharp/language-reference/compiler-options/index.md)