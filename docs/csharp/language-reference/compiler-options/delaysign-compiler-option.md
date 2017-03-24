---
title: "/delaysign (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/delaysign"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-delaysign compiler option [C#]"
  - "delaysign compiler option [C#]"
  - "/delaysign compiler option [C#]"
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# /delaysign (C# Compiler Options)
Specificando questa opzione, il compilatore riserva spazio nel file di output in modo da poter aggiungere in seguito una firma digitale.  
  
## Sintassi  
  
```  
/delaysign[ + | - ]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Utilizzare **\/delaysign\-** se si desidera che l'assembly abbia firma completa.  Utilizzare **\/delaysign\+** se si desidera inserire nell'assembly solo la chiave pubblica.  Il valore predefinito è **\/delaysign\-**.  
  
## Note  
 L'opzione **\/delaysign** ha effetto solo se utilizzata con [\/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) o [\/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md).  
  
 Quando si richiede un assembly completamente firmato, il compilatore genera un hash per il file che contiene il manifesto, o metadati dell'assembly, e quindi firma l'hash risultante con la chiave privata.  La firma digitale risultante viene archiviata nel file contenente il manifesto.  Se per un assembly si utilizza una firma posticipata, la firma non verrà elaborata e quindi memorizzata dal compilatore, ma verrà riservato uno spazio nel file in modo che la firma possa essere aggiunta successivamente.  
  
 Ad esempio, l'utilizzo di **\/delaysign\+** consente a un tester di inserire l'assembly nella Global Assembly Cache.  Al termine del test sarà possibile apporre una firma completa all'assembly inserendo la chiave privata mediante l'utilità [Assembly Linker](../Topic/Al.exe%20\(Assembly%20Linker\).md).  
  
 Per ulteriori informazioni, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md) e [Ritardo della firma di un assembly](../Topic/Delay%20Signing%20an%20Assembly.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Modificare la proprietà **Solo firma ritardata**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)