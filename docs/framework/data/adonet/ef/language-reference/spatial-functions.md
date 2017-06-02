---
title: "Funzioni spaziali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 90cb177d-88a0-45be-97e8-3b306283c6e0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Funzioni spaziali
Nessun formato letterale per i tipi spaziali.  Tuttavia, è possibile usare le funzioni canoniche di Entity Framework che si chiamano tramite stringhe in formato Well\-Known Text.  Ad esempio, la seguente chiamata di funzione crea un punto di geometria:  
  
```  
GeometryFromText('POINT (43 -73)')  
```  
  
 Nella pagina [Metodi SpatialEdmFunctions](http://msdn.microsoft.com/library/hh749531.aspx) sono elencati tutti i metodi canonici spaziali di Entity Framework.  Fare clic su un metodo per visualizzare i parametri che devono essere passati a una funzione.