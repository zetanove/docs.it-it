---
title: "Elemento &lt;compiler&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#compiler"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers/compiler"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<compiler> (elemento)"
  - "attributi di configurazione del compilatore"
  - "elementi di configurazione del compilatore, <compiler> (elemento)"
  - "compiler (elemento)"
ms.assetid: 7a151659-b803-4c27-b5ce-1c4aa0d5a823
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# Elemento &lt;compiler&gt;
Specifica gli attributi di configurazione del compilatore per un provider di linguaggio.  
  
## Sintassi  
  
```  
<compiler  
  language="languageName[;...;...]"  
  extension="fileExtension[;...;...]"  
  type="typeName, assemblyName"  
  warningLevel="number"  
  compilerOptions="option1 option2"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`compilerOptions`|Attributo facoltativo.<br /><br /> Specifica ulteriori argomenti specifici del compilatore per la compilazione.  I valori dell'attributo `compilerOptions` sono in genere elencati in un argomento delle opzioni del compilatore.  Nella documentazione di Visual Studio 2005 è possibile trovare le opzioni del compilatore cercando "opzioni del compilatore" nell'indice.|  
|`extension`|Attributo obbligatorio.<br /><br /> Fornisce un elenco separato da punto e virgola delle estensioni dei file utilizzate dai file di origine del provider di linguaggio.  come ad esempio ".cs".|  
|`language`|Attributo obbligatorio.<br /><br /> Fornisce un elenco separato da punto e virgola di linguaggi supportati dal provider di linguaggio,  come ad esempio "c\#;cs;csharp".|  
|`type`|Attributo obbligatorio.<br /><br /> Specifica il nome del tipo del provider di linguaggio, incluso il nome dell'assembly contenente l'implementazione del provider.  Il nome del tipo deve soddisfare i requisiti definiti in [Specifica di nomi di tipo completi](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|`warningLevel`|Attributo facoltativo.<br /><br /> Specifica il livello avvisi predefinito del compilatore; determina il livello raggiunto il quale il provider del linguaggio gestisce gli avvisi del compilatore come errori.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<providerOption\>](../../../../../docs/framework/configure-apps/file-schema/compiler/provideroption-element.md)|Specifica gli attributi di versione del compilatore per un provider di linguaggio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|[Elemento \<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|Specifica le impostazioni di configurazione del compilatore per i provider di linguaggi disponibili.|  
|[Elemento \<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Contenitore degli elementi di configurazione del compilatore. Contiene o meno elementi `<compiler>`.|  
  
## Note  
 Ciascun elemento `<compiler>` specifica gli attributi di configurazione del compilatore per un provider di linguaggio specifico.  Il provider estende la classe <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=fullName> per un linguaggio specifico. L'elemento `<compiler>` definisce le impostazioni del compilatore e del generatore di codice per il provider di linguaggio.  
  
 In .NET Framework le impostazioni iniziali del compilatore vengono definite nel file di configurazione del computer \(Machine.config\).  Gli sviluppatori e i fornitori di compilatori possono aggiungere impostazioni di configurazione per una nuova implementazione di <xref:System.CodeDom.Compiler.CodeDomProvider>.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> per enumerare a livello di codice le impostazioni di configurazione del compilatore e del provider di linguaggio su un computer.  
  
 Gli elementi del compilatore nei file di configurazione Web o dell'applicazione possono integrare o sostituire le impostazioni nel file di configurazione del computer.  Se sono presenti più implementazioni del provider configurate per lo stesso nome di linguaggio o la stessa estensione di file, l'ultima configurazione corrispondente avrà la precedenza su qualsiasi provider precedentemente configurato per il nome di linguaggio o l'estensione di file.  
  
## File di configurazione  
 Questo elemento può essere utilizzato nel file di configurazione del computer e nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato un elemento di configurazione del compilatore.  
  
```  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler  
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=2.0.3600.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions="/optimize"  
        warningLevel="1" />  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.CodeDom.Compiler.CompilerInfo>   
 <xref:System.CodeDom.Compiler.CodeDomProvider>   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)   
 [Specifying Fully Qualified Type Names](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)   
 [Elemento compiler per compilers per compilation \(schema delle impostazioni ASP.NET\)](http://msdn.microsoft.com/it-it/f7d6b078-5d42-4134-b3f7-62e1aba1df1e)