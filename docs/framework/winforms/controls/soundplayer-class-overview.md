---
title: "Cenni preliminari sulla classe SoundPlayer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "riproduzione di suoni, SoundPlayer (classe)"
  - "Classe SoundPlayer, informazioni sulla classe SoundPlayer"
  - "riproduzione di suoni"
ms.assetid: fcebb938-62b9-4677-9cbe-6465bc863e22
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sulla classe SoundPlayer
Il <xref:System.Media.SoundPlayer> classe consente di includere facilmente suoni nelle applicazioni.  
  
 Il <xref:System.Media.SoundPlayer> classe consente di riprodurre file audio in formato WAV, da una risorsa o da percorsi UNC o HTTP. Inoltre, il <xref:System.Media.SoundPlayer> classe consente di caricare o riprodurre suoni in modo asincrono.  
  
 È inoltre possibile utilizzare il <xref:System.Media.SystemSounds> classe per riprodurre suoni del sistema comuni, compresi i segnali acustici.  
  
## <a name="commonly-used-properties-methods-and-events"></a>Proprietà utilizzate di frequente, metodi ed eventi  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Media.SoundPlayer.SoundLocation%2A> proprietà|Il percorso del file o l'indirizzo Web dell'audio. I valori accettabili sono UNC o HTTP.|  
|<xref:System.Media.SoundPlayer.LoadTimeout%2A> proprietà|Il numero di millisecondi di attesa per caricare un suono prima genera un'eccezione. Il valore predefinito è 10 secondi.|  
|<xref:System.Media.SoundPlayer.IsLoadCompleted%2A> proprietà|Valore booleano che indica se l'audio è stato caricato.|  
|<xref:System.Media.SoundPlayer.Load%2A> (metodo)|Carica un suono in modo sincrono.|  
|<xref:System.Media.SoundPlayer.LoadAsync%2A> (metodo)|Inizia a caricare in modo asincrono un suono. Una volta completato il caricamento, viene generato il <xref:System.Media.SoundPlayer.OnLoadCompleted%2A> evento.|  
|<xref:System.Media.SoundPlayer.Play%2A> (metodo)|Riproduce il suono specificato nel <xref:System.Media.SoundPlayer.SoundLocation%2A> o <xref:System.Media.SoundPlayer.Stream%2A> in un nuovo thread.|  
|<xref:System.Media.SoundPlayer.PlaySync%2A> (metodo)|Riproduce il suono specificato nel <xref:System.Media.SoundPlayer.SoundLocation%2A> o <xref:System.Media.SoundPlayer.Stream%2A> nel thread corrente.|  
|<xref:System.Media.SoundPlayer.Stop%2A> (metodo)|Arresta un suono.|  
|<xref:System.Media.SoundPlayer.LoadCompleted> evento|Generato dopo il caricamento di un suono.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Media.SoundPlayer>   
 <xref:System.Media.SystemSounds>