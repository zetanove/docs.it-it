---
title: "Procedura: configurare IIS 5.0 e IIS 6.0 per distribuire applicazioni WPF | Microsoft Docs"
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
  - "regolazione dell'impostazione di scadenza del contenuto"
  - "applicazioni, distribuzione"
  - "configurazione di server Web per la distribuzione di applicazioni WPF"
  - "impostazione di scadenza del contenuto, regolazione"
  - "distribuzione di applicazioni"
  - "estensioni file, registrazione"
  - "MIME (tipi), registrazione"
  - "registrazione di estensioni di file"
  - "registrazione di tipi MIME"
  - "server Web, configurazione per la distribuzione di applicazioni WPF"
ms.assetid: c6e8c2cb-9ba2-4e75-a0d5-180ec9639433
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: configurare IIS 5.0 e IIS 6.0 per distribuire applicazioni WPF
È possibile distribuire un'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] dalla maggior parte dei server Web, purché siano configurati con i tipi [!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] appropriati.  Per impostazione predefinita, [!INCLUDE[TLA#tla_iis70](../../../../includes/tlasharptla-iis70-md.md)] è configurato con questi tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)], tuttavia [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] e [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] non lo sono.  
  
 In questo argomento viene illustrato come configurare [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] e [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] per distribuire le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
> [!NOTE]
>  È possibile controllare la stringa *UserAgent* nel Registro di sistema per determinare se in un sistema è installato [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)].  Per informazioni dettagliate e uno script che esamina la stringa *UserAgent* da determinare se [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] è installato in un sistema, vedere [Verificare se .NET Framework 3.0 è installato](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md).  
  
<a name="content_expiration"></a>   
## Regolare l'impostazione di scadenza del contenuto  
 È necessario regolare l'impostazione della scadenza del contenuto su 1 minuto.  Di seguito viene illustrato come eseguire questa operazione con [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)].  
  
1.  Fare clic sul menu **Start**, scegliere **Strumenti di amministrazione**, quindi fare clic su **Gestione Internet Information Services \(IIS\)**.  È anche possibile avviare questa applicazione dalla riga di comando con "%SystemRoot%\\system32\\inetsrv\\iis.msc".  
  
2.  Espandere la struttura ad albero di [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)] fino a trovare il nodo **Sito Web predefinito**.  
  
3.  Fare clic con il pulsante destro del mouse su **Sito Web predefinito** e scegliere **Proprietà** dal menu di scelta rapida.  
  
4.  Selezionare la scheda **Intestazioni HTTP** e fare clic su "Abilita scadenza contenuto"  
  
5.  Impostare il contenuto in modo che scada dopo 1 minuto.  
  
<a name="register_mime_types"></a>   
## Registrare tipi MIME ed estensioni file  
 Per consentire al browser del sistema del client di caricare il gestore corretto, è necessario registrare diversi tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] ed estensioni file.  È necessario aggiungere i seguenti tipi:  
  
|Estensione|Tipo MIME|  
|----------------|---------------|  
|.manifest|application\/manifest|  
|.xaml|application\/xaml\+xml|  
|.application|application\/x\-ms\-application|  
|.xbap|application\/x\-ms\-xbap|  
|deploy|application\/octet\-stream|  
|.xps|application\/vnd.ms\-xpsdocument|  
  
> [!NOTE]
>  Non è necessario registrare tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] o estensioni file nei sistemi client.  Questi vengono registrati automaticamente quando si installa [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)].  
  
 Nell'esempio [!INCLUDE[TLA#tla_visualbscrpt](../../../../includes/tlasharptla-visualbscrpt-md.md)] seguente i tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] necessari vengono aggiunti automaticamente a [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)].  Per utilizzare lo script, copiare il codice in un file vbs sul server.  Quindi, eseguire lo script eseguendo il file dalla riga di comando oppure facendo doppio clic sul file in [!INCLUDE[TLA#tla_winexpl](../../../../includes/tlasharptla-winexpl-md.md)].  
  
```  
' This script adds the necessary Windows Presentation Foundation MIME types   
' to an IIS Server.  
' To use this script, just double-click or execute it from a command line.  
' Running this script multiple times results in multiple entries in the IIS MimeMap.  
  
Dim MimeMapObj, MimeMapArray, MimeTypesToAddArray, WshShell, oExec  
Const ADS_PROPERTY_UPDATE = 2   
  
' Set the MIME types to be added  
MimeTypesToAddArray = Array(".manifest", "application/manifest", ".xaml", _  
    "application/xaml+xml", ".application", "application/x-ms-application", _  
    ".deploy", "application/octet-stream", ".xbap", "application/x-ms-xbap", _  
    ".xps", "application/vnd.ms-xpsdocument")   
  
' Get the mimemap object   
Set MimeMapObj = GetObject("IIS://LocalHost/MimeMap")  
  
' Call AddMimeType for every pair of extension/MIME type  
For counter = 0 to UBound(MimeTypesToAddArray) Step 2  
    AddMimeType MimeTypesToAddArray(counter), MimeTypesToAddArray(counter+1)  
Next  
  
' Create a Shell object  
Set WshShell = CreateObject("WScript.Shell")  
  
' Stop and Start the IIS Service  
Set oExec = WshShell.Exec("net stop w3svc")  
Do While oExec.Status = 0  
    WScript.Sleep 100  
Loop  
  
Set oExec = WshShell.Exec("net start w3svc")  
Do While oExec.Status = 0  
    WScript.Sleep 100  
Loop  
  
Set oExec = Nothing  
  
' Report status to user  
WScript.Echo "Windows Presentation Foundation MIME types have been registered."  
  
' AddMimeType Sub  
Sub AddMimeType (Ext, MType)  
  
    ' Get the mappings from the MimeMap property.   
    MimeMapArray = MimeMapObj.GetEx("MimeMap")   
  
    ' Add a new mapping.   
    i = UBound(MimeMapArray) + 1   
    Redim Preserve MimeMapArray(i)   
    Set MimeMapArray(i) = CreateObject("MimeMap")   
    MimeMapArray(i).Extension = Ext   
    MimeMapArray(i).MimeType = MType   
    MimeMapObj.PutEx ADS_PROPERTY_UPDATE, "MimeMap", MimeMapArray  
    MimeMapObj.SetInfo  
  
End Sub  
```  
  
> [!NOTE]
>  Se lo script viene eseguito più volte, vengono create voci di mappa [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] multiple nella metabase [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] o [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)].  
  
 Dopo avere eseguito questo script, potrebbe non essere possibile visualizzare tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] aggiuntivi da [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] o [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)][!INCLUDE[TLA#tla_mmc](../../../../includes/tlasharptla-mmc-md.md)].  Tuttavia, questi tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] sono stati aggiunti alla metabase [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] o [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)].  Mediante lo script seguente saranno visualizzati tutti i tipi [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] della metabase [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] o [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)].  
  
```  
' This script lists the MIME types for an IIS Server.  
' To use this script, just double-click or execute it from a command line   
' by calling cscript.exe  
  
dim mimeMapEntry, allMimeMaps  
  
' Get the mimemap object.  
Set mimeMapEntry = GetObject("IIS://localhost/MimeMap")  
allMimeMaps = mimeMapEntry.GetEx("MimeMap")  
  
' Display the mappings in the table.  
For Each mimeMap In allMimeMaps  
    WScript.Echo(mimeMap.MimeType & " (" & mimeMap.Extension + ")")  
Next  
```  
  
 Salvare lo script come file `.vbs` \(ad esempio, `DiscoverIISMimeTypes.vbs`\) ed eseguirlo dal prompt dei comandi utilizzando il comando seguente:  
  
 `cscript DiscoverIISMimeTypes.vbs`