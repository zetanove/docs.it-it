---
title: Creazione e uso di componenti in Visual Basic | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- components [Visual Basic]
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
caps.latest.revision: 9
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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 1235f62f6ac0878e16387c35150764f3585bc004
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="creating-and-using-components-in-visual-basic"></a>Creazione e utilizzo di componenti in Visual Basic
Un *componente* è una classe che implementa l'interfaccia <xref:System.ComponentModel.IComponent?displayProperty=fullName> o che deriva direttamente o indirettamente da una classe che implementa <xref:System.ComponentModel.IComponent>. Un componente di [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)] è un oggetto riutilizzabile in grado di interagire con altri oggetti, che consente di controllare le risorse esterne e il supporto in fase di progettazione.  
  
 Una caratteristica importante dei componenti è che possono essere manipolati in fase di progettazione, quindi se una classe è un componente può essere usata nell'ambiente di sviluppo integrato (IDE) di [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)]. Un componente può essere aggiunto alla casella degli strumenti, trascinato e rilasciato in un form e manipolato in un'area di progettazione. Si noti che il supporto di base per i componenti in fase di progettazione è incorporato in [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)], quindi uno sviluppatore di componenti non deve effettuare operazioni aggiuntive per sfruttare la funzionalità di base in fase di progettazione.  
  
 Un *controllo* è simile a un componente, poiché entrambi possono essere manipolati. A differenza di un componente, un controllo produce però un'interfaccia utente. Un controllo deve derivare da una delle classi di controllo di base: <xref:System.Windows.Forms.Control> o <xref:System.Web.UI.Control>.  
  
## <a name="when-to-create-a-component"></a>Quando si crea un componente  
 Se la classe viene usata in un'area di progettazione, ad esempio Windows Form o Progettazione Web Form, ma non ha un'interfaccia utente, deve essere un componente e implementare <xref:System.ComponentModel.IComponent> oppure derivare da una classe che implementa direttamente o indirettamente <xref:System.ComponentModel.IComponent>.  
  
 Le classi <xref:System.ComponentModel.Component> e <xref:System.ComponentModel.MarshalByValueComponent> sono implementazioni di base dell'interfaccia <xref:System.ComponentModel.IComponent>. La differenza principale tra queste classi è che la classe <xref:System.ComponentModel.Component> viene sottoposta a marshalling in base al riferimento, mentre <xref:System.ComponentModel.IComponent> è sottoposta a marshalling in base al valore. L'elenco seguente contiene indicazioni generali per gli implementatori.  
  
-   Se il componente deve essere sottoposto a marshalling in base al riferimento, derivare la classe da <xref:System.ComponentModel.Component>.  
  
-   Se il componente deve essere sottoposto a marshalling in base al valore, derivare la classe da <xref:System.ComponentModel.MarshalByValueComponent>.  
  
-   Se il componente non può derivare da una delle implementazioni di base a causa di un'ereditarietà singola, implementare <xref:System.ComponentModel.IComponent>.  
  
 Per altre informazioni sul supporto in fase di progettazione, vedere [Attributi per componenti in fase di progettazione](http://msdn.microsoft.com/library/12050fe3-9327-4509-9e21-4ee2494b95c3) e [Estensione del supporto in fase di progettazione](http://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2).  
  
## <a name="component-classes"></a>Classi di componenti  
 Lo spazio dei nomi <xref:System.ComponentModel> offre classi usate per implementare il comportamento dei componenti e dei controlli in fase di progettazione e di esecuzione. Questo spazio dei nomi include le classi e le interfacce di base per l'implementazione di attributi e convertitori, l'associazione a origini dati e le licenze per i componenti.  
  
 Le classi di componenti principali sono:  
  
-   <xref:System.ComponentModel.Component>. Un'implementazione di base per l'interfaccia <xref:System.ComponentModel.IComponent>. Questa classe abilita la condivisione degli oggetti tra applicazioni.  
  
-   <xref:System.ComponentModel.MarshalByValueComponent>. Un'implementazione di base per l'interfaccia <xref:System.ComponentModel.IComponent>.  
  
-   <xref:System.ComponentModel.Container>. L'implementazione di base per l'interfaccia <xref:System.ComponentModel.IContainer>. Questa classe incapsula zero o più componenti.  
  
 Alcune delle classi utilizzate per le licenze dei componenti sono:  
  
-   <xref:System.ComponentModel.License>. Classe di base astratta per tutte le licenze. La licenza viene concessa a un'istanza specifica di un componente.  
  
-   <xref:System.ComponentModel.LicenseManager>. Offre proprietà e metodi per aggiungere una licenza a un componente e gestire <xref:System.ComponentModel.LicenseProvider>.  
  
-   <xref:System.ComponentModel.LicenseProvider>. Classe di base astratta per l'implementazione di un provider di licenza.  
  
-   <xref:System.ComponentModel.LicenseProviderAttribute>. Specifica la classe <xref:System.ComponentModel.LicenseProvider> da usare con una classe.  
  
 Classi usate in genere per descrivere e rendere persistenti i componenti.  
  
-   <xref:System.ComponentModel.TypeDescriptor>. Offre informazioni sulle caratteristiche di un componente, ad esempio gli attributi, le proprietà e gli eventi.  
  
-   <xref:System.ComponentModel.EventDescriptor>. Include informazioni su un evento.  
  
-   <xref:System.ComponentModel.PropertyDescriptor>. Include informazioni su una proprietà.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Confronto tra classe, componente e controllo](http://msdn.microsoft.com/library/db8b842e-44d9-40cc-a0f8-70fd189632c3)  
 Definisce *componenti* e *controlli*e spiega le differenze tra questi elementi e le classi.  
  
 [Modifica di componenti](http://msdn.microsoft.com/library/4a5a5e49-0378-4a31-83bc-24da0f1a727d)  
 Guida di orientamento per iniziare a usare i componenti.  
  
 [Procedure dettagliate per la modifica di componenti](http://msdn.microsoft.com/library/c414cca9-2489-4208-8b38-954586d91c13)  
 Collegamenti ad argomenti che offrono istruzioni dettagliate per la programmazione dei componenti.  
  
 [Classi di componenti](http://msdn.microsoft.com/library/ce2e5647-e673-4c2b-8125-ffebbd9d71bc)  
 Descrive che cosa fa di una classe un componente, i modi per esporre la funzionalità del componente, il controllo dell'accesso ai componenti e il controllo delle modalità di creazione delle istanze dei componenti.  
  
 [Risoluzione dei problemi relativi alla modifica di controlli e componenti](../../framework/winforms/controls/troubleshooting-control-and-component-authoring.md)  
 Viene illustrato come risolvere i problemi comuni.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: Accedere al supporto in fase di progettazione in Windows Forms](http://msdn.microsoft.com/library/a84f8579-1f47-41b9-ba37-69030b0aff09)   
 [Procedura: Estendere l'aspetto e il comportamento di controlli in modalità progettazione](http://msdn.microsoft.com/library/68f85054-2253-47f5-a4f2-3f1ac8c9f27b)   
 [Procedura: Eseguire un'inizializzazione personalizzata per i controlli in modalità progettazione](http://msdn.microsoft.com/library/914eaa03-092f-4556-9160-b8a2a40641d9)
