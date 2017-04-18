---
title: Assemblaggio e distribuzione personalizzate estensioni My (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
- My namespace, extending
ms.assetid: fd89c54b-0290-4c50-95a3-ff17d4487a21
caps.latest.revision: 10
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
ms.openlocfilehash: 950592c0fb197959ce1c3cf6128093846a022709
ms.lasthandoff: 03/13/2017

---
# <a name="packaging-and-deploying-custom-my-extensions-visual-basic"></a>Assemblaggio e distribuzione personalizzate estensioni My (Visual Basic)
Visual Basic fornisce un modo semplice per la distribuzione personalizzata `My` estensioni dello spazio dei nomi utilizzando modelli di Visual Studio. Se si sta creando un modello di progetto per il quale il `My` le estensioni sono parte integrante del nuovo tipo di progetto, è possibile includere personalizzato `My` codice di estensione con il progetto quando si esporta il modello. Per ulteriori informazioni sull'esportazione di modelli di progetto, vedere [procedura: creare modelli di progetto](http://msdn.microsoft.com/library/a1a6999d-a34c-48a8-b1cf-027eb5c76398).  
  
 Se personalizzato `My` estensione è in un singolo file di codice, è possibile esportare il file come modello di elemento che possono essere aggiunte a qualsiasi tipo di progetto Visual Basic. È quindi possibile personalizzare il modello di elemento per abilitare funzionalità aggiuntive e il comportamento per personalizzato `My` estensione in un progetto di Visual Basic. Tali funzionalità includono:  
  
-   Consentendo agli utenti di gestire personalizzato `My` dall'estensione di **estensioni My** pagina della finestra di progettazione di progetto Visual Basic.  
  
-   Aggiunta automatica personalizzati `My` estensione quando un riferimento a un assembly specificato viene aggiunto a un progetto.  
  
-   Nascondere il `My` modello di elemento di estensione nel **Aggiungi elemento** nella finestra di dialogo in modo che non è incluso nell'elenco di elementi di progetto.  
  
 In questo argomento viene illustrato come creare un pacchetto personalizzato `My` estensione come un modello di elemento nascosto che può essere gestito dal **estensioni My** pagina della finestra di progettazione di progetto Visual Basic. Personalizzata `My` estensione può anche essere aggiunta automaticamente quando un riferimento a un assembly specificato viene aggiunto a un progetto.  
  
## <a name="create-a-my-namespace-extension"></a>Creare un'estensione dello spazio dei nomi  
 Il primo passaggio nella creazione di un pacchetto di distribuzione per un oggetto personalizzato `My` estensione consiste nel creare l'estensione come un singolo file di codice. Per informazioni dettagliate e istruzioni su come creare un oggetto personalizzato `My` estensione, vedere [estensione di My Namespace in Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md).  
  
## <a name="export-a-my-namespace-extension-as-an-item-template"></a>Esportare un'estensione dello spazio dei nomi come un modello di elemento  
 Dopo aver creato un file di codice che include il `My` estensione dello spazio dei nomi, è possibile esportare il file di codice come modello di elemento Visual Studio. Per istruzioni su come esportare un file come modello di elemento Visual Studio, vedere [procedura: creare modelli di elemento](http://msdn.microsoft.com/library/77bc53d4-d607-4820-a032-7e3b365891b5).  
  
> [!NOTE]
>  Se il `My` estensione dello spazio dei nomi ha una dipendenza su un particolare assembly, è possibile personalizzare il modello di elemento per installare automaticamente il `My` estensione dello spazio dei nomi quando viene aggiunto un riferimento a tale assembly. Verrà di conseguenza, si desidera escludere tale riferimento all'assembly quando si esporta il file di codice come un modello di elemento Visual Studio.  
  
## <a name="customize-the-item-template"></a>Personalizzare il modello di elemento  
 È possibile attivare il modello di elemento dal **estensioni My** pagina della finestra di progettazione di progetto Visual Basic. È inoltre possibile abilitare il modello di elemento da aggiungere automaticamente quando un riferimento a un assembly specificato viene aggiunto a un progetto. Per abilitare queste personalizzazioni, si verrà aggiungere un nuovo file, chiamato CustomData, per il modello e quindi aggiungere un nuovo elemento al codice XML nel file. vstemplate.  
  
### <a name="add-the-customdata-file"></a>Aggiungere il file CustomData  
 Il file CustomData è un file di testo con un'estensione di. CustomData (il nome del file può essere impostato su qualsiasi valore significativo per il modello) e che contiene il codice XML. Il codice XML nel file CustomData indica di includere il `My` estensione quando gli utenti utilizzeranno il **estensioni My** pagina della finestra di progettazione di progetto Visual Basic. È possibile aggiungere facoltativamente il `AssemblyFullName>` attributo XML del file CustomData. Ciò indica a Visual Basic per installare automaticamente personalizzato `My` estensione quando un riferimento a un particolare assembly viene aggiunto al progetto. È possibile utilizzare qualsiasi editor di testo o editor XML per creare il file CustomData e quindi aggiungerlo alla cartella compressa del modello di elemento (file con estensione zip).  
  
 Ad esempio, il codice XML seguente viene illustrato il contenuto di un file CustomData che consentiranno di aggiungere l'elemento del modello nella cartella Estensioni My di un progetto di Visual Basic quando un riferimento all'assembly Microsoft.VisualBasic.PowerPacks.Vs.dll viene aggiunto al progetto.  
  
```  
<VBMyExtensionTemplate   
    ID="Microsoft.VisualBasic.Samples.MyExtensions.MyPrinterInfo"   
    Version="1.0.0.0"  
    AssemblyFullName="Microsoft.VisualBasic.PowerPacks.vs"  
/>  
```  
  
 Il file CustomData contiene un `VBMyExtensionTemplate>` elemento con attributi, come indicato nella tabella seguente.  
  
|Attributo|Descrizione|  
|---|---|  
|`ID`|Obbligatorio. Identificatore univoco per l'estensione. Se l'estensione con questo ID è già stato aggiunto al progetto, l'utente non necessario aggiungerlo di nuovo.|  
|`Version`|Obbligatorio. Numero di versione per il modello di elemento.|  
|`AssemblyFullName`|Facoltativo. Nome dell'assembly. Quando un riferimento a questo assembly viene aggiunto al progetto, l'utente verrà richiesto di aggiungere il `My` estensione da questo modello di elemento.|  
  
### <a name="add-the-customdatasignature-element-to-the-vstemplate-file"></a>Aggiungere il \<CustomDataSignature > elemento del file. vstemplate  
 Per identificare il modello di elemento Visual Studio come un `My` estensione dello spazio dei nomi, è necessario modificare anche il file. vstemplate del modello di elemento. È necessario aggiungere un `<CustomDataSignature>` elemento per il `<TemplateData>` elemento. Il `<CustomDataSignature>` elemento deve contenere il testo `Microsoft.VisualBasic.MyExtension`, come illustrato nell'esempio seguente.  
  
```  
<CustomDataSignature>Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
```  
  
 È possibile modificare direttamente i file in una cartella compressa (zip). È necessario copiare il file. vstemplate dalla cartella compressa, modificarlo e quindi sostituire il file. vstemplate nella cartella compressa con la copia aggiornata.  
  
 Nell'esempio seguente viene illustrato il contenuto di un file. vstemplate con il `<CustomDataSignature>` elemento aggiunto.  
  
```  
<VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">  
  <TemplateData>  
    <DefaultName>MyCustomExtensionModule.vb</DefaultName>  
    <Name>MyPrinterInfo</Name>  
    <Description>Custom My Extensions Item Template</Description>  
    <ProjectType>VisualBasic</ProjectType>  
    <SortOrder>10</SortOrder>  
    <Icon>__TemplateIcon.ico</Icon>  
    <CustomDataSignature      >Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
  </TemplateData>  
  <TemplateContent>  
    <References />  
    <ProjectItem SubType="Code"   
                 TargetFileName="$fileinputname$.vb"  
                 ReplaceParameters="true"  
     >MyCustomExtensionModule.vb</ProjectItem>  
  </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="install-the-template"></a>Installare il modello  
 Per installare il modello, è possibile copiare la cartella compressa (zip) nella cartella dei modelli di elemento Visual Basic (ad esempio, Documenti\Visual Studio 2008\Templates\Item elementi\Visual base). In alternativa, è possibile pubblicare il modello come un file di Visual Studio Installer (vsi).  
  
## <a name="see-also"></a>Vedere anche  
 [Estensione dello spazio dei nomi My in Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)   
 [Estensione del modello di applicazione Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [Personalizzazione degli oggetti sono disponibili in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Pagina Estensioni My, Progettazione progetti](https://docs.microsoft.com/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)
