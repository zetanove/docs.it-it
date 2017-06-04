---
title: "Configurazione del reindirizzamento dell&#39;associazione di assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "assembly [.NET Framework], reindirizzamento dell'associazione"
  - "esecuzione affiancata, reindirizzamento dell'associazione di assembly"
ms.assetid: d266cbd8-bf91-41d1-baf0-afbc481a741f
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Configurazione del reindirizzamento dell&#39;associazione di assembly
Per impostazione predefinita, le applicazioni usano l'insieme di assembly .NET Framework fornito con la versione di runtime usata per compilare l'applicazione.  Per reindirizzare i riferimenti di binding di assembly a una specifica versione degli assembly .NET Framework, è possibile usare l'attributo **appliesTo** dell'elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) di un file di configurazione dell'applicazione.  Questo attributo facoltativo usa un numero di versione di .NET Framework per indicare la versione a cui deve essere applicato.  Se non si specifica alcun attributo **appliesTo**, l'elemento **\<assemblyBinding\>** viene applicato a tutte le versioni di .NET Framework.  
  
 L'attributo **appliesTo** è stato introdotto in .NET Framework versione 1.1 e viene ignorato dalla versione 1.0.  Quando si usa .NET Framework versione 1.0, vengono quindi applicati tutti gli elementi **\<assemblyBinding\>**, anche se viene specificato un attributo **appliesTo**.  
  
> [!NOTE]
>  Usare l'attributo **appliesTo** per limitare il reindirizzamento del binding di assembly a una specifica versione del runtime.  
  
 Ad esempio, per reindirizzare un binding di assembly per un assembly di .NET Framework versione 1.0, è necessario includere il codice XML seguente nel file di configurazione dell'applicazione.  
  
```  
<runtime>  
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
            <dependentAssembly>   
               * assembly information goes here *  
            </dependentAssembly>  
       </assemblyBinding>  
</runtime>  
```  
  
 Gli elementi **\<assemblyBinding\>** vengono elaborati nell'ordine specificato.  È necessario immettere prima le informazioni di reindirizzamento di binding di assembly per gli assembly di .NET Framework versione 1.0, poi le informazioni di reindirizzamento di binding di assembly per gli assembly di .NET Framework versione 1.1.  Immettere infine le informazioni di reindirizzamento dell'binding di assembly per qualsiasi reindirizzamento di assembly .NET Framework in cui non viene usato l'attributo **appliesTo** e che quindi viene applicato a tutte le versioni di .NET Framework.  In caso di conflitto nel reindirizzamento, verrà usata la prima istruzione di reindirizzamento corrispondente nel file di configurazione.  
  
 Per reindirizzare, ad esempio, un riferimento a un assembly di .NET Framework versione 1.0 e un altro riferimento a un assembly di .NET Framework versione 1.1, è possibile usare il modello illustrato nel frammento di codice che segue.  
  
```  
<assemblyBinding xmlns="..." appliesTo="v1.0.3705">   
<! — .NET Framework version 1.0 redirects here. -->   
</assemblyBinding>   
  
<assemblyBinding xmlns="..." appliesTo="v1.1.4322">   
    <! — .NET Framework version 1.1 redirects here. -->   
</assemblyBinding>   
  
<assemblyBinding xmlns="...">   
<!-- Redirects meant for all versions of the .NET Framework. -->   
</assemblyBinding>  
```  
  
## Debug degli errori del file di configurazione  
 I file di configurazione vengono analizzati nel runtime al momento della creazione di un dominio applicazione e vengono quindi caricati in tale dominio applicazione.  In Common Language Runtime, gli errori in un file di configurazione vengono gestiti ignorando la voce che genera l'errore.  Un file di configurazione contenente XML in formato non corretto viene ignorato completamente.   In caso di codice XML non valido, verranno ignorate solo le sezioni non valide.  
  
 È possibile determinare se un file di configurazione viene usato determinando se si verificano reindirizzamenti del binding di assembly.  Per visualizzare gli assembly caricati, usare [Fuslogvw.exe \(Visualizzatore log associazioni assembly\)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md).  Per visualizzare tutte le associazioni di assembly, è necessario impostare una voce per **ForceLog** nel Registro di sistema.  
  
## Vedere anche  
 [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)