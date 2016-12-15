---
title: "/appconfig (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/appconfig"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/appconfig compiler option [C#]"
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /appconfig (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione del compilatore **\/appconfig** consente a un'applicazione C\# di specificare il percorso del file di configurazione dell'applicazione \(app.config\) di un assembly al Common Language Runtime \(CLR\) all'ora dell'associazione dell'assembly.  
  
## Sintassi  
  
```  
/appconfig:file  
```  
  
## Argomenti  
 `file`  
 Obbligatorio.  File di configurazione dell'applicazione che contiene le impostazioni di associazione degli assembly.  
  
## Note  
 Un utilizzo di **\/appconfig** sono gli scenari avanzati nei quali un assembly deve fare contemporaneamente riferimento alla versione sia di .NET Framework sia di .NET Framework per Silverlight di un particolare assembly di riferimento.  Ad esempio, una finestra di progettazione XAML scritta in Windows Presentation Foundation \(WPF\) potrebbe dovere fare riferimento sia al Desktop WPF, per l'interfaccia utente della finestra di progettazione che al sottoinsieme di WPF incluso con Silverlight.  Lo stesso assembly della finestra di progettazione deve accedere a entrambi gli assembly.  Per impostazione predefinita, i riferimenti separati provocano un errore del compilatore, perché l'associazione di assembly vede i due assembly come equivalenti.  
  
 L'opzione del compilatore **\/appconfig** consente di specificare il percorso di un file app.config che disabilita il comportamento predefinito tramite un tag `<supportPortability>`, come illustrato nell'esempio seguente.  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 Il compilatore passa il percorso del file alla logica di associazione degli assembly del CLR.  
  
> [!NOTE]
>  Se si esegue la compilazione dell'applicazione tramite Microsoft Build Engine \(MSBuild\), è possibile impostare l'opzione del compilatore **\/appconfig** aggiungendo una tag di proprietà al file .csproj.  Per utilizzare il file app.config già impostato nel progetto, aggiungere il tag della proprietà `<UseAppConfigForCompiler>` al file .csproj e impostare il relativo valore su `true`.  Per specificare un file app.config diverso, aggiungere il tag `<AppConfigForCompiler>` della proprietà e impostare il relativo valore in corrispondenza della posizione del file.  
  
## Esempio  
 Nell'esempio seguente viene mostrato un file app.config che consente a un'applicazione di avere riferimenti sia all'implementazione di .NET Framework sia all'implementazione di .NET Framework for Silverlight di qualsiasi assembly di .NET Framework presente in entrambe le implementazioni.  L'opzione del compilatore **\/appconfig** consente di specificare il percorso di questo file app.config.  
  
```  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [.NET Framework Assembly Unification Overview](http://msdn.microsoft.com/it-it/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)   
 [Elemento \<supportPortability\>](../Topic/%3CsupportPortability%3E%20Element.md)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)