---
title: "/resource (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/13/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/resource"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-resource compiler option [C#]"
  - "/resource compiler option [C#]"
  - "-res compiler option [C#]"
  - "/res compiler option [C#]"
  - "res compiler option [C#]"
  - "resource compiler option [C#]"
ms.assetid: 5212666e-98ab-47e4-a497-b5545ab15c7f
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /resource (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Incorpora la risorsa specificata in un file di output.  
  
## Sintassi  
  
```  
/resource:filename[,identifier[,accessibility-modifier]]  
```  
  
## Argomenti  
 `filename`  
 Rappresenta il file di risorse .NET Framework che si desidera incorporare nel file di output.  
  
 `identifier` \(facoltativo\)  
 Nome logico della risorsa, utilizzato per caricare la risorsa stessa.  Il valore predefinito è il nome del file.  
  
 `accessibility-modifier` \(facoltativo\)  
 Rappresenta l'accessibilità della risorsa: public o private.  L'impostazione predefinita è public.  
  
## Note  
 Utilizzare [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md) per collegare una risorsa a un assembly senza aggiungere il file di risorse al file di output.  
  
 Per impostazione predefinita, le risorse sono pubbliche nell'assembly quando vengono create utilizzando il compilatore C\#.  Per renderle private, specificare `private` come modificatore di accessibilità.  Non è consentito alcun valore di accessibilità diverso da `public` o `private`.  
  
 Se `filename` è un file di risorse .NET Framework creato, ad esempio, tramite [Resgen.exe](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) oppure nell'ambiente di sviluppo, sarà accessibile con i membri dello spazio dei nomi <xref:System.Resources>.  Per ulteriori informazioni, vedere <xref:System.Resources.ResourceManager?displayProperty=fullName>.  Per tutte le altre risorse, utilizzare i metodi `GetManifestResource`\* nella classe <xref:System.Reflection.Assembly> per accedere alla risorsa in fase di esecuzione.  
  
 **\/res** rappresenta la versione abbreviata di **\/resource**.  
  
 L'ordine delle risorse nel file di output è determinato dall'ordine specificato nella riga di comando.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aggiungere un file di risorse al progetto.  
  
2.  Selezionare il file che si desidera incorporare in **Esplora soluzioni**.  
  
3.  Nella finestra **Proprietà** selezionare **Operazione di compilazione** per il file.  
  
4.  Impostare **Operazione di compilazione** su **Risorsa incorporata**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.FileProperties2.BuildAction%2A>.  
  
## Esempio  
 Compilare `in.cs` e allegare il file di risorse `rf.resource`:  
  
```  
csc /resource:rf.resource in.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)