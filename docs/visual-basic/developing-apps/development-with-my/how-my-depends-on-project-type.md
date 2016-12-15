---
title: "How My Depends on Project Type (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "_MYTYPE"
ms.assetid: c188b38e-bd9d-4121-9983-41ea6a94d28e
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How My Depends on Project Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`My` espone solo gli oggetti richiesti da un particolare tipo di progetto.  Ad esempio, l'oggetto `My.Forms` è disponibile in un'applicazione Windows Form ma non è disponibile in un'applicazione console.  In questo argomento vengono descritti gli oggetti `My` disponibili nei differenti tipi di progetto.  
  
## My nelle applicazioni Windows e nei siti Web  
 `My` espone solo gli oggetti utili nel tipo di progetto corrente ed elimina gli oggetti non applicabili.  Ad esempio, nella seguente immagine è illustrato il modello a oggetti `My` in un progetto Windows Form.  
  
 ![Struttura di My in un'applicazione Windows Form](../../../visual-basic/developing-apps/development-with-my/media/myinwinform.png "MyInWinForm")  
  
 In un progetto di un sito Web, `My` espone gli oggetti rilevanti per uno sviluppatore Web \(ad esempio gli oggetti `My.Request` e `My.Response`\), eliminando gli oggetti irrilevanti \(ad esempio, l'oggetto `My.Forms`\).  Nell'immagine riportata di seguito è illustrato il modello a oggetti `My` in un progetto di un sito Web:  
  
 ![Struttura di My in un'applicazione Web](../../../visual-basic/developing-apps/development-with-my/media/myinweb.png "MyInWeb")  
  
## Dettagli di progetto  
 Nella tabella riportata di seguito sono elencati gli oggetti `My` attivati per impostazione predefinita per otto tipi di progetti: applicazione Windows, Libreria di classi, applicazione console, libreria di controlli Windows, libreria di controlli Web, servizio Windows, vuoto e sito Web.  
  
 Sono presenti tre versioni dell'oggetto `My.Application`, due versioni dell'oggetto `My.Computer` e due versioni dell'oggetto `My.User`. Nelle note in calce alla tabella sono fornite informazioni dettagliate sulle versioni.  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
|Oggetto My|Applicazione Windows|Libreria di classi|Applicazione console|Libreria di controlli Windows|Libreria di controlli Web|Servizio Windows|Vuoto|Sito Web|  
|`My.Application`|**Sì** <sup>1</sup>|**Sì** <sup>2</sup>|**Sì** <sup>3</sup>|**Sì** <sup>2</sup>|No|**Sì** <sup>3</sup>|No|No|  
|`My.Computer`|**Sì** <sup>4</sup>|**Sì** <sup>4</sup>|**Sì** <sup>4</sup>|**Sì** <sup>4</sup>|**Sì** <sup>5</sup>|**Sì** <sup>4</sup>|No|**Sì** <sup>5</sup>|  
|`My.Forms`|**Sì**|No|No|**Sì**|No|No|No|No|  
|`My.Log`|No|No|No|No|No|No|No|**Sì**|  
|`My.Request`|No|No|No|No|No|No|No|**Sì**|  
|`My.Resources`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
|`My.Response`|No|No|No|No|No|No|No|**Sì**|  
|`My.Settings`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
|`My.User`|**Sì** <sup>6</sup>|**Sì** <sup>6</sup>|**Sì** <sup>6</sup>|**Sì** <sup>6</sup>|**Sì** <sup>7</sup>|**Sì** <sup>6</sup>|No|**Sì** <sup>7</sup>|  
|`My.WebServices`|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|**Sì**|No|No|  
  
 <sup>1</sup> Versione Windows Form di `My.Application`.  Deriva dalla versione console \(vedere Nota 3\). Aggiunge supporto per l'interazione con le finestre dell'applicazione e fornisce il modello applicativo di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 <sup>2</sup> Versione libreria di `My.Application`.  Fornisce la funzionalità di base richiesta da un'applicazione: fornisce membri per la scrittura nel registro applicazioni e l'accesso alle informazioni sull'applicazione.  
  
 <sup>3</sup> Versione console di `My.Application`.  Deriva dalla versione libreria \(vedere Nota 2\). Aggiunge ulteriori membri per l'accesso agli argomenti della riga di comando dell'applicazione e alle informazioni di distribuzione di ClickOnce.  
  
 <sup>4</sup> Versione Windows di `My.Computer`.  Deriva dalla versione server \(vedere Nota 5\). Fornisce l'accesso a oggetti utili su un computer client, ad esempio la tastiera, lo schermo e il mouse.  
  
 <sup>5</sup> Versione server di `My.Computer`.  Fornisce informazioni di base sul computer, ad esempio il nome, l'accesso all'orologio e così via.  
  
 <sup>6</sup> Versione Windows di `My.User`.  Questo oggetto è associato all'identità corrente del thread.  
  
 <sup>7</sup> Versione Web di `My.User`.  Questo oggetto è associato all'identità dell'utente della richiesta HTTP corrente dell'applicazione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [Customizing Which Objects are Available in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)   
 [My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.Request Object](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [My.Response Object](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)