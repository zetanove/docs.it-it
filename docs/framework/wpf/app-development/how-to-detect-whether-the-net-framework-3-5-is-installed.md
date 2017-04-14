---
title: "Procedura: verificare se .NET Framework 3.5 &#232; installato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 3.5 (rilevamento dell'installazione) [WPF]"
  - "rilevamento dell'installazione di .NET Framework 3.5 [WPF]"
  - "determinazione dell'installazione di .NET Framework 3.5 [WPF]"
  - "verifica dell'installazione di .NET Framework 3.5 [WPF]"
ms.assetid: 8556a9d2-1eb8-48ef-919c-5baf22a2a9a2
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: verificare se .NET Framework 3.5 &#232; installato
Prima di poter distribuire le applicazioni [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] in un sistema con destinazione [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)], gli amministratori devono confermare la presenza del runtime di [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)].  In questo argomento viene fornito uno script HTML\/JavaScript utilizzabile dagli amministratori per determinare se [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] è presente in un sistema.  
  
> [!NOTE]
>  Per informazioni più dettagliate sull'installazione, la distribuzione e il rilevamento di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], vedere [Installazione di .NET Framework](../../../../docs/framework/install/guide-for-developers.md).  
  
## Esempio  
 Quando [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] è installato, MSI aggiunge "CLR .NET" e il numero di versione alla stringa UserAgent.  Nell'esempio seguente viene mostrato uno script incorporato in una semplice pagina HTML.  Lo script consente di cercare la stringa UserAgent per determinare se [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] è installato e, successivamente, consente di visualizzare un messaggio di stato con i risultati della ricerca.  
  
> [!NOTE]
>  Questo script è progettato per Internet Explorer.  Altri browser non possono includere le informazioni di CLR .NET nella stringa UserAgent.  
  
```  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.5</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.5.0.0";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.5."  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.5." +  
          " The required version is v" + dotNETRuntimeVersion + ".";  
      }  
      result.innerText += "\n\nThis machine's userAgent string is: " +   
        navigator.userAgent + ".";  
    }  
  
    //  
    // Retrieve the version from the user agent string and   
    // compare with the specified version.  
    //  
    function HasRuntimeVersion(versionToCheck)  
    {  
      var userAgentString =   
        navigator.userAgent.match(/.NET CLR [0-9.]+/g);  
  
      if (userAgentString != null)  
      {  
        var i;  
  
        for (i = 0; i < userAgentString.length; ++i)  
        {  
          if (CompareVersions(GetVersion(versionToCheck),   
            GetVersion(userAgentString[i])) <= 0)  
            return true;  
        }  
      }  
  
      return false;  
    }  
  
    //  
    // Extract the numeric part of the version string.  
    //  
    function GetVersion(versionString)  
    {  
      var numericString =   
        versionString.match(/([0-9]+)\.([0-9]+)\.([0-9]+)/i);  
      return numericString.slice(1);  
    }  
  
    //  
    // Compare the 2 version strings by converting them to numeric format.  
    //  
    function CompareVersions(version1, version2)  
    {  
      for (i = 0; i < version1.length; ++i)  
      {  
        var number1 = new Number(version1[i]);  
        var number2 = new Number(version2[i]);  
  
        if (number1 < number2)  
          return -1;  
  
        if (number1 > number2)  
          return 1;  
      }  
  
      return 0;  
    }  
  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY>  
    <div id="result" />  
  </BODY>  
</HTML>  
  
```  
  
 Se la ricerca di "CLR .NET " ha esito positivo, viene visualizzato il tipo di messaggio di stato seguente:  
  
 `This machine has the correct version of the .NET Framework 3.5.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; .NET CLR 3.5.20726; MS-RTC LM 8).`  
  
 In caso contrario, viene visualizzato il tipo di messaggio di stato seguente:  
  
 `This machine does not have the correct version of the .NET Framework 3.5.  The required version is v3.5.0.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; MS-RTC LM 8).`  
  
## Vedere anche  
 [Verificare se .NET Framework 3.0 è installato](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)