---
title: "Procedura: Creare un modello di attivit&#224; personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6760a5cc-6eb8-465f-b4fa-f89b39539429
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Procedura: Creare un modello di attivit&#224; personalizzato
I modelli di attività personalizzati vengono utilizzati per personalizzare la configurazione delle attività, incluse CompositeActivity personalizzate, in modo che gli utenti non debbano creare individualmente ciascuna attività e configurare manualmente le relative proprietà e altre impostazioni.Questi modelli personalizzati possono essere resi disponibili nella **Casella degli strumenti** in [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] o da una finestra di progettazione riallocata dalla quale gli utenti possono trascinarli nell'area di progettazione preconfigurata.In [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] sono disponibili validi esempi di questi modelli: [Finestra di progettazione del modello SendAndReceiveReply](../Topic/SendAndReceiveReply%20Template%20Designer.md) e [Finestra di progettazione del modello ReceiveAndSendReply](../Topic/ReceiveAndSendReply%20Template%20Designer.md) nella categoria [ActivityDesigner Messaggistica](../Topic/Messaging%20Activity%20Designers.md).  
  
 Nella prima procedura di questo argomento viene descritto come creare un modello di attività personalizzato per un'attività **Delay**, mentre nella seconda procedura viene descritto brevemente come renderlo disponibile in [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] per verificare che il modello personalizzato funzioni.  
  
 I modelli di attività personalizzati devono implementare l'oggetto <xref:System.Activities.Presentation.IActivityTemplateFactory>.L'interfaccia dispone di un singolo metodo <xref:System.Activities.Presentation.IActivityTemplateFactory.Create%2A> con il quale è possibile creare e configurare le istanze dell'attività utilizzate nel modello.  
  
### Per creare un modello per l'attività Delay  
  
1.  Avviare [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
3.  Nel riquadro **Tipi progetto** selezionare **Flusso di lavoro** dal gruppo di progetti **Visual C\#** o **Visual Basic** a seconda del linguaggio preferito.  
  
4.  Nel riquadro **Modelli** selezionare **Libreria attività**.  
  
5.  Nella casella **Nome** immettere `DelayActivityTemplate`.  
  
6.  Accettare le impostazioni predefinite nelle caselle di testo **Percorso** e **Nome soluzione**, quindi fare clic su **OK**.  
  
7.  Fare clic con il pulsante destro del mouse sulla directory Riferimenti del progetto DelayActivityTemplate in **Esplora soluzioni** e scegliere **Aggiungi riferimento** per aprire la finestra di dialogo corrispondente.  
  
8.  Andare alla scheda **.NET** e selezionare **PresentationFramework** dalla colonna **Nome componente** a sinistra e fare clic su **OK** per aggiungere un riferimento al file PresentationFramework.dll.  
  
9. Ripetere questa procedura per aggiungere riferimenti ai file System.Activities.Presentation.dll e WindowsBase.dll.  
  
10. Fare clic con il pulsante destro del mouse sul progetto DelayActivityTemplate in **Esplora soluzioni**, scegliere **Aggiungi**, quindi fare clic su **Nuovo elemento** per aprire la finestra di dialogo **Aggiungi nuovo elemento**.  
  
11. Selezionare il modello **Class**, denominarlo MyDelayTemplate e quindi fare clic su **OK**.  
  
12. Aprire il file MyDelayTemplate.cs e aggiungere le istruzioni seguenti.  
  
    ```  
  
    //Namespaces added  
    using System.Activities;  
    using System.Activities.Statements;  
    using System.Activities.Presentation;  
    using System.Windows;  
  
    ```  
  
13. Implementare <xref:System.Activities.Presentation.IActivityTemplateFactory> con la classe `MyDelayActivity` con il codice seguente.In questo modo viene configurata una durata del ritardo di 10 secondi.  
  
    ```  
  
    public sealed class MyDelayActivity : IActivityTemplateFactory  
    {  
        public Activity Create(System.Windows.DependencyObject target)  
        {  
            return new System.Activities.Statements.Delay  
            {  
                DisplayName = "DelayActivityTemplate",  
                Duration = new TimeSpan(0, 0, 10)  
  
            };  
        }  
    }  
  
    ```  
  
14. Selezionare **Compila soluzione** dal menu **Compila** per generare il file DelayActivityTemplate.dll.  
  
### Per rendere disponibile il modello in Progettazione flussi di lavoro  
  
1.  Fare clic con il pulsante destro del mouse sulla soluzione DelayActivityTemplate in **Esplora soluzioni**, scegliere **Aggiungi**, quindi fare clic su **Nuovo progetto** per aprire la finestra di dialogo **Aggiungi nuovo progetto**.  
  
2.  Selezionare il modello **Applicazione console flusso di lavoro**, denominarlo `CustomActivityTemplateApp`, quindi fare clic su **OK**.  
  
3.  Fare clic con il pulsante destro del mouse sulla directory Riferimenti del progetto CustomActivityTemplateApp in **Esplora soluzioni** e scegliere **Aggiungi riferimento** per aprire la finestra di dialogo corrispondente.  
  
4.  Andare alla scheda **Progetti** e selezionare **DelayActivityTemplate** dalla colonna **Nome progetto** a sinistra e fare clic su **OK** per aggiungere un riferimento al file DelayActivityTemplate.dll creato nella prima procedura.  
  
5.  Fare clic con il pulsante destro del mouse sul progetto CustomActivityTemplateApp in**Esplora soluzioni** e scegliere **Compila** per compilare l'applicazione.  
  
6.  Fare clic con il pulsante destro del mouse sul progetto CustomActivityTemplateApp in **Esplora soluzioni** e scegliere **Imposta come progetto di avvio**.  
  
7.  Selezionare **Avvia senza eseguire debug** dal menu **Debug** e premere qualsiasi tasto per continuare quando richiesto nella finestra di cmd.exe.  
  
8.  Aprire il file Workflow1.xaml e quindi **Casella degli strumenti**.  
  
9. Individuare il modello **MyDelayActivity** nella categoria **DelayActivityTemplate**.Trascinarlo nell'area di progettazione.Nella finestra **Proprietà** verificare che la proprietà `Duration` sia impostata su 10 secondi.  
  
## Esempio  
 Il file MyDelayActivity.cs deve contenere il codice seguente.  
  
```  
  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
  
//Namespaces added  
using System.Activities;  
using System.Activities.Statements;  
using System.Activities.Presentation;  
using System.Windows;  
  
namespace DelayActivityTemplate  
{  
    public sealed class MyDelayActivity : IActivityTemplateFactory  
    {  
        public Activity Create(System.Windows.DependencyObject target)  
        {  
            return new System.Activities.Statements.Delay  
            {  
                DisplayName = "DelayActivityTemplate",  
                Duration = new TimeSpan(0, 0, 10)  
  
            };  
        }  
    }  
}  
  
```  
  
## Vedere anche  
 <xref:System.Activities.Presentation.IActivityTemplateFactory>   
 [Personalizzazione della fase di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//customizing-the-workflow-design-experience.md)