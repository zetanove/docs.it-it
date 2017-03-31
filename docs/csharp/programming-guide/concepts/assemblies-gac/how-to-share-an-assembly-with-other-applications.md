---
title: 'Procedura: Condividere un assembly con altre applicazioni (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c30e972b-1693-4e05-b115-c31831fdf9f2
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 79397b18b67becf91d04358ea62cb2351be7d252
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-share-an-assembly-with-other-applications-c"></a>Procedura: Condividere un assembly con altre applicazioni (C#)
Gli assembly possono essere privati o condivisi. Per impostazione predefinita, i programmi più semplici sono costituiti da un assembly privato perché non sono destinati ad essere usati in altre applicazioni.  
  
 Per condividerlo con altre applicazioni, un assembly deve essere inserito nella [Global Assembly Cache](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202) (GAC).  
  
### <a name="sharing-an-assembly"></a>Condivisione di un assembly  
  
1.  Creare l'assembly. Per altre informazioni, vedere [Creazione degli assembly](http://msdn.microsoft.com/library/54832ee9-dca8-4c8b-913c-c0b9d265e9a4).  
  
2.  Assegnare all'assembly un nome sicuro. Per altre informazioni, vedere [Procedura: Firmare un assembly con un nome sicuro](http://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67).  
  
3.  Assegnare all'assembly le informazioni sulla versione. Per altre informazioni, vedere [Controllo delle versioni degli assembly](https://msdn.microsoft.com/library/51ket42z).  
  
4.  Aggiungere l'assembly alla Global Assembly Cache. Per altre informazioni, vedere [Procedura: installare un assembly nella Global Assembly Cache](http://msdn.microsoft.com/library/a7e6f091-d02c-49ba-b736-7295cb0eb743).  
  
5.  Accedere ai tipi contenuti nell'assembly da altre applicazioni. Per altre informazioni, vedere [Procedura: Aggiungere un riferimento a un assembly con nome sicuro](http://msdn.microsoft.com/library/4c6a406a-b5eb-44fa-b4ed-4e95bb95a813).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Programmazione con gli assembly](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)
