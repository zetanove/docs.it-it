---
title: Personalizzazione degli oggetti sono disponibili in My (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
caps.latest.revision: 12
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
ms.openlocfilehash: 6791398270e4348adf356eb36a385bfbefde873c
ms.lasthandoff: 03/13/2017

---
# <a name="customizing-which-objects-are-available-in-my-visual-basic"></a>Personalizzazione degli oggetti disponibili in My (Visual Basic)
Questo argomento viene descritto come è possibile controllare quali `My` gli oggetti vengono abilitati mediante l'impostazione del progetto `_MYTYPE` costante di compilazione condizionale. Il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] ambiente di sviluppo integrato (IDE) mantiene la `_MYTYPE` costante di compilazione condizionale per un progetto in sincronia con il tipo di progetto.  
  
## <a name="predefined-mytype-values"></a>Valori predefiniti di MyType  
 È necessario utilizzare il `/define` l'opzione del compilatore per impostare il `_MYTYPE` costante di compilazione condizionale. Quando si specifica il valore per il `_MYTYPE` costante, è necessario racchiudere il valore della stringa mark barre rovesciate/virgolette (\\") le sequenze. Ad esempio, è possibile utilizzare:  
  
```  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 Questa tabella viene mostrato l'aspetto di `_MYTYPE` viene impostata la costante di compilazione condizionale per diversi tipi di progetto.  
  
|Tipo di progetto|Valore di MyType|  
|------------------|--------------------|  
|Libreria di classi|"Windows"|  
|Applicazione console|"Console"|  
|Web|"Web"|  
|Libreria di controlli Web|"WebControl"|  
|Applicazione Windows|"WindowsForms"|  
|Applicazione di Windows, quando si avvia con personalizzato`Sub Main`|"WindowsFormsWithCustomSubMain"|  
|Libreria di controlli Windows|"Windows"|  
|Servizio Windows|"Console"|  
|Empty|"Vuota"|  
  
> [!NOTE]
>  Tutti i confronti di stringa di compilazione condizionale tra maiuscole e minuscole, indipendentemente da come la `Option Compare` istruzione è impostata.  
  
## <a name="dependent-my-compilation-constants"></a>Costanti di compilazione dipendenti My  
 Il `_MYTYPE` costante di compilazione condizionale, a sua volta, controlla i valori di molte altre `_MY` costanti di compilazione:  
  
|_MYTYPE|_MYAPPLICATIONTYPE|_MYCOMPUTERTYPE|_MYFORMS|_MYUSERTYPE|_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|"Console"|"Console"|"Windows"|Non definito|"Windows"|TRUE|  
|"Custom"|Non definito|Non definito|Non definito|Non definito|Non definito|  
|"Vuota"|Non definito|Non definito|Non definito|Non definito|Non definito|  
|"Web"|Non definito|"Web"|FALSE|"Web"|FALSE|  
|"WebControl"|Non definito|"Web"|FALSE|"Web"|TRUE|  
|"Windows" o ""|"Windows"|"Windows"|Non definito|"Windows"|TRUE|  
|"WindowsForms"|"WindowsForms"|"Windows"|TRUE|"Windows"|TRUE|  
|"WindowsFormsWithCustomSubMain"|"Console"|"Windows"|TRUE|"Windows"|TRUE|  
  
 Per impostazione predefinita, le costanti di compilazione condizionale non definite risolvere `FALSE`. Quando si compila il progetto per eseguire l'override del comportamento predefinito, è possibile specificare valori per le costanti non definite.  
  
> [!NOTE]
>  Quando `_MYTYPE` è impostato su "Custom", il progetto contiene il `My` dello spazio dei nomi, ma non contiene oggetti. Tuttavia, l'impostazione `_MYTYPE` a "Empty" impedisce al compilatore l'aggiunta di `My` dello spazio dei nomi e i relativi oggetti.  
  
 Questa tabella vengono descritti gli effetti dei valori predefiniti del `_MY` costanti di compilazione.  
  
|Costante|Significato|  
|--------------|-------------|  
|`_MYAPPLICATIONTYPE`|Consente di `My.Application`, se la costante è "Console" Windows "o"WindowsForms":<br /><br /> -La versione "Console" deriva da <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase>.</xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> e ha meno membri rispetto alla versione "Windows".<br />-La versione "Windows" deriva da <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>e dispone di meno membri rispetto alla versione "WindowsForms".</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase><br />-La versione "WindowsForms" di `My.Application` deriva da <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> Se il `TARGET` costante è definita come "winexe", quindi la classe include un `Sub Main` metodo.|  
|`_MYCOMPUTERTYPE`|Consente di `My.Computer`, se la costante è "Web" o "Windows":<br /><br /> -La versione "Web" deriva da <xref:Microsoft.VisualBasic.Devices.ServerComputer>, e ha meno membri rispetto alla versione "Windows".</xref:Microsoft.VisualBasic.Devices.ServerComputer><br />-La versione "Windows" del `My.Computer` deriva da <xref:Microsoft.VisualBasic.Devices.Computer>.</xref:Microsoft.VisualBasic.Devices.Computer>|  
|`_MYFORMS`|Consente di `My.Forms`, se la costante è `TRUE`.|  
|`_MYUSERTYPE`|Consente di `My.User`, se la costante è "Web" o "Windows":<br /><br /> -La versione "Web" di `My.User` è associato l'identità dell'utente della richiesta HTTP corrente.<br />-La versione "Windows" di `My.User` è associata l'entità del thread corrente.|  
|`_MYWEBSERVICES`|Consente di `My.WebServices`, se la costante è `TRUE`.|  
|`_MYTYPE`|Consente di `My.Log`, `My.Request`, e `My.Response`, se la costante è "Web".|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer></xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log></xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User></xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [Il mio dipende dal tipo di progetto](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)   
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)   
 [Forms (oggetto)](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [Oggetto My. Request](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [Oggetto My. Response](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [Oggetto My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md)
