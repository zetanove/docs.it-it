---
title: "Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico | Microsoft Docs"
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
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "assembly [.NET Framework], reindirizzamento dell'associazione"
  - "esecuzione affiancata, reindirizzamento dell'associazione di assembly"
ms.assetid: 5fca42f3-bdce-4b81-a704-61e42c89d3ba
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico
A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], quando si compilano app destinate a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], i reindirizzamenti di associazione possono essere aggiunti automaticamente al file di configurazione dell'app per eseguire l'override dell'unificazione degli assembly.  I reindirizzamenti di associazione vengono aggiunti se l'app o i relativi componenti fanno riferimento a più di una versione dello stesso assembly, anche se è possibile specificare manualmente i reindirizzamenti di associazione nel file di configurazione dell'app.  La funzionalità di reindirizzamento di associazione automatica interessa le app desktop e Web tradizionali destinate a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], anche se il comportamento è leggermente diverso per un'app Web.  È possibile abilitare il reindirizzamento di associazione automatico se sono presenti app destinate alle versioni precedenti di .NET Framework o per mantenere i reindirizzamenti di associazione creati manualmente.  
  
## Disabilitazione dei reindirizzamenti di associazione automatici nelle app desktop  
 I reindirizzamenti di associazione automatici sono abilitati per impostazione predefinita per le app desktop tradizionali destinate a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] e versioni successive.  I reindirizzamenti di associazione vengono aggiunti al file di configurazione di output \(app.config\) quando l'applicazione viene compilata ed eseguire l'override dell'unificazione degli assembly che in caso contrario potrebbe essere eseguito.  Il file app.config di origine non viene modificato.  È possibile disabilitare questa funzionalità modificando il file di progetto per l'app.  
  
#### Per disabilitare i reindirizzamenti di associazione automatici  
  
1.  In Visual Studio selezionare il progetto in **Esplora soluzioni**, quindi scegliere **Apri cartella in Esplora file** dal menu di scelta rapida.  
  
2.  In Esplora file trovare il file di progetto \(con estensione CSPROJ o VBPROJ\) e aprirlo in Blocco note.  
  
3.  Nel file di progetto trovare la voce di proprietà seguente:  
  
     `<AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>`  
  
4.  Modificare `true` in `false`:  
  
     `<AutoGenerateBindingRedirects>false</AutoGenerateBindingRedirects>`  
  
## Abilitazione dei reindirizzamenti di associazione manuali  
 È possibile abilitare reindirizzamenti di associazione automatici nelle app esistenti destinate alle versioni precedenti di .NET Framework o nei casi in cui non viene automaticamente richiesto di aggiungere un reindirizzamento.  Se si usa una versione più recente di .NET Framework ma non viene automaticamente richiesto di aggiungere un reindirizzamento, verrà visualizzato un output della compilazione in cui viene suggerito di rimappare gli assembly.  
  
#### Per aggiungere manualmente una proprietà di reindirizzamento di associazione automatico  
  
1.  In Visual Studio selezionare il progetto in **Esplora soluzioni**, quindi scegliere **Apri cartella in Esplora file** dal menu di scelta rapida.  
  
2.  In Esplora file trovare il file di progetto \(con estensione CSPROJ o VBPROJ\) e aprirlo in Blocco note.  
  
3.  Aggiungere l'elemento seguente al primo gruppo di proprietà di configurazione \(sotto il tag \<PropertyGroup\>\):  
  
     `<AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>`  
  
     Di seguito è illustrato un file di progetto di esempio con l'elemento inserito.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Project ToolsVersion="12.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
      <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" />  
      <PropertyGroup>  
        <Configuration Condition=" '$(Configuration)' == ''     ">Debug</Configuration>  
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>  
        <ProjectGuid>{123334}</ProjectGuid>  
        ...  
        <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>  
      </PropertyGroup>  
    ...  
    </Project>  
  
    ```  
  
4.  Compilare l'app.  
  
## Abilitazione dei reindirizzamenti di associazione automatici nelle app Web  
 I reindirizzamenti di associazione automatici vengono implementati in modo diverso per le app Web.  Poiché il file di configurazione di origine \(web.config\) deve essere modificato per le app Web, i reindirizzamenti di associazione non vengono aggiunti automaticamente al file di configurazione.  Visual Studio notifica, tuttavia, eventuali conflitti di associazione ed è possibile aggiungere reindirizzamenti di associazione per risolverli.  Poiché viene sempre richiesto di aggiungere reindirizzamenti di associazione, non è necessario disabilitare in modo esplicito questa funzionalità per un'app Web.  
  
#### Per aggiungere reindirizzamenti di associazione a un file web.config  
  
1.  In Visual Studio compilare l'app e cercare eventuali avvisi di compilazione.  
  
     ![Avviso di compilazione per conflitti di riferimenti all'assembly](../../../docs/framework/configure-apps/media/clr-assemblyrefwarning.png "CLR\_AssemblyRefWarning")  
  
2.  In caso di conflitti di associazione a livello di assembly, viene visualizzato un avviso.  Fare doppio clic sull'avviso.  \(Tastiera: selezionare l'avviso e premere **INVIO**\).  
  
     Verrà visualizzata una finestra di dialogo che consente di aggiungere automaticamente i reindirizzamenti di associazione necessari al file web.config di origine.  
  
     ![Finestra di dialogo dell'autorizzazione reindirizzamento associazione](../../../docs/framework/configure-apps/media/clr-addbindingredirect.png "CLR\_AddBindingRedirect")  
  
## Vedere anche  
 [Elemento \<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md)   
 [Reindirizzamento delle versioni di assembly](../../../docs/framework/configure-apps/redirect-assembly-versions.md)