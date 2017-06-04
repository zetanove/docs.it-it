---
title: "Elemento &lt;system.codedom&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.codedom"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<system.codedom> (elemento)"
  - "elementi di configurazione del compilatore, <system.codedom> (elemento)"
  - "system.codedom (elemento)"
ms.assetid: 672a68f7-e69f-4479-ac30-e980085ec4fe
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Elemento &lt;system.codedom&gt;
Specifica le impostazioni di configurazione del compilatore per i provider di linguaggi disponibili.  
  
## Sintassi  
  
```  
<system.codedom>  
  <compilers> ... </compilers>  
</system.codedom>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<compilatori\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Il contenitore degli elementi di configurazione del compilatore; contiene zero o più elementi [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<configurazione\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Note  
  
## .NET Framework versione 2.0  
 L'elemento [\<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md) contiene impostazioni di configurazione del compilatore per i provider di linguaggi installati in un computer oltre ai provider predefiniti installati con .NET Framework, come <xref:Microsoft.CSharp.CSharpCodeProvider> e <xref:Microsoft.VisualBasic.VBCodeProvider>.  L'elemento [\<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) contiene zero o più elementi [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).  Ciascun elemento [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) specifica gli attributi di configurazione del compilatore per un provider di linguaggi specifico.  
  
 Gli sviluppatori e i fornitori di compilatori possono aggiungere impostazioni di configurazione al file di configurazione del computer \(Machine.config\) per una nuova implementazione di <xref:System.CodeDom.Compiler.CodeDomProvider>.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> per enumerare a livello di codice sia i provider di linguaggi predefiniti che i provider di linguaggi identificati dalle impostazioni di configurazione del compilatore su un computer.  
  
> [!NOTE]
>  In .NET Framework versioni 1.0 e 1.1 i provider di linguaggi predefiniti forniti da .NET Framework sono identificati dall'elemento [\<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md).  In .NET Framework versione 2.0 i provider di linguaggi predefiniti sono identificati dall'elemento [\<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) ma possono essere enumerati utilizzando il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A>.  
  
## .NET Framework versioni 1.0 e 1.1  
 L'elemento [\<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md) contiene le impostazioni di configurazione del compilatore per i provider di linguaggi su un computer.  L'elemento [\<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) contiene zero o più elementi [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).  Ciascun elemento [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) specifica gli attributi di configurazione del compilatore per un provider di linguaggi specifico.  
  
 In .NET Framework le impostazioni iniziali del compilatore vengono definite nel file di configurazione del computer \(Machine.config\).  Gli sviluppatori e i fornitori di compilatori possono aggiungere impostazioni di configurazione per una nuova implementazione di <xref:System.CodeDom.Compiler.CodeDomProvider>.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> per enumerare a livello di codice le impostazioni di configurazione del compilatore e del provider di linguaggio su un computer.  
  
## File di configurazione  
 Questo elemento può essere utilizzato nel file di configurazione del computer e nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una configurazione tipica del compilatore.  
  
```  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler   
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=1.0.5000.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions=""  
        warningLevel="1" />  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.CodeDom.Compiler.CompilerInfo>   
 <xref:System.CodeDom.Compiler.CodeDomProvider>   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Schema di impostazioni del compilatore e del provider di linguaggi](../../../../../docs/framework/configure-apps/file-schema/compiler/index.md)   
 [Elemento \<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)