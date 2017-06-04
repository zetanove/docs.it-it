---
title: "Procedura: ospitare un servizio WCF scritto con .NET Framework 3.5 in IIS in esecuzione in .NET Framework 4 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9aabc785-068d-4d32-8841-3ef39308d8d6
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Procedura: ospitare un servizio WCF scritto con .NET Framework 3.5 in IIS in esecuzione in .NET Framework 4
Quando si ospita un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] scritto con [!INCLUDE[netfx35_long](../../../includes/netfx35-long-md.md)] su un computer che esegue [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)], è possibile ottenere un'eccezione <xref:System.ServiceModel.ProtocolException> con il testo indicato di seguito.  
  
```Output  
Eccezione non gestita: System.ServiceModel.ProtocolException: Il tipo di contenuto text/html; charset=utf-8 del messaggio di risposta non corrisponde al tipo di contenuto del binding (application/soap+xml; charset=utf-8).Se si utilizza un codificatore standard, verificare che il metodo IsContentTypeSupported sia implementato correttamente.I primi 1024 byte della risposta erano: '<html>    <head>        <title>Il dominio di applicazione o il pool di applicazioni esegue attualmente .NET Framework 4 o versione successiva.Questa condizione può verificarsi se le impostazioni di IIS sono state configurate per la versione 4.0 o successive per l'applicazione Web in questione o se si utilizza il server di sviluppo Web ASP.NET 4.0 o versione successiva.L'elemento <compilation> nel file Web.config per l'applicazione Web non contiene l'attributo 'targetFrameworkMoniker' necessario per questa versione di .NET Framework (ad esempio, '<compilation targetFrameworkMoniker=".NETFramework,Version=v4.0">').Aggiornare il file Web.config con questo attributo o configurare l'applicazione Web per l'utilizzo di una versione diversa di .NET Framework.</title>...  
```  
  
 Se in alternativa si tenta di passare al file con estensione svc del servizio, è possibile visualizzare una pagina di errore con il testo indicato di seguito.  
  
```Output  
Il dominio dell'applicazione o il pool di applicazioni esegue attualmente .NET Framework 4.0 o versione successiva.Questa condizione può verificarsi se le impostazioni di IIS sono state configurate per la versione 4.0 o successive per l'applicazione Web in questione o se si utilizza il server di sviluppo Web ASP.NET 4.0 o versione successiva.L'elemento <compilation> nel file Web.config per l'applicazione Web non contiene l'attributo 'targetFrameworkMoniker' necessario per questa versione di .NET Framework (ad esempio, '<compilation targetFrameworkMoniker=".NETFramework,Version=v4.0">').Aggiornare il file Web.config con questo attributo o configurare l'applicazione Web per l'utilizzo di una versione diversa di .NET Framework.  
```  
  
 Questi errori si verificano poiché il dominio di applicazione all'interno del quale è in esecuzione IIS esegue [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] e il servizio WCF è in attesa di esecuzione in [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)].In questo argomento vengono illustrate le modifiche necessarie per eseguire il servizio.  
  
 Cercare quindi l'elemento \<`compilers`\> e modificare l'opzione di provider CompilerVersion per ottenere un valore 4.0.Per impostazione predefinita sono presenti due elementi \<`compiler`\> al di sotto dell'elemento \<`compilers`\>.È necessario aggiornare l'opzione di provider CompilerVersion per entrambi gli elementi, come indicato nell'esempio seguente.  
  
```  
<system.codedom>  
      <compilers>  
        <compiler language="c#;cs;csharp" extension=".cs" warningLevel="4"  
                  type="Microsoft.CSharp.CSharpCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
          <providerOption name="CompilerVersion" value="v3.5"/>  
          <providerOption name="WarnAsError" value="false"/>  
        </compiler>  
        <compiler language="vb;vbs;visualbasic;vbscript" extension=".vb" warningLevel="4"  
                  type="Microsoft.VisualBasic.VBCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
          <providerOption name="CompilerVersion" value="v3.5"/>  
          <providerOption name="OptionInfer" value="true"/>  
          <providerOption name="WarnAsError" value="false"/>  
        </compiler>  
      </compilers>  
    </system.codedom>  
```  
  
### Aggiungere l'attributo targetFramework obbligatorio  
  
1.  Aprire il file Web.config del servizio e cercare l'elemento \<`compilation`\>.  
  
2.  Aggiungere l'attributo `targetFramework` all'elemento \<`compilation`\>, come indicato nell'esempio seguente.  
  
    ```  
    <compilation debug="false"  
            targetFramework="4.0">  
  
            <assemblies>  
              <add assembly="System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
              <add assembly="System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
              <add assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35"/>  
              <add assembly="System.Data.DataSetExtensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
            </assemblies>  
  
          </compilation>  
    ```  
  
3.  Cercare l'elemento \<`compilers`\> e modificare l'opzione di provider CompilerVersion per ottenere un valore 4.0.Per impostazione predefinita sono presenti due elementi \<`compiler`\> al di sotto dell'elemento \<`compilers`\>.È necessario aggiornare l'opzione di provider CompilerVersion per entrambi gli elementi, come indicato nell'esempio seguente.  
  
    ```  
    <system.codedom>  
          <compilers>  
            <compiler language="c#;cs;csharp" extension=".cs" warningLevel="4"  
                      type="Microsoft.CSharp.CSharpCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
              <providerOption name="CompilerVersion" value="v3.5"/>  
              <providerOption name="WarnAsError" value="false"/>  
            </compiler>  
            <compiler language="vb;vbs;visualbasic;vbscript" extension=".vb" warningLevel="4"  
                      type="Microsoft.VisualBasic.VBCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
              <providerOption name="CompilerVersion" value="v3.5"/>  
              <providerOption name="OptionInfer" value="true"/>  
              <providerOption name="WarnAsError" value="false"/>  
            </compiler>  
          </compilers>  
        </system.codedom>  
    ```