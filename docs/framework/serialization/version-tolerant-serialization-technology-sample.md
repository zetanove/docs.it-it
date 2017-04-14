---
title: "Esempio di tecnologia di serializzazione indipendente dalla versione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2a183664-bfbf-4ff0-96f6-c836284ea916
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Esempio di tecnologia di serializzazione indipendente dalla versione
[Scarica esempio](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/VTS.zip.exe)  
  
 In questo esempio vengono illustrate le funzionalità relative alla tolleranza dalla versione della serializzazione .NET.L'esempio compila applicazioni che, nonostante utilizzino versioni diverse di un oggetto <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> per serializzare e deserializzare i dati,sono in grado di comunicare senza problemi.Per ulteriori informazioni, vedere [Serializzazione a tolleranza di versione](../../../docs/framework/serialization/version-tolerant-serialization.md).  
  
### Per compilare l'esempio utilizzando il prompt dei comandi  
  
1.  Aprire una finestra del prompt dei comandi, quindi spostarsi in una delle sottodirectory specifiche del linguaggio \(in V1 Application o V2 Application\) relative all'esempio.  
  
2.  Digitare **msbuild.exe \<ver\> application.sln** alla riga di comando \(in cui \<ver\> corrisponde a v1 o v2\).  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Aprire [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)], quindi passare a una delle sottodirectory specifiche del linguaggio relative all'esempio.  
  
2.  Spostarsi nella sottodirectory V1 Application della directory selezionata nel passaggio precedente.  
  
3.  Fare doppio clic sull'icona relativa a V1 Application.sln per aprire il file in Visual Studio.  
  
4.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
5.  Spostarsi nella sottodirectory V2 Application e ripetere i due passaggi precedenti per compilare l'applicazione denominata V2 Application.  
  
 Le applicazioni verranno compilate nelle sottodirectory predefinite \\bin o \\bin\\Debug delle rispettive directory di progetto.  
  
### Per eseguire l’esempio  
  
1.  Nella finestra del prompt dei comandi spostarsi nella sottodirectory specifica del linguaggio selezionata durante la compilazione delle applicazioni di esempio.  
  
2.  Digitare **runme.cmd** dalla riga di comando per eseguire entrambe le applicazioni contemporaneamente.  
  
 In alternativa, spostarsi nelle directory contenenti i nuovi eseguibili ed eseguirli in sequenza.  
  
> [!NOTE]
>  L'esempio compila applicazioni console.Per visualizzare l'output delle applicazioni, è necessario avviarle ed eseguirle in una finestra del prompt dei comandi.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>   
 <xref:System.IO.FileStream>