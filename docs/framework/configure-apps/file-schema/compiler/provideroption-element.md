---
title: "Elemento &lt;providerOption&gt; | Microsoft Docs"
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
  - "provideroption"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "elemento <provideroption>"
  - "elemento <provideroption>"
  - "providerOption"
ms.assetid: 014f2e0b-c0b5-4fc4-92d3-73f02978b2a1
caps.latest.revision: 22
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 22
---
# Elemento &lt;providerOption&gt;
Specifica gli attributi di versione del compilatore per un provider di linguaggi.  
  
## Sintassi  
  
```  
<providerOption  
  name="option-name"  
  value="option-value"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo obbligatorio.<br /><br /> Specifica il nome dell'opzione; ad esempio, "CompilerVersion".|  
|`value`|Attributo obbligatorio.<br /><br /> Specifica il valore dell'opzione; ad esempio, "v3.5".|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|È l'elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni per .NET Framework.|  
|[Elemento \<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|Specifica le impostazioni di configurazione del compilatore per i provider di linguaggi disponibili.|  
|[Elemento \<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Contenitore degli elementi di configurazione del compilatore. Contiene o meno elementi `<compiler>`.|  
|[Elemento \<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)|Specifica gli attributi di configurazione del compilatore per un provider di linguaggio.|  
  
## Note  
 In .NET Framework versione 3.5 i provider di codice CodeDOM \(Code Document Object Model\) possono supportare opzioni specifiche del provider utilizzando l'elemento `<providerOption>`.  
  
 In .NET Framework 3.5 sono inclusi gli assembly .NET Framework 2.0 aggiornati e i nuovi assembly versione 3.5 contenenti nuovi tipi.  I provider di codice Microsoft C\# e Visual Basic sono contenuti negli assembly .NET Framework 2.0, che però sono stati aggiornati per supportare i compilatori versione 3.5.  Per impostazione predefinita, i provider di codice aggiornati generano codice per i compilatori versione 2.0.  È possibile utilizzare l'elemento `<providerOption>` per modificare la versione del compilatore di destinazione in 3.5.  Per farlo, specificare "CompilerVersion" per l'attributo `name` e "v3.5" per l'attributo `value`.  È necessario inserire la lettera minuscola "v" prima del numero di versione.  
  
 È possibile rendere globale la specifica della versione aggiungendo l'elemento `<providerOption>` al file Machine.config o al file radice Web.config di .NET Framework 2.0.  Se si aggiorna la versione del compilatore predefinita in 3.5 nel file Machine.config, è possibile modificarla di nuovo in 2.0 per ogni singola applicazione utilizzando l'elemento `<providerOption>` nel file di configurazione dell'applicazione.  
  
 Gli implementatori di provider di codice CodeDOM possono elaborare opzioni personalizzate fornendo un costruttore che accetta un parametro `providerOptions` di tipo <xref:System.Collections.Generic.IDictionary%602>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare l'utilizzo della versione 3.5 del provider di codice C\#.  
  
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
        warningLevel="1" >  
          <providerOption  
            name="CompilerVersion"  
            value="v3.5" />  
      </compiler>  
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