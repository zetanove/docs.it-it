---
title: "Procedura: ereditare form mediante la finestra di dialogo Selezione ereditariet&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ereditarietà, form"
  - "Selezione ereditarietà (finestra di dialogo)"
  - "form ereditati, creazione"
ms.assetid: 969b4c04-12aa-4297-93a2-0ae747447823
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: ereditare form mediante la finestra di dialogo Selezione ereditariet&#224;
Il modo più semplice di ereditare un form o un altro oggetto consiste nell'usare la finestra di dialogo**Selezione ereditarietà**.  In questo modo è possibile recuperare e riutilizzare il codice o un'interfaccia utente precedentemente creata in altre soluzioni.  
  
> [!NOTE]
>  Per ereditare da un form con la finestra di dialogo **Selezione ereditarietà**, il progetto che contiene il form deve essere incorporato in un file eseguibile o in una DLL.  Per compilare il progetto scegliere **Compila soluzione** dal menu **Compila**.  
>   
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un Windows Form ereditato da un form esistente usando Selezione ereditarietà  
  
1.  Scegliere **Aggiungi Windows Form** dal menu **Progetto**.  
  
     Verrà aperta la finestra di dialogo **Aggiungi nuovo elemento**.  
  
2.  Selezionare il modello **Form ereditato** e denominarlo nella casella **Nome**.  Fare clic sul pulsante **Aggiungi** per procedere.  
  
     Verrà aperta la finestra di dialogo **Selezione ereditarietà**.  Se il progetto corrente include già form, verranno visualizzati nella finestra di dialogo **Selezione ereditarietà**.  
  
3.  Per ereditare da un form in un altro assembly, fare clic sul pulsante **Sfoglia**.  
  
4.  Nella finestra di dialogo **Selezionare un file che contiene un componente da cui ereditare** passare al progetto contenente il form o il modulo desiderato.  
  
5.  Fare clic sul nome del file EXE o del file DLL per selezionarlo, quindi fare clic sul pulsante **Apri**.  
  
     Verrà nuovamente visualizzata finestra di dialogo **Selezione ereditarietà**, in cui ora il componente risulta visualizzato unitamente al progetto in cui si trova.  
  
6.  Selezionare il componente.  
  
     Il componente verrà aggiunto al progetto in **Esplora soluzioni**.  Se il componente include un'interfaccia utente, i controlli che fanno parte del form ereditato saranno contraddistinti da un glifo \(![Schermata VisualBasicInheritanceSymbol](../../../../docs/framework/winforms/advanced/media/vbinheritanceglyph.png "vbInheritanceGlyph")\) e, una volta selezionati, verranno visualizzati con un bordo che indica il livello di sicurezza del controllo sul form impostato come superclasse.  I comportamenti che corrispondono ai vari livelli di sicurezza sono elencati nella tabella seguente.  
  
    |Livello di sicurezza del controllo|Interazione possibile nella finestra di progettazione e nell'editor di codice con il form ereditato|  
    |----------------------------------------|---------------------------------------------------------------------------------------------------------|  
    |Public|Bordo standard con quadratini di ridimensionamento: il controllo può essere ridimensionato e spostato.  È possibile accedere al controllo internamente tramite la classe che lo dichiara ed esternamente tramite le altre classi.|  
    |Protetta|Bordo standard con quadratini di ridimensionamento: il controllo può essere ridimensionato e spostato.  È possibile accedere al controllo internamente tramite la classe che lo dichiara e tramite qualsiasi classe che eredita dalla classe padre, ma non tramite classi esterne.|  
    |Protected Internal \(Protected Friend in Visual Basic\)|Bordo standard con quadratini di ridimensionamento: il controllo può essere ridimensionato e spostato.  Accessibile internamente dalla classe che lo dichiara, da qualsiasi classe che eredita dalla classe padre e da altri membri dell'assembly che lo include.|  
    |Internal \(Friend in Visual Basic\)|Bordo standard senza quadratini di ridimensionamento, visualizzato nel form, con proprietà visibili nella finestra **Proprietà**.  Tutti gli aspetti del controllo saranno tuttavia considerati di sola lettura.  Non è possibile spostare il controllo, ridimensionarlo né modificarne le proprietà.  Se il controllo è un contenitore di altri controlli, come una casella di gruppo, non è possibile aggiungere nuovi controlli né rimuovere i controlli esistenti, anche in caso di controlli con livello di sicurezza Public.  È possibile accedere al controllo solo tramite altri membri dell'assembly che lo contiene.|  
    |Private|Bordo standard senza quadratini di ridimensionamento, visualizzato nel form, con proprietà visibili nella finestra **Proprietà**.  Tutti gli aspetti del controllo saranno tuttavia considerati di sola lettura.  Non è possibile spostare il controllo, ridimensionarlo né modificarne le proprietà.  Se il controllo è un contenitore di altri controlli, come una casella di gruppo, non è possibile aggiungere nuovi controlli né rimuovere i controlli esistenti, anche in caso di controlli con livello di sicurezza Public.  È possibile accedere al controllo solo tramite la classe che lo dichiara.|  
  
     Per informazioni su come modificare l'aspetto di un form di base, vedere [Effetti della modifica dell'aspetto di un form di base](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md).  
  
    > [!NOTE]
    >  Quando si uniscono controlli e componenti ereditati con controlli e componenti standard in Windows Form, possono verificarsi conflitti nell'ordinamento z.  È possibile correggere il problema modificando l'ordine z. Fare clic sul menu **Formato**, scegliere **Ordine** e quindi fare clic su **Porta in primo piano** o **Porta in secondo piano**.  Per altre informazioni sull'ordine z dei controlli, vedere [Procedura: disporre oggetti su più livelli in Windows Form](../../../../docs/framework/winforms/controls/how-to-layer-objects-on-windows-forms.md).  
  
## Vedere anche  
 [Inherits Statement](../../../../ocs/visual-basic/language-reference/statements/inherits-statement.md)   
 [utilizzo](../Topic/using%20\(C%23%20Reference\).md)   
 [Effetti della modifica dell'aspetto di un form di base](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)   
 [Ereditarietà visiva di Windows Form](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)