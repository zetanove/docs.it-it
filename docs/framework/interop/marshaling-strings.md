---
title: "Marshaling Strings | Microsoft Docs"
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
helpviewer_keywords: 
  - "marshaling, samples"
  - "platform invoke, marshaling data"
  - "data marshaling, strings"
  - "data marshaling, samples"
  - "data marshaling, platform invoke"
  - "marshaling. strings"
  - "marshaling, platform invoke"
  - "sample applications [.NET Framework], marshaling strings"
ms.assetid: e21b078b-70fb-4905-be26-c097ab2433ff
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Marshaling Strings
Con platform invoke vengono copiati i parametri di stringa mediante la conversione dal formato .NET Framework \(Unicode\) a quello non gestito, se necessario.  Poiché le stringhe gestite sono immutabili, con platform invoke non vengono copiate di nuovo dalla memoria non gestita a quella gestita al completamento della funzione.  
  
 Nella tabella riportata di seguito sono elencate le opzioni di marshalling per le stringhe, con la descrizione dell'utilizzo e un collegamento all'esempio corrispondente di .NET Framework.  
  
|String|Descrizione|Esempio|  
|------------|-----------------|-------------|  
|Per valore.|Passa le stringhe come parametri in.|[MsgBox](../../../docs/framework/interop/msgbox-sample.md)|  
|Come risultato.|Restituisce le stringhe dal codice non gestito.|[Stringhe](http://msdn.microsoft.com/it-it/be9e82a3-dc95-4aaa-9396-61b66e467e02)|  
|Per riferimento.|Passa le stringhe come parametri in\/out mediante <xref:System.Text.StringBuilder>.|[Buffer](http://msdn.microsoft.com/it-it/e30d36e8-d7c4-4936-916a-8fdbe4d9ffd5)|  
|In una struttura per valore.|Passa le stringhe in una struttura che è un parametro in.|[Strutture](http://msdn.microsoft.com/it-it/96a62265-dcf9-4608-bc0a-1f762ab9f48e)|  
|In una struttura per riferimento **\(char\*\)**.|Passa le stringhe in una struttura che è un parametro in\/out.  Per la funzione non gestita è previsto un puntatore a un buffer di caratteri e la dimensione del buffer è un membro della struttura.|[Stringhe](http://msdn.microsoft.com/it-it/be9e82a3-dc95-4aaa-9396-61b66e467e02)|  
|In una struttura per riferimento **\(char\[\]\)**.|Passa le stringhe in una struttura che è un parametro in\/out.  Per la funzione non gestita è previsto un buffer di caratteri incorporato.|[OSInfo](http://msdn.microsoft.com/it-it/69d89067-507b-41fe-859d-30bf3ff29455)|  
|In una classe per valore **\(char\*\)**.|Passa le stringhe in una classe che è un parametro in\/out.  Per la funzione non gestita è previsto un puntatore a un buffer di caratteri.|[OpenFileDlg](http://msdn.microsoft.com/it-it/b7dea792-cb92-4baf-ac7b-6a24803e6c75)|  
|In una classe per valore **\(char\[\]\)**.|Passa le stringhe in una classe che è un parametro in\/out.  Per la funzione non gestita è previsto un buffer di caratteri incorporato.|[OSInfo](http://msdn.microsoft.com/it-it/69d89067-507b-41fe-859d-30bf3ff29455)|  
|Come matrice di stringhe per valore.|Crea una matrice di stringhe passata come valore.|[Matrici](../../../docs/framework/interop/marshaling-different-types-of-arrays.md)|  
|Come matrice di strutture che contengono stringhe per valore.|Crea una matrice di strutture che contengono stringhe e la matrice viene passata come valore.|[Matrici](../../../docs/framework/interop/marshaling-different-types-of-arrays.md)|  
  
## Vedere anche  
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)   
 [Platform Invoke Data Types](http://msdn.microsoft.com/it-it/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [Marshaling Classes, Structures, and Unions](../../../docs/framework/interop/marshaling-classes-structures-and-unions.md)   
 [Marshaling Arrays of Types](http://msdn.microsoft.com/it-it/049b1c1b-228f-4445-88ec-91bc7fd4b1e8)   
 [Miscellaneous Marshaling Samples](http://msdn.microsoft.com/it-it/a915c948-54e9-4d0f-a525-95a77fd8ed70)