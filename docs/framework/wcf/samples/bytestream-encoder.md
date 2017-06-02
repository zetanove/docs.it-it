---
title: "Codificatore ByteStream | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e674a8ab-f79a-4a93-b984-54b34392dafc
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Codificatore ByteStream
In questo esempio descritto come creare una `ByteStreamHttpBinding`, una <xref:System.ServiceModel.Channels.Binding> che dimostra la funzionalità del codificatore del flusso di byte.  
  
## Discussione  
 In questo esempio viene descritto come creare un oggetto <xref:System.ServiceModel.Channels.Binding> standard usando gli elementi di associazione standard <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.HttpTransportBindingElement>.  In questo esempio viene illustrato come usare il codificatore del flusso di byte per caricare e scaricare un'immagine.  La funzionalità di codificatore del flusso di byte supporta solo il trasporto HTTP e non supporta funzionalità quali la messaggistica affidabile o la sicurezza.  L'unica <xref:System.ServiceModel.Channels.MessageVersion> supportata è <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.  
  
> [!IMPORTANT]
>  Se si esegue questo esempio in [!INCLUDE[windowsver](../../../../includes/windowsver-md.md)] o [!INCLUDE[win7_client_firstref](../../../../includes/win7-client-firstref-md.md)], verificare di eseguire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi elevati.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Binding\ByteStreamEncoder`  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire il file ByteStreamHttpBinding.sln in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Avviare una nuova istanza del progetto ByteStreamHttpBindingServer facendo clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliendo **Debug**, quindi **Avvia nuova istanza** dal menu di scelta rapida.  
  
3.  Avviare una nuova istanza del progetto ByteStreamHttpBindingClient facendo clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliendo **Debug**, quindi **Avvia nuova istanza** dal menu di scelta rapida.