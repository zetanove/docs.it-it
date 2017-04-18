---
title: Il mio dipende dal tipo di progetto (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- _MYTYPE
ms.assetid: c188b38e-bd9d-4121-9983-41ea6a94d28e
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d193dade94980f04b31605ea6fa968f9fa7d0ad6
ms.lasthandoff: 03/13/2017

---
# <a name="how-my-depends-on-project-type-visual-basic"></a>Dipendenza di My dal tipo di progetto (Visual Basic)
`My`espone solo gli oggetti richiesti da un particolare tipo di progetto. Ad esempio, il `My.Forms` oggetto è disponibile in un'applicazione Windows Form, ma non è disponibile in un'applicazione console. Questo argomento viene descritto che `My` gli oggetti sono disponibili in diversi tipi di progetto.  
  
## <a name="my-in-windows-applications-and-web-sites"></a>In Windows le applicazioni e siti Web  
 `My`espone solo gli oggetti che sono utili per il tipo di progetto corrente. esso Elimina gli oggetti che non sono applicabili. Ad esempio, di seguito viene illustrato il `My` modello a oggetti in un progetto Windows Form.  
  
 ![Forma di My in un'applicazione Windows Form](../../../visual-basic/developing-apps/development-with-my/media/myinwinform.png "MyInWinForm")  
  
 In un progetto di sito Web, `My` espone gli oggetti che sono rilevanti per gli sviluppatori Web (ad esempio il `My.Request` e `My.Response` oggetti), eliminando gli oggetti che non sono importanti (ad esempio il `My.Forms` oggetto). La figura seguente mostra il `My` modello a oggetti in un progetto di sito Web:  
  
 ![Forma di My in un'applicazione Web](../../../visual-basic/developing-apps/development-with-my/media/myinweb.png "MyInWeb")  
  
## <a name="project-details"></a>Dettagli di progetto  
 Nella tabella seguente viene illustrato che `My` gli oggetti sono abilitati per impostazione predefinita per otto tipi di progetti: applicazione Windows, libreria di classi, applicazione console, libreria di controlli Windows, libreria di controlli Web, servizio Windows, vuoto e sito Web.  
  
 Sono disponibili tre versioni della `My.Application` oggetto, le due versioni della `My.Computer` oggetto e due versioni di `My.User` dell'oggetto; informazioni dettagliate su queste versioni sono espressi nel piè di pagina dopo la tabella.  
  
|My (oggetto)|Applicazione Windows|Libreria di classi|Applicazione console|Libreria di controlli Windows|Libreria di controlli Web|Servizio Windows|Empty|Sito Web|  
|---|---|---|---|---|---|---|---|---|  
|`My.Application`|**Yes** <sup>1</sup>|**Yes** <sup>2</sup>|**Yes** <sup>3</sup>|**Yes** <sup>2</sup>|No|**Yes** <sup>3</sup>|No|No|  
|`My.Computer`|**Yes** <sup>4</sup>|**Yes** <sup>4</sup>|**Yes** <sup>4</sup>|**Yes** <sup>4</sup>|**Yes** <sup>5</sup>|**Yes** <sup>4</sup>|No|**Yes** <sup>5</sup>|  
|`My.Forms`|**Sì**|No|No|**Sì**|No|No|No|No|  
|`My.Log`|No|No|No|No|No|No|No|**Sì**|  
|`My.Request`|No|No|No|No|No|No|No|**Sì**|  
|`My.Resources`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
|`My.Response`|No|No|No|No|No|No|No|**Sì**|  
|`My.Settings`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
|`My.User`|**Yes** <sup>6</sup>|**Yes** <sup>6</sup>|**Yes** <sup>6</sup>|**Yes** <sup>6</sup>|**Yes** <sup>7</sup>|**Yes** <sup>6</sup>|No|**Yes** <sup>7</sup>|  
|`My.WebServices`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
  
 <sup>1</sup> versione di Windows Form di `My.Application`. Deriva dalla versione console (vedere nota 3); Aggiunge il supporto per l'interazione con le finestre dell'applicazione e fornisce il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modello di applicazione.  
  
 <sup>2</sup> versione della libreria `My.Application`. Fornisce la funzionalità di base necessaria a un'applicazione: fornisce membri per la scrittura nel registro applicazione e l'accesso a informazioni sull'applicazione.  
  
 <sup>3</sup> versione console di `My.Application`. Deriva dalla versione della libreria (vedere nota 2), e aggiunge membri aggiuntivi per l'accesso ad argomenti della riga di comando dell'applicazione e informazioni sulla distribuzione ClickOnce.  
  
 <sup>4</sup> versione di Windows `My.Computer`. Deriva dalla versione del Server (vedere nota 5) e fornisce l'accesso a oggetti utili in un computer client, ad esempio la tastiera, schermo e del mouse.  
  
 <sup>5</sup> versione server di `My.Computer`. Fornisce informazioni di base relative al computer, ad esempio il nome, l'accesso per l'orologio e così via.  
  
 <sup>6</sup> versione di Windows `My.User`. Questo oggetto è associato l'identità del thread corrente.  
  
 <sup>7</sup> versione web del `My.User`. Questo oggetto è associato l'identità dell'utente della richiesta HTTP corrente dell'applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer></xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log></xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User></xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [Personalizzazione degli oggetti sono disponibili in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)   
 [Forms (oggetto)](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [Oggetto My. Request](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [Oggetto My. Response](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [Oggetto My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md)
