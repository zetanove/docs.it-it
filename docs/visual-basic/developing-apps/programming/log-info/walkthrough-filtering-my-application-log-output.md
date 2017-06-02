---
title: Filtro dell&quot;output di My.Application.Log (Visual Basic) | Microsoft Docs
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
- My.Log object, filtering output
- My.Application.Log object, filtering output
- application event logs, output filtering
ms.assetid: 2c0a457a-38a4-49e1-934d-a51320b7b4ca
caps.latest.revision: 22
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: c0b8b0a4174527d1fc512b461355d2508e34e152
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="walkthrough-filtering-myapplicationlog-output-visual-basic"></a>Procedura dettagliata: filtro dell'output di My.Application.Log
Questa procedura dettagliata illustra come modificare il filtro di log predefinito per l'oggetto `My.Application.Log` per stabilire quali informazioni vengono passate dall'oggetto `Log` ai listener e quali informazioni vengono scritte dai listener. È possibile modificare il comportamento di registrazione anche dopo la compilazione dell'applicazione, poiché le informazioni di configurazione vengono archiviate nel file di configurazione dell'applicazione.  
  
## <a name="getting-started"></a>Introduzione  
 A ogni messaggio scritto da `My.Application.Log` è associato un livello di gravità, che i meccanismi di filtro usano per controllare l'output del log. Questa applicazione di esempio usa i metodi `My.Application.Log` per scrivere alcuni messaggi di log con diversi livelli di gravità.  
  
#### <a name="to-build-the-sample-application"></a>Per compilare l'applicazione di esempio  
  
1.  Aprire un nuovo progetto Applicazione Windows in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
2.  Aggiungere un pulsante denominato Button1 a Form1.  
  
3.  Aggiungere il codice seguente al gestore eventi <xref:System.Windows.Forms.Control.Click> per Button1:  
  
     [!code-vb[VbVbcnMyApplicationLogFiltering#1](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-filtering-my-application-log-output_1.vb)]  
  
4.  Eseguire l'applicazione nel debugger.  
  
5.  Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti nel file di log e di output di debug dell'applicazione.  
  
     `DefaultSource Information: 0 : In Button1_Click`  
  
     `DefaultSource Error: 2 : Error in the application.`  
  
6.  Chiudere l'applicazione.  
  
     Per informazioni su come visualizzare la finestra di output di debug dell'applicazione, vedere [Finestra di output](https://docs.microsoft.com/visualstudio/ide/reference/output-window). Per informazioni sul percorso del file di log dell'applicazione, vedere [Procedura dettagliata: Individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
    > [!NOTE]
    >  Per impostazione predefinita, l'applicazione elimina l'output del file di log alla chiusura dell'applicazione.  
  
     Nell'esempio precedente la seconda chiamata al metodo <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> e la chiamata al metodo <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> generano l'output del log, mentre non lo generano la prima e l'ultima chiamata al metodo `WriteEntry`. Questo avviene poiché i livelli di gravità di `WriteEntry` e `WriteException` sono "Information" ed "Error", entrambi consentiti dal filtro di log predefinito dell'oggetto `My.Application.Log`. Tuttavia, agli eventi con i livelli di gravità "Start" e "Stop" non è consentito creare output di log.  
  
## <a name="filtering-for-all-myapplicationlog-listeners"></a>Filtro per tutti i listener di My.Application.Log  
 L'oggetto `My.Application.Log` usa una classe <xref:System.Diagnostics.SourceSwitch> denominata `DefaultSwitch` per stabilire quali messaggi vengono passati dai metodi `WriteEntry` e `WriteException` ai listener di log. È possibile configurare `DefaultSwitch` nel file di configurazione dell'applicazione impostando il relativo valore su uno dei valori di enumerazione di <xref:System.Diagnostics.SourceLevels>. Per impostazione predefinita, il valore è "Information".  
  
 Questa tabella illustra il livello di gravità richiesto al log per la scrittura di un messaggio ai listener, data un'impostazione `DefaultSwitch` specifica.  
  
|Valore DefaultSwitch|Gravità del messaggio richiesto per l'output|  
|---|---| 
|`Critical`|`Critical`|  
|`Error`|`Critical` o `Error`|  
|`Warning`|`Critical`, `Error` o `Warning`|  
|`Information`|`Critical`, `Error`, `Warning` o `Information`|  
|`Verbose`|`Critical`, `Error`, `Warning`, `Information` o `Verbose`|  
|`ActivityTracing`|`Start`, `Stop`, `Suspend`, `Resume` o `Transfer`|  
|`All`|Sono consentiti tutti i messaggi.|  
|`Off`|Tutti i messaggi vengono bloccati.|  
  
> [!NOTE]
>  I metodi `WriteEntry` e `WriteException` hanno entrambi un overload che non specifica un livello di gravità. Il livello di gravità implicito per l'overload di `WriteEntry` è "Information" e il livello di gravità implicito per l'overload `WriteException` è "Error".  
  
 In questa tabella viene illustrato l'output di log dell'esempio precedente: con l'impostazione predefinita "Information" per `DefaultSwitch` solo la seconda chiamata al metodo `WriteEntry` e la chiamata al `WriteException` producono output di log.  
  
#### <a name="to-log-only-activity-tracing-events"></a>Per registrare solo gli eventi di traccia attività  
  
1.  Fare clic con il pulsante destro del mouse su app.config **Esplora soluzioni** e selezionare **Apri**.  
  
     -oppure-  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Individuare la sezione `<switches>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
3.  Trovare l'elemento che consente di aggiungere `DefaultSwitch` alla raccolta di opzioni. Deve essere simile all'elemento seguente:  
  
     `<add name="DefaultSwitch" value="Information" />`  
  
4.  Modificare il valore dell'attributo `value` impostandolo su "ActivityTracing".  
  
5.  Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="ActivityTracing" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
6.  Eseguire l'applicazione nel debugger.  
  
7.  Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti nel file di log e di output di debug dell'applicazione:  
  
     `DefaultSource Start: 4 : Entering Button1_Click`  
  
     `DefaultSource Stop: 5 : Leaving Button1_Click`  
  
8.  Chiudere l'applicazione.  
  
9. Impostare di nuovo il valore dell'attributo `value` su "Information".  
  
    > [!NOTE]
    >  L'impostazione dell'opzione `DefaultSwitch` controlla solo `My.Application.Log`. Non modifica il comportamento delle classi <xref:System.Diagnostics.Trace?displayProperty=fullName> e <xref:System.Diagnostics.Debug?displayProperty=fullName> di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
## <a name="individual-filtering-for-myapplicationlog-listeners"></a>Filtro individuale per i listener di My.Application.Log  
 Nell'esempio precedente viene illustrato come modificare il filtro per tutto l'output di `My.Application.Log`. Questo esempio illustra come filtrare un singolo listener di log. Per impostazione predefinita, un'applicazione ha due listener che scrivono nell'output di debug dell'applicazione e nel file di log.  
  
 Il file di configurazione controlla il comportamento dei listener di log, consentendo a ognuno di essi di avere un filtro, che è simile a un'opzione per `My.Application.Log`. Un listener di log genera un messaggio solo se la gravità del messaggio è consentita sia dall'opzione `DefaultSwitch` del log, sia dal filtro del listener di log.  
  
 In questo esempio viene illustrato come configurare il filtro per un nuovo listener di debug e aggiungerlo all'oggetto `Log`. Il listener di debug predefinito deve essere rimosso dall'oggetto `Log` in modo che sia chiaro che i messaggi di debug provengono dal nuovo listener di debug.  
  
#### <a name="to-log-only-activity-tracing-events"></a>Per registrare solo gli eventi di traccia attività  
  
1.  Fare clic con il pulsante destro del mouse su app.config in **Esplora soluzioni** e scegliere **Apri**.  
  
     -oppure-  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Fare clic con il pulsante destro del mouse su app.config in **Esplora soluzioni**. Scegliere **Apri**.  
  
3.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>` . La sezione `<sources>` si trova nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
4.  Aggiungere l'elemento seguente alla sezione `<listeners>`:  
  
    ```xml  
    <!-- Remove the default debug listener. -->  
    <remove name="Default"/>  
    <!-- Add a filterable debug listener. -->  
    <add name="NewDefault"/>  
    ```  
  
5.  Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
6.  Aggiungere l'elemento seguente alla sezione `<sharedListeners>` :  
  
    ```xml  
    <add name="NewDefault"   
         type="System.Diagnostics.DefaultTraceListener,   
               System, Version=2.0.0.0, Culture=neutral,   
               PublicKeyToken=b77a5c561934e089,   
               processorArchitecture=MSIL">  
        <filter type="System.Diagnostics.EventTypeFilter"   
                initializeData="Error" />  
    </add>  
    ```  
  
     Il filtro <xref:System.Diagnostics.EventTypeFilter> accetta uno dei valori di enumerazione di <xref:System.Diagnostics.SourceLevels> come proprio attributo `initializeData`.  
  
7.  Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Remove the default debug listener. -->  
              <remove name="Default"/>  
              <!-- Add a filterable debug listener. -->  
              <add name="NewDefault"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="Information" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
          <add name="NewDefault"   
               type="System.Diagnostics.DefaultTraceListener,   
                     System, Version=2.0.0.0, Culture=neutral,   
                     PublicKeyToken=b77a5c561934e089,   
                     processorArchitecture=MSIL">  
            <filter type="System.Diagnostics.EventTypeFilter"   
                    initializeData="Error" />  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
8.  Eseguire l'applicazione nel debugger.  
  
9. Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti nel file di log dell'applicazione:  
  
     `Default Information: 0 : In Button1_Click`  
  
     `Default Error: 2 : Error in the application.`  
  
     L'applicazione scrive meno informazioni nell'output di debug dell'applicazione perché il filtro è più restrittivo.  
  
     `Default Error   2   Error`  
  
10. Chiudere l'applicazione.  
  
 Per altre informazioni sulla modifica delle impostazioni del log dopo la distribuzione, vedere [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)   
 [Procedura dettagliata: Modifica della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [Procedura dettagliata: Creazione di listener di log personalizzati](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)   
 [Procedura: Scrivere messaggi di log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Opzioni di traccia](../../../../framework/debug-trace-profile/trace-switches.md)   
 [Registrazione di informazioni relative all'applicazione](../../../../visual-basic/developing-apps/programming/log-info/logging-information-from-the-application.md)
