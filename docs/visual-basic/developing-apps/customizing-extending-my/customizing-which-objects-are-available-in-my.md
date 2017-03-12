---
title: "Customizing Which Objects are Available in My (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My namespace, customizing"
  - "My namespace"
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Customizing Which Objects are Available in My (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento viene descritto come verificare quali oggetti `My` sono abilitati impostando la costante della compilazione condizionale `_MYTYPE` del progetto.  L'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\) di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] mantiene la costante di compilazione condizionale `_MYTYPE` per un progetto in sincronia con il tipo di progetto.  
  
## Valori predefiniti di \_MYTYPE  
 È necessario utilizzare l'opzione del compilatore `/define` per impostare la costante della compilazione condizionale `_MYTYPE`.  Quando si specifica un proprio valore per la costante `_MYTYPE`, è necessario racchiudere il valore della stringa in sequenze barre rovesciate\/virgolette \(\\"\).  Ad esempio, utilizzare:  
  
```  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 In questa tabella viene mostrato come viene impostata la costante di compilazione condizionale `_MYTYPE` per diversi tipi di progetto.  
  
|Tipo di progetto|Valore di \_MYTYPE|  
|----------------------|------------------------|  
|Libreria di classi|"Windows"|  
|Applicazione console|"Console"|  
|Web|"Web"|  
|Libreria di controlli Web|"WebControl"|  
|Applicazione Windows|"WindowsForms"|  
|Applicazione Windows, quando inizia con `Sub Main` personalizzato|"WindowsFormsWithCustomSubMain"|  
|Libreria di controlli Windows|"Windows"|  
|Servizio Windows|"Console"|  
|Vuoto|"Empty"|  
  
> [!NOTE]
>  Tutti i confronti della stringa di compilazione condizionale sono con distinzione tra maiuscole e minuscole, indipendentemente a come è impostata l'istruzione `Option Compare`.  
  
## Costanti dipendenti \_MY Compilation  
 La costante di compilazione condizionale `_MYTYPE`, a sua volta, controlla i valori di molte altre costanti di compilazione condizionale `_MY`:  
  
|\_MYTYPE|\_MYAPPLICATIONTYPE|\_MYCOMPUTERTYPE|\_MYFORMS|\_MYUSERTYPE|\_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|"Console"|"Console"|"Windows"|Non definito|"Windows"|TRUE|  
|"Custom"|Non definito|Non definito|Non definito|Non definito|Non definito|  
|"Empty"|Non definito|Non definito|Non definito|Non definito|Non definito|  
|"Web"|Non definito|"Web"|FALSE|"Web"|FALSE|  
|"WebControl"|Non definito|"Web"|FALSE|"Web"|TRUE|  
|"Windows" o ""|"Windows"|"Windows"|Non definito|"Windows"|TRUE|  
|"WindowsForms"|"WindowsForms"|"Windows"|TRUE|"Windows"|TRUE|  
|"WindowsFormsWithCustomSubMain"|"Console"|"Windows"|TRUE|"Windows"|TRUE|  
  
 Per impostazione predefinita, le costanti di compilazione condizionale non definite vengono risolte in `FALSE`.  È possibile specificare i valori per le costanti non definite quando si compila il progetto per sovrascrivere il comportamento predefinito.  
  
> [!NOTE]
>  Quando `_MYTYPE` è impostato su "Custom", il progetto contiene lo spazio dei nomi `My` ma non contiene alcun oggetto.  Tuttavia, impostando `_MYTYPE` su "Empty" si impedisce al compilatore di aggiungere lo spazio dei nomi `My` e i relativi oggetti.  
  
 In questa tabella vengono descritti gli effetti dei valori predefiniti delle costanti di compilazione `_MY`.  
  
|Costante|Significato|  
|--------------|-----------------|  
|`_MYAPPLICATIONTYPE`|Consente di abilitare `My.Application`, se la costante è "Console", Windows", o "WindowsForms":<br /><br /> -   La versione "Console" deriva da <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> e include un numero minore di membri rispetto alla versione "Windows".<br />-   La versione "Windows" deriva da <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> e dispone di un numero inferiore di membri della versione "WindowsForms".<br />-   La versione "WindowsForms" di `My.Application` deriva da <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>.  Se la costante `TARGET` viene definita come "winexe", la classe include un metodo `Sub Main`.|  
|`_MYCOMPUTERTYPE`|Consente di abilitare `My.Computer`, se la costante è "Web" o Windows":<br /><br /> -   La versione "Web" deriva da <xref:Microsoft.VisualBasic.Devices.ServerComputer> e dispone di un numero inferiore di membri della versione "Windows".<br />-   La versione "Windows" di `My.Computer` deriva da <xref:Microsoft.VisualBasic.Devices.Computer>.|  
|`_MYFORMS`|Consente di abilitare `My.Forms` se la costante è `TRUE`.|  
|`_MYUSERTYPE`|Consente di abilitare `My.User`, se la costante è "Web" o Windows":<br /><br /> -   La versione "Web" di `My.User` è associata all'identità dell'utente della richiesta HTTP corrente.<br />-   La versione "Windows" di `My.User` è associata al Principal corrente del thread.|  
|`_MYWEBSERVICES`|Consente di abilitare `My.WebServices` se la costante è `TRUE`.|  
|`_MYTYPE`|Consente di abilitare `My.Log`, `My.Request`e `My.Response` se la costante è "Web".|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [How My Depends on Project Type](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)   
 [My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.Request Object](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [My.Response Object](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)