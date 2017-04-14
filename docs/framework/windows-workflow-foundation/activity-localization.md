---
title: "Localizzazione di attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ee7bc16-e609-469a-a3e8-8062952e2676
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Localizzazione di attivit&#224;
Quando le applicazioni e i componenti del flusso di lavoro possono essere localizzati in altre impostazioni cultura e lingue, le stringhe di risorsa devono essere utilizzate in modo da poter essere localizzate senza ricompilare.  
  
## Localizzazione di attività  
 Come avviene con tutte le applicazioni che devono essere localizzate \(rilasciate in versioni diverse per lingue e impostazioni cultura differenti\), qualsiasi stringa visualizzata all'utente non deve essere inserita direttamente nel codice, bensì archiviata in un file di risorse.L'accesso alle stringhe può quindi essere eseguito tramite l'oggetto <xref:System.Environment.GetResourceString>.Se si sta sviluppando un componente che viene distribuito in diverse lingue, si desidera anche utilizzare stringhe di risorsa per i messaggi di convalida delle attività, i dati di rilevamento definiti dall'utente, i messaggi di traccia e quelli di errore.  
  
 Nell'esercizio seguente viene illustrato come utilizzare un file di risorse.  
  
#### Utilizzo di file di risorse per le stringhe localizzate  
  
1.  In [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni**, quindi selezionare **Aggiungi...** e **Nuovo elemento…**.  
  
2.  Selezionare **File di risorse** e assegnare il nome ErrorResources.resx al file.Scegliere **Aggiungi**.  
  
3.  Aprire il file di risorse.Aggiungere una nuova voce con il **Nome** ErrorString e il **Valore** "L'attività non è valida".  
  
4.  Aggiungere le seguenti istruzioni `using` alla classe.  
  
    ```  
    using System.Reflection;  
    using System.Resources;  
  
    ```  
  
5.  Creare un gestore di risorse nel progetto.  
  
    ```  
    ResourceManager ErrorManager;  
    ...  
    ErrorManager = new ResourceManager("MyNamespace.ErrorResources", Assembly.GetExecutingAssembly());  
  
    ```  
  
6.  Ottenere la stringa dal gestore di risorse in cui è richiesta.  
  
    ```  
    String errorMessage = ErrorManager.GetString("ErrorString");  
  
    ```  
  
 Nell'esempio di codice seguente viene illustrato come utilizzare le stringhe localizzate nel metodo <xref:System.Activities.Activity.CacheMetadata%2A>.  
  
```  
       protected override void CacheMetadata(CodeActivityMetadata metadata)  
        {  
           .....  
          // rest of the code elided for brevity  
           .....  
            if (this.Value != null && this.To != null)  
            {  
                if (!TypeHelper.AreTypesCompatible(this.Value.ArgumentType, this.To.ArgumentType))  
                {  
//---------------------------------------------  
// ** SR.TypeMismatchForAssign will fetch the string from the resource manager **  
//---------------------------------------------  
                    metadata.AddValidationError(SR.TypeMismatchForAssign(  
                                this.Value.ArgumentType,  
                                this.To.ArgumentType,  
                                this.DisplayName));  
                }  
            }  
        }  
```