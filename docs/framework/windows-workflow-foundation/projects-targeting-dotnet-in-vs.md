---
title: "Scrittura di progetti destinati a .NET Framework 3.0 e 3.5 in Visual Studio 2010 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 81858ab7-763c-4eac-83fe-d7205e5c4c98
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Scrittura di progetti destinati a .NET Framework 3.0 e 3.5 in Visual Studio 2010
È possibile utilizzare [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] per creare progetti destinati a [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versione 3.0 o 3.5.In questo argomento viene descritto come eseguire questa operazione.  
  
> [!NOTE]
>  Quando si aggiungono attività, verificare che venga impostata la versione desiderata di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].Se si modifica la versione di destinazione del flusso di lavoro dopo l'aggiunta delle attività, non sarà possibile convalidare il flusso di lavoro.  
  
> [!WARNING]
>  L'apertura di flussi di lavoro esistenti in [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] in cui sono presenti attività di .NET Framework 3.5 provocherà un errore in `this.SetValue()`.Per aprire progetti creati con versioni precedenti di .NET Framework, aprire prima un flusso di lavoro vuoto nella finestra di progettazione, quindi aggiungere un'attività .NET Framework 3.5.  
  
## Per creare un progetto .NET Framework 3.0 o 3.5 in Visual Studio 2010  
  
1.  Aprire [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
3.  Nell'elenco a discesa nella parte superiore della finestra di dialogo selezionare la versione desiderata di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## Per aggiornare la versione di destinazione di .NET Framework  
  
1.  Fare clic con il pulsante destro del mouse in Esplora soluzioni, quindi scegliere **Proprietà**.  
  
2.  Nell'elenco a discesa **Versione .NET Framework di destinazione** selezionare la versione desiderata.