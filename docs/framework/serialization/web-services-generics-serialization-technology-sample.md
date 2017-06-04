---
title: "Esempio di tecnologia per la serializzazione di generics dei servizi Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cdc15ea4-f678-4729-8ebe-188ae720bef7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Esempio di tecnologia per la serializzazione di generics dei servizi Web
[Scarica esempio](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/GenericsSerialization.zip.exe)  
  
 In questo esempio viene illustrato come utilizzare e controllare la serializzazione di generics nei servizi Web ASP.NET.  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Aprire Visual Studio e scegliere **Nuovo sito Web** dal menu **File**.  
  
2.  Nel riquadro sinistro della finestra **Nuovo sito Web** scegliere il linguaggio di programmazione desiderato, quindi selezionare **Servizio Web ASP.NET** nel riquadro destro.  
  
3.  Fare clic su **Sfoglia** e passare alla sottodirectory \\CS\\GenericsService.  
  
4.  Selezionare il file Service.asmx per aprirlo in Visual Studio.  
  
5.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
> [!NOTE]
>  I primi cinque passaggi di questo elenco sono facoltativi.Il runtime di .NET Framework genererà automaticamente il servizio Web la prima volta che verrà richiesto.  
  
> [!NOTE]
>  Di seguito sono indicati i passaggi necessari per compilare l'esempio.  
  
1.  Aprire [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)], quindi spostarsi nella sottodirectory \\CS.  
  
2.  Fare clic con il pulsante destro del mouse sull'icona della sottodirectory GenericsService, quindi scegliere **Condivisione e sicurezza**.  
  
3.  Nella scheda **Condivisione Web** selezionare **Condividi cartella**.  
  
> [!IMPORTANT]
>  Prendere nota del nome della directory virtuale elencata nel riquadro **Alias** in quanto servirà per eseguire l'esempio.  
  
### Per compilare l'esempio utilizzando Internet Information Services  
  
1.  Aprire lo snap\-in di gestione **Internet Information Services** ed espandere **Siti Web**.  
  
2.  Fare clic con il pulsante sinistro del mouse su **Sito Web predefinito** e selezionare **Nuovo**, quindi **Directory virtuale** per creare la **Creazione guidata Directory virtuale**.  
  
3.  Fare clic su **Avanti**, immettere l'alias pubblico per la directory virtuale e fare clic su **Avanti**.  
  
4.  Immettere il percorso della directory in cui è stato salvato l'esempio \(generalmente la sottodirectory \\CS\\GenericsService\) e fare clic su **Avanti**.Fare clic su **Avanti** per chiudere la procedura guidata.  
  
> [!IMPORTANT]
>  Prendere nota del nome della directory virtuale elencata nel riquadro **Alias** in quanto servirà per eseguire l'esempio.  
  
### Per eseguire l'esempio  
  
1.  Aprire una finestra del browser, quindi fare clic sulla barra degli indirizzi.  
  
2.  Digitare **http:\/\/localhost\/**\[directory virtuale\]**\/Service.asmx**, dove \[directory virtuale\] rappresenta la directory virtuale creata quando è stato compilato l'esempio.  
  
## Note  
 Nell'esempio viene visualizzata una pagina ASP.NET predefinita che contiene collegamenti alla definizione del servizio Web.Oltre a modificare il codice sorgente per il servizio Web, è possibile personalizzare la visualizzazione.Per ulteriori informazioni, vedere [Building XML Web Service Clients](http://msdn.microsoft.com/it-it/c606f3cb-4111-45b4-ae42-9300420fa16c).  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 <xref:System.Web.Services>   
 <xref:System.Xml.Serialization>   
 [Serializzazione](../../../docs/framework/serialization/index.md)   
 [XML Web Services Created Using ASP.NET and XML Web Service Clients](http://msdn.microsoft.com/it-it/1e64af78-d705-4384-b08d-591a45f4379c)