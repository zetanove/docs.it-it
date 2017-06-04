---
title: "Generazione di classi di tipo dati da XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4e5e4e8-527f-44d1-92fa-8904a08784ea
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Generazione di classi di tipo dati da XML
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] include una nuova funzionalità per generare classi di tipi di dati da XML.  In questo argomento viene descritto come generare automaticamente tipi di dati per il feed RSS di MSDN Library.  
  
### Acquisizione del codice XML dal feed RSS di MSDN Library  
  
1.  In Internet Explorer passare al [feed RSS di MSDN](http://go.microsoft.com/fwlink/?LinkId=225209).  
  
2.  Fare clic con il pulsante destro del mouse sulla pagina e scegliere **Visualizza origine**.  
  
3.  Copiare il testo del feed premendo **CTRL\+A** per selezionare tutto il testo e **CTRL\+C** per effettuare la copia.  
  
### Creazione dei tipi di dati  
  
1.  Aprire un file di codice in cui deve essere usato il proxy.  Questo file deve far parte di un progetto [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  
  
2.  Posizionare il cursore nel file ma all'esterno di a qualsiasi classe esistente.  
  
3.  Selezionare **Modifica**, **Incolla speciale**, **Incolla XML come classi**.  
  
4.  Le classi denominate `rss`, `rssChannel`, `rssChannelImage` e `rssChannelItem` vengono create con i membri necessari per accedere agli elementi nel feed RSS.  
  
### Uso delle classi generate  
  
1.  Una volta generate, le classi possono essere usate nel codice come qualsiasi altra classe.  Nell'esempio di codice seguente viene restituita una nuova istanza della classe `rssChannelImage`.  
  
    ```  
    var channelImage = new rssChannelImage()   
    {   
        title = "MyImage",   
        link = "http://www.contoso.com/images/channelImage.jpg",   
        url = "http://www.contoso.com/entries/myEntry.html"   
    };  
  
    ```