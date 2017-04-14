---
title: "Servizio solo XAML di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c106feb0-0245-43b5-aefe-93ce0e4d38eb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Servizio solo XAML di base
In questo esempio viene illustrato come creare un servizio solo XAML.Lo scenario è quello di un servizio di diagnostica per problemi correlati all'auto.Il servizio viene implementato come flusso di lavoro che pone al client una serie di domande per diagnosticare il problema.Esistono due tipi di problema diagnosticabili dal servizio \(l'auto non parte oppure l'aria condizionata non funziona\).Il flusso di lavoro utilizza il modello Request\/Reply della finestra di progettazione per esporre tre operazioni di servizio semplici.Il servizio viene ospitato in IIS creando una directory virtuale in IIS e copiando i file service1.xamlx e Web.config nella directory virtuale. Non è richiesto alcun codice compilato.Per impostazione predefinita, in questo esempio vengono automaticamente copiati i file necessari nella directory virtuale creata durante l'esecuzione delle istruzioni di installazione per gli esempi di WF e WCF: [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) quando incorporata in Visual Studio 2010.  
  
#### Per utilizzare questo esempio  
  
1.  Caricare la soluzione del progetto in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e compilare il progetto.  
  
2.  Eseguire l'applicazione client generata in \[directory soluzione di base\]\\Client\\bin\\debug.  
  
3.  L'applicazione stampa le opzioni, ne seleziona unae pone alcune domande, rispondendo con sì o no \(utilizzo di chiavi S\/N\).Quando il servizio ha diagnosticato i problemi, l'applicazione stampa una diagnosi.  
  
4.  L'applicazione torna alle opzioni.È possibile diagnosticare un altro problema o uscire dall'applicazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\XAMLService`  
  
## Vedere anche