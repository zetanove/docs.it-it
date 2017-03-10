---
title: "Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "oggetto My.Application.Log, procedure dettagliate"
  - "log eventi, modifica del percorso di output"
ms.assetid: ecc74f95-743c-450d-93f6-09a30db0fe4a
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione. Questa procedura dettagliata mostra come eseguire l'override delle impostazioni predefinite e fare in modo che l'oggetto `Log` scriva le informazioni in altri listener di log.  
  
## Prerequisiti  
 L'oggetto `Log` può scrivere le informazioni in diversi listener di log. Prima di modificare le configurazioni dei listener di log è necessario determinarne la configurazione corrente. Per altre informazioni, vedere [Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
 Può essere opportuno consultare [How to: Write Event Information to a Text File](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md) o [Procedura: scrivere nel log eventi di un'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md).  
  
### Per aggiungere listener  
  
1.  Fare clic con il pulsante destro del mouse sul file app.config in **Esplora soluzioni**, quindi scegliere **Apri**.  
  
     \-oppure\-  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento**dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>`. La sezione `<sources>` si trova nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>`.  
  
3.  Aggiungere gli elementi seguenti alla sezione `<listeners>`.  
  
    ```  
    <!-- Uncomment to connect the application file log. -->  
    <!-- <add name="FileLog" /> -->  
    <!-- Uncomment to connect the event log. -->  
    <!-- <add name="EventLog" /> -->  
    <!-- Uncomment to connect the event log. -->  
    <!-- <add name="Delimited" /> -->  
    <!-- Uncomment to connect the XML log. -->  
    <!-- <add name="XmlWriter" /> -->  
    <!-- Uncomment to connect the console log. -->  
    <!-- <add name="Console" /> -->  
    ```  
  
4.  Rimuovere il commento dai listener di log per i quali si vuole ricevere i messaggi di `Log`.  
  
5.  Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>`.  
  
6.  Aggiungere gli elementi seguenti alla sezione `<sharedListeners>`.  
  
    ```  
    <add name="FileLog"  
         type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
               Microsoft.VisualBasic, Version=8.0.0.0,   
               Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
         initializeData="FileLogWriter" />  
    <add name="EventLog"  
         type="System.Diagnostics.EventLogTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="sample application"/>  
    <add name="Delimited"   
         type="System.Diagnostics.DelimitedListTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="c:\temp\sampleDelimitedFile.txt"  
         traceOutputOptions="DateTime" />  
    <add name="XmlWriter"  
         type="System.Diagnostics.XmlWriterTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="c:\temp\sampleLogFile.xml" />  
    <add name="Console"  
         type="System.Diagnostics.ConsoleTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="true" />  
    ```  
  
7.  Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Uncomment to connect the application file log. -->  
              <!-- <add name="FileLog" /> -->  
              <!-- Uncomment to connect the event log. -->  
              <!-- <add name="EventLog" /> -->  
              <!-- Uncomment to connect the event log. -->  
              <!-- <add name="Delimited" /> -->  
              <!-- Uncomment to connect the XML log. -->  
              <!-- <add name="XmlWriter" /> -->  
              <!-- Uncomment to connect the console log. -->  
              <!-- <add name="Console" /> -->  
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
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
               initializeData="FileLogWriter" />  
          <add name="EventLog"  
               type="System.Diagnostics.EventLogTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="sample application"/>  
          <add name="Delimited"   
               type="System.Diagnostics.DelimitedListTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="c:\temp\sampleDelimitedFile.txt"  
               traceOutputOptions="DateTime" />  
          <add name="XmlWriter"  
               type="System.Diagnostics.XmlWriterTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="c:\temp\sampleLogFile.xml" />  
          <add name="Console"  
               type="System.Diagnostics.ConsoleTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="true" />  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
### Per riconfigurare un listener  
  
1.  Individuare l'elemento `<add>` del listener nella sezione `<sharedListeners>`.  
  
2.  L'attributo `type` fornisce il nome del tipo di listener. Questo tipo deve ereditare dalla classe <xref:System.Diagnostics.TraceListener>. Usare il tipo con nome sicuro per assicurarsi di usare il tipo corretto. Per altre informazioni, vedere la sezione seguente "Per aggiungere riferimenti a un tipo con nome sicuro".  
  
     Di seguito sono riportati alcuni esempi di listener che si possono usare.  
  
    -   Il listener <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName>, che scrive le informazioni in un log file.  
  
    -   Il listener <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>, che scrive le informazioni nel log eventi del computer specificato dal parametro `initializeData`.  
  
    -   I listener <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> e <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName>, che scrivono le informazioni nel file specificato nel parametro `initializeData`.  
  
    -   Il listener <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName>, che scrive le informazioni nella console della riga di comando.  
  
     Per sapere dove gli altri tipi di listener di log scrivono le informazioni, consultare la documentazione relativa al tipo di listener desiderato.  
  
3.  Quando crea l'oggetto listener di log, l'applicazione passa l'attributo `initializeData` come parametro del costruttore. Il significato dell'attributo `initializeData` dipende dal listener di traccia.  
  
4.  Dopo aver creato il listener di log, l'applicazione imposta le proprietà del listener. Tali proprietà sono definite dagli altri attributi contenuti nell'elemento `<add>`. Per altre informazioni sulle proprietà di un determinato listener, consultare la documentazione relativa al tipo di listener corrispondente.  
  
### Per aggiungere riferimenti a un tipo con nome sicuro  
  
1.  Per assicurarsi di usare il tipo di listener di log appropriato, usare il nome di tipo completo e il nome di assembly sicuro. La sintassi di un tipo con nome sicuro è la seguente:  
  
     \<*nome tipo*\>, \<*nome assembly*\>, \<*numero versione*\>, \<*impostazioni cultura*\>, \<*nome sicuro*\>  
  
2.  L'esempio di codice seguente mostra come determinare il tipo con nome sicuro per un tipo completo, in questo caso "System.Diagnostics.FileLogTraceListener".  
  
     [!code-vb[VbVbalrMyApplicationLog#15](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/visualbasic/VbVbalrMyApplicationLog/Form1.vb#15)]  
  
     Questo è l'output, e può essere usato per aggiungere riferimenti univoci a un tipo con nome sicuro, come nella procedura "Per aggiungere listener" precedente.  
  
     `Microsoft.VisualBasic.Logging.FileLogTraceListener, Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a`  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName>   
 <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>   
 [How to: Write Event Information to a Text File](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)   
 [Procedura: scrivere nel log eventi di un'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)