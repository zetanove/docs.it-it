---
title: 'Procedura: Scrivere nel log eventi di un&quot;applicazione (Visual Basic) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Computer.EventLog element
- WriteEntry method
- My.Computer.EventLog element
- event logs, writing to
ms.assetid: cadbc8c1-87af-4746-934e-55b79a4f6e2b
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: ea527f0161a3bff759a8d33e4c5fa1c6c6e1df29
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-write-to-an-application-event-log-visual-basic"></a>Procedura: scrivere nel log eventi di un'applicazione (Visual Basic)
È possibile usare gli oggetti `My.Application.Log` e `My.Log` per scrivere informazioni sugli eventi che si verificano nell'applicazione. L'esempio seguente mostra come configurare un listener di log eventi in modo che `My.Application.Log` scriva le informazioni di traccia nel log eventi dell'applicazione.  
  
 Non è possibile scrivere nel log di sicurezza. Per scrivere nel log di sistema, è necessario essere membro dell'account LocalSystem o Administrator.  
  
 Per visualizzare un log eventi, è possibile usare **Esplora server** o **Visualizzatore eventi di Windows**. Per altre informazioni, vedere [ETW Events in the .NET Framework](http://msdn.microsoft.com/library/d186276f-6afb-4dfd-bf3c-4251edc2c299).  
  
> [!NOTE]
>  I log eventi non sono supportati in Windows 95, Windows 98 o Windows Millennium Edition.  
  
### <a name="to-add-and-configure-the-event-log-listener"></a>Per aggiungere e configurare il listener di log eventi  
  
1.  Fare clic con il pulsante destro del mouse sul file app.config in **Esplora soluzioni** , quindi scegliere **Apri**.  
  
     \- oppure -  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Individuare la sezione `<listeners>` nel file di configurazione dell'applicazione.  
  
     La sezione `<listeners>` si trova nella sezione `<source>` con l'attributo del nome "DefaultSource" annidato sotto la sezione `<system.diagnostics>` a sua volta annidata sotto la sezione di primo livello `<configuration>` .  
  
3.  Aggiungere l'elemento seguente alla sezione `<listeners>` :  
  
    ```  
    <add name="EventLog"/>  
    ```  
  
4.  Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
5.  Aggiungere l'elemento seguente alla sezione `<sharedListeners>` :  
  
    ```  
    <add name="EventLog"  
        type="System.Diagnostics.EventLogTraceListener, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="APPLICATION_NAME"/>  
    ```  
  
     Sostituire `APPLICATION_NAME` con il nome dell'applicazione.  
  
    > [!NOTE]
    >  In genere, nel log eventi vengono scritti solo gli errori. Per informazioni sull'applicazione dei filtri all'output dei log, vedere [Walkthrough: Filtering My.Application.Log Output](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
### <a name="to-write-event-information-to-the-event-log"></a>Per scrivere informazioni sugli eventi nel log eventi  
  
-   Usare il metodo `My.Application.Log.WriteEntry` o `My.Application.Log.WriteException` per scrivere le informazioni nel log eventi. Per altre informazioni, vedere [Procedura: Scrivere messaggi di log ](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md) e [Procedura: Registrare eccezioni](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md).  
  
     Dopo aver configurato il listener del log eventi per un assembly, vengono ricevuti tutti i messaggi che `My.Applcation.Log` scrive da tale assembly.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Procedura: Registrare eccezioni](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [Procedura dettagliata: Individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
