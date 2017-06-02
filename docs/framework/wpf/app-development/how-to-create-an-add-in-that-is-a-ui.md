---
title: "Procedura: creare un componente aggiuntivo che costituisce un&#39;interfaccia utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "creazione di un componente aggiuntivo rappresentante un'interfaccia utente [WPF]"
  - "componenti aggiuntivi [WPF], interfaccia utente"
  - "creazione di componenti aggiuntivi dell'interfaccia utente [WPF]"
  - "Interfaccia utente componenti aggiuntivi [WPF], creazione"
  - "implementazione di componenti aggiuntivi dell'interfaccia utente [WPF]"
  - "segmenti di pipeline [WPF], creazione di componenti aggiuntivi"
ms.assetid: 86375525-282b-4039-8352-8680051a10ea
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: creare un componente aggiuntivo che costituisce un&#39;interfaccia utente
\<?xml version="1.0" encoding="utf-8"?>
\<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>In questo esempio viene illustrato come creare un componente aggiuntivo che è un <token>TLA #tla_wpf</token> <token>TLA #tla_ui</token> ed è ospitato da un <token>TLA&#2;tla_wpf</token> applicazione autonoma.</para> 
    <para>Il componente aggiuntivo è un <token>TLA&#2;tla_ui</token> vale a dire un <token>TLA&#2;tla_wpf</token> controllo utente. Il contenuto del controllo utente è un singolo pulsante che, quando si fa clic, viene visualizzato un messaggio. Il <token>TLA&#2;tla_wpf</token> applicazione autonoma ospita il componente aggiuntivo <token>TLA&#2;tla_ui</token> come il contenuto della finestra principale dell'applicazione.</para> 
    <para> 
      <embeddedLabel>Prerequisiti</embeddedLabel>
    </para>
    <para>quest'esempio evidenzia il <token>TLA&#2;tla_wpf</token> estensioni per il <token>dnprdnshort</token> modello del componente aggiuntivo che abilitare questo scenario e si presuppongono le seguenti:</para>
    <list class="bullet">
      <listItem>
        <para>conoscere il <token>dnprdnshort</token> modello componente aggiuntivo, tra cui sviluppo di pipeline, componenti aggiuntivi e host. Se non si ha familiarità con questi concetti, vedere \<legacyLink xlink:href="8dd45b02-7218-40f9-857d-40d7b98b850b">componenti aggiuntivi ed estensibilità</legacyLink>. Per un'esercitazione che illustra l'implementazione di una pipeline, un componente aggiuntivo e un'applicazione host, vedere \<legacyLink xlink:href="694a33c5-a040-450d-aed5-ac49fc88ce61">procedura dettagliata: creazione di un'applicazione estensibile</legacyLink>.</para> 
      </listItem> 
      <listItem> 
        <para>Conoscere il <token>TLA&#2;tla_wpf</token> estensioni per il <token>dnprdnshort</token> modello del componente aggiuntivo, che sono disponibili qui: \<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">Cenni preliminari sui componenti aggiuntivi di WPF</link>.</para> 
      </listItem> 
    </list> 
  </introduction> 
  <codeExample> 
    <legacy> 
      <content> 
        <para>Per creare un componente aggiuntivo che è un <token>TLA&#2;tla_wpf</token> <token>TLA&#2;tla_ui</token> richiede codice specifico per ogni segmento di pipeline, il componente aggiuntivo e l'applicazione host.</para> 
        <para> 
          <token>autoOutline</token>
        </para>
      </content>
      <sections>
        <section address="Contract">
          <title>Implementazione del segmento di Pipeline contratto</title>
          <content>
            <para>quando un componente aggiuntivo è un <token>TLA&#2;tla_ui</token>, il contratto per il componente aggiuntivo deve implementare <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>. Nell'esempio <codeInline>IWPFAddInContract</codeInline> implementa <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>, come illustrato nel codice seguente.</para>
            <code language="c#">using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // AddInContractAttribute

namespace Contracts
{
    /// &lt;summary&gt;
    /// Defines the services that an add-in will provide to a host application.
    /// In this case, the add-in is a UI.
    /// &lt;/summary&gt;
    [AddInContract]
    public interface IWPFAddInContract : INativeHandleContract {}
}</code>
          <code language="vb">Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' AddInContractAttribute

Namespace Contracts
    ''' &lt;summary&gt;
    ''' Defines the services that an add-in will provide to a host application.
    ''' In this case, the add-in is a UI.
    ''' &lt;/summary&gt;
    &lt;AddInContract&gt;
    Public Interface IWPFAddInContract
        Inherits INativeHandleContract
        Inherits IContract
    End Interface
End Namespace</code></content>
        </section>
        <section address="AddInViewPipeline">
          <title>Implementazione del segmento di Pipeline visualizzazione componente aggiuntivo</title>
          <content>
            <para>perché il componente aggiuntivo viene implementato come una sottoclasse di <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> tipo, la visualizzazione del componente aggiuntivo deve inoltre creare una sottoclasse <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference>. Il codice seguente viene illustrata la visualizzazione del componente aggiuntivo del contratto, implementato come il <codeInline>WPFAddInView</codeInline> classe</para> 
            <code language="c#">using System.AddIn.Pipeline; // AddInBaseAttribute
using System.Windows.Controls; // UserControl

namespace AddInViews
{
    /// &lt;summary&gt;
    /// Defines the add-in's view of the contract.
    /// &lt;/summary&gt;
    [AddInBase]
    public class WPFAddInView : UserControl { }
}</code> 
          <code language="vb">Imports System.AddIn.Pipeline ' AddInBaseAttribute
Imports System.Windows.Controls ' UserControl

Namespace AddInViews
    ''' &lt;summary&gt;
    ''' Defines the add-in's view of the contract.
    ''' &lt;/summary&gt;
    &lt;AddInBase&gt;
    Public Class WPFAddInView
        Inherits UserControl
    End Class
End Namespace</code> 
            <para>In questo caso, la visualizzazione del componente aggiuntivo deriva da <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference>. Di conseguenza, il componente aggiuntivo <token>TLA&#2;tla_ui</token> anche deve derivare da <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference>.</para>
          </content>
        </section>
        <section address="AddInSideAdapter">
          <title>Implementazione del segmento di Pipeline dell'adattatore Add-In-Side</title>
          <content>
            <para>mentre il contratto è un <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>, il componente aggiuntivo è un <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> (come specificato dal segmento di pipeline del componente aggiuntivo). Pertanto, il <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> deve essere convertito in un <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> prima di oltrepassare il limite di isolamento. Questa operazione viene eseguita dall'adattatore lato componente aggiuntivo chiamando <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter (System.Windows.FrameworkElement)</codeEntityReference>, come illustrato nel codice seguente.</para> 
            <code language="c#">using System; // IntPtr
using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // AddInAdapterAttribute, FrameworkElementAdapters, ContractBase
using System.Security.Permissions;

using AddInViews; // WPFAddInView
using Contracts; // IWPFAddInContract

namespace AddInSideAdapters
{
    /// &lt;summary&gt;
    /// Adapts the add-in's view of the contract to the add-in contract
    /// &lt;/summary&gt;
    [AddInAdapter]
    public class WPFAddIn_ViewToContractAddInSideAdapter : ContractBase, IWPFAddInContract
    {
        WPFAddInView wpfAddInView;

        public WPFAddIn_ViewToContractAddInSideAdapter(WPFAddInView wpfAddInView)
        {
            // Adapt the add-in view of the contract (WPFAddInView) 
            // to the contract (IWPFAddInContract)
            this.wpfAddInView = wpfAddInView;
        }

        /// &lt;summary&gt;
        /// ContractBase.QueryContract must be overridden to:
        /// * Safely return a window handle for an add-in UI to the host 
        ///   application's application.
        /// * Enable tabbing between host application UI and add-in UI, in the
        ///   "add-in is a UI" scenario.
        /// &lt;/summary&gt;
        public override IContract QueryContract(string contractIdentifier)
        {
            if (contractIdentifier.Equals(typeof(INativeHandleContract).AssemblyQualifiedName))
            {
                return FrameworkElementAdapters.ViewToContractAdapter(this.wpfAddInView);
            }

            return base.QueryContract(contractIdentifier);
        }

        /// &lt;summary&gt;
        /// GetHandle is called by the WPF add-in model from the host application's 
        /// application domain to to get the window handle for an add-in UI from the 
        /// add-in's application domain. GetHandle is called if a window handle isn't 
        /// returned by other means ie overriding ContractBase.QueryContract, 
        /// as shown above.
        /// NOTE: This method requires UnmanagedCodePermission to be called 
        ///       (full-trust by default), to prevent illegal window handle
        ///       access in partially trusted scenarios. If the add-in could
        ///       run in a partially trusted application domain 
        ///       (eg AddInSecurityLevel.Internet), you can safely return a window
        ///       handle by overriding ContractBase.QueryContract, as shown above.
        /// &lt;/summary&gt;
        [SecurityPermissionAttribute(SecurityAction.Demand, Flags = SecurityPermissionFlag.UnmanagedCode)]
        public IntPtr GetHandle()
        {
            return FrameworkElementAdapters.ViewToContractAdapter(this.wpfAddInView).GetHandle();
        }
    }
}</code> 
          <code language="vb">Imports System ' IntPtr
Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' AddInAdapterAttribute, FrameworkElementAdapters, ContractBase
Imports System.Security.Permissions

Imports AddInViews ' WPFAddInView
Imports Contracts ' IWPFAddInContract

Namespace AddInSideAdapters
    ''' &lt;summary&gt;
    ''' Adapts the add-in's view of the contract to the add-in contract
    ''' &lt;/summary&gt;
    &lt;AddInAdapter&gt;
    Public Class WPFAddIn_ViewToContractAddInSideAdapter
        Inherits ContractBase
        Implements IWPFAddInContract

        Private wpfAddInView As WPFAddInView

        Public Sub New(ByVal wpfAddInView As WPFAddInView)
            ' Adapt the add-in view of the contract (WPFAddInView) 
            ' to the contract (IWPFAddInContract)
            Me.wpfAddInView = wpfAddInView
        End Sub

        ''' &lt;summary&gt;
        ''' ContractBase.QueryContract must be overridden to:
        ''' * Safely return a window handle for an add-in UI to the host 
        '''   application's application.
        ''' * Enable tabbing between host application UI and add-in UI, in the
        '''   "add-in is a UI" scenario.
        ''' &lt;/summary&gt;
        Public Overrides Function QueryContract(ByVal contractIdentifier As String) As IContract
            If contractIdentifier.Equals(GetType(INativeHandleContract).AssemblyQualifiedName) Then
                Return FrameworkElementAdapters.ViewToContractAdapter(Me.wpfAddInView)
            End If

            Return MyBase.QueryContract(contractIdentifier)
        End Function

        ''' &lt;summary&gt;
        ''' GetHandle is called by the WPF add-in model from the host application's 
        ''' application domain to to get the window handle for an add-in UI from the 
        ''' add-in's application domain. GetHandle is called if a window handle isn't 
        ''' returned by other means ie overriding ContractBase.QueryContract, 
        ''' as shown above.
        ''' NOTE: This method requires UnmanagedCodePermission to be called 
        '''       (full-trust by default), to prevent illegal window handle
        '''       access in partially trusted scenarios. If the add-in could
        '''       run in a partially trusted application domain 
        '''       (eg AddInSecurityLevel.Internet), you can safely return a window
        '''       handle by overriding ContractBase.QueryContract, as shown above.
        ''' &lt;/summary&gt;
        &lt;SecurityPermissionAttribute(SecurityAction.Demand, Flags:=SecurityPermissionFlag.UnmanagedCode)&gt;
        Public Function GetHandle() As IntPtr Implements INativeHandleContract.GetHandle
            Return FrameworkElementAdapters.ViewToContractAdapter(Me.wpfAddInView).GetHandle()
        End Function

    End Class
End Namespace</code> 
            <para>Nel modello componente aggiuntivo in cui un componente aggiuntivo che restituisce un <token>TLA&#2;tla_ui</token> (vedere \<link xlink:href="57f274b7-4c66-4b72-92eb-81939a393776">procedura: creare un componente aggiuntivo che restituisce un'interfaccia utente</link>), convertita adattatore componente aggiuntivo il <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> per un <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> chiamando <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter (System.Windows.FrameworkElement)</codeEntityReference>. <codeEntityReference autoUpgrade="true">M:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter (System.Windows.FrameworkElement)</codeEntityReference> deve essere chiamato anche in questo modello, anche se è necessario implementare un metodo da cui scrivere il codice per chiamarla. A tale scopo, si esegue l'override <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.ContractBase.QueryContract</codeEntityReference> e implementare il codice che chiama <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter (System.Windows.FrameworkElement)</codeEntityReference> se il codice che chiama <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.ContractBase.QueryContract</codeEntityReference> prevede un <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>. In questo caso, il chiamante sarà l'adattatore lato host, disponibile in una sottosezione successiva.</para>
            <alert class="note">
              <para> È inoltre necessario eseguire l'override <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.ContractBase.QueryContract</codeEntityReference> in questo modello per abilitare la tabulazione tra l'applicazione host <token>TLA&#2;tla_ui</token> e componente aggiuntivo <token>TLA&#2;tla_ui</token>. Per ulteriori informazioni, vedere "Limitazioni componenti WPF" in \<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">WPF Add-Ins Overview</link>.</para> 
            </alert> 
            <para>Poiché l'adattatore lato componente aggiuntivo implementa un'interfaccia che deriva da <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>, è necessario implementare <codeEntityReference autoUpgrade="true">M:System.AddIn.Contract.INativeHandleContract.GetHandle</codeEntityReference>, anche se questo parametro viene ignorato quando <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.ContractBase.QueryContract</codeEntityReference> viene sottoposto a override.</para>
          </content>
        </section>
        <section address="HostViewPipeline">
          <title>Implementazione del segmento di Pipeline vista Host</title>
          <content>
            <para>In questo modello, l'applicazione host prevede in genere la visualizzazione host deve essere un <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> sottoclasse. L'adattatore lato host deve convertire il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> per un <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> dopo il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> supera il limite di isolamento. Perché un metodo non viene chiamato dall'applicazione host per ottenere il <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference>, la visualizzazione host deve "return" il <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> da che lo contiene. Di conseguenza, la visualizzazione host deve derivare da una sottoclasse di <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> che possono contenere altri <token>TLA&#2;tla_ui #plural</token>, ad esempio <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference>. Il codice seguente viene illustrata la visualizzazione host del contratto, implementato come il <codeInline>WPFAddInHostView</codeInline> (classe).</para>
            <code language="c#">using System.Windows.Controls; // UserControl

namespace HostViews
{
    /// &lt;summary&gt;
    /// Defines the host's view of the add-in
    /// &lt;/summary&gt;
    public class WPFAddInHostView : UserControl { }
}</code>
          <code language="vb">Imports System.Windows.Controls ' UserControl

Namespace HostViews
    ''' &lt;summary&gt;
    ''' Defines the host's view of the add-in
    ''' &lt;/summary&gt;
    Public Class WPFAddInHostView
        Inherits UserControl
    End Class
End Namespace</code>
          </content>
        </section>
        <section address="HostSideAdapter">
          <title>Implementazione del segmento di Pipeline dell'adattatore lato Host</title>
          <content>
            <para>mentre il contratto è un <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference>, l'applicazione host prevede un <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference> (come specificato dalla visualizzazione host). Di conseguenza, il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> deve essere convertito in un <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> dopo aver oltrepassato il limite di isolamento, prima di essere impostato come contenuto della visualizzazione host (che deriva da <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference>).</para> 
            <para>La conversione viene eseguita dall'adattatore lato host, come illustrato nel codice seguente. </para> 
            <code language="c#">using System.AddIn.Contract; // INativeHandleContract
using System.AddIn.Pipeline; // HostAdapterAttribute, FrameworkElementAdapters, ContractHandle
using System.Windows; // FrameworkElement

using Contracts; // IWPFAddInContract
using HostViews; // WPFAddInHostView

namespace HostSideAdapters
{
    /// &lt;summary&gt;
    /// Adapts the add-in contract to the host's view of the add-in
    /// &lt;/summary&gt;
    [HostAdapter]
    public class WPFAddIn_ContractToViewHostSideAdapter : WPFAddInHostView
    {
        IWPFAddInContract wpfAddInContract;
        ContractHandle wpfAddInContractHandle;

        public WPFAddIn_ContractToViewHostSideAdapter(IWPFAddInContract wpfAddInContract)
        {
            // Adapt the contract (IWPFAddInContract) to the host application's
            // view of the contract (WPFAddInHostView)
            this.wpfAddInContract = wpfAddInContract;

            // Prevent the reference to the contract from being released while the
            // host application uses the add-in
            this.wpfAddInContractHandle = new ContractHandle(wpfAddInContract);

            // Convert the INativeHandleContract for the add-in UI that was passed 
            // from the add-in side of the isolation boundary to a FrameworkElement
            string aqn = typeof(INativeHandleContract).AssemblyQualifiedName;
            INativeHandleContract inhc = (INativeHandleContract)wpfAddInContract.QueryContract(aqn);
            FrameworkElement fe = (FrameworkElement)FrameworkElementAdapters.ContractToViewAdapter(inhc);

            // Add FrameworkElement (which displays the UI provided by the add-in) as
            // content of the view (a UserControl)
            this.Content = fe;
        }
    }
}</code> 
          <code language="vb">Imports System.AddIn.Contract ' INativeHandleContract
Imports System.AddIn.Pipeline ' HostAdapterAttribute, FrameworkElementAdapters, ContractHandle
Imports System.Windows ' FrameworkElement

Imports Contracts ' IWPFAddInContract
Imports HostViews ' WPFAddInHostView

Namespace HostSideAdapters
    ''' &lt;summary&gt;
    ''' Adapts the add-in contract to the host's view of the add-in
    ''' &lt;/summary&gt;
    &lt;HostAdapter&gt;
    Public Class WPFAddIn_ContractToViewHostSideAdapter
        Inherits WPFAddInHostView
        Private wpfAddInContract As IWPFAddInContract
        Private wpfAddInContractHandle As ContractHandle

        Public Sub New(ByVal wpfAddInContract As IWPFAddInContract)
            ' Adapt the contract (IWPFAddInContract) to the host application's
            ' view of the contract (WPFAddInHostView)
            Me.wpfAddInContract = wpfAddInContract

            ' Prevent the reference to the contract from being released while the
            ' host application uses the add-in
            Me.wpfAddInContractHandle = New ContractHandle(wpfAddInContract)

            ' Convert the INativeHandleContract for the add-in UI that was passed 
            ' from the add-in side of the isolation boundary to a FrameworkElement
            Dim aqn As String = GetType(INativeHandleContract).AssemblyQualifiedName
            Dim inhc As INativeHandleContract = CType(wpfAddInContract.QueryContract(aqn), INativeHandleContract)
            Dim fe As FrameworkElement = CType(FrameworkElementAdapters.ContractToViewAdapter(inhc), FrameworkElement)

            ' Add FrameworkElement (which displays the UI provided by the add-in) as
            ' content of the view (a UserControl)
            Me.Content = fe
        End Sub
    End Class
End Namespace</code> 
            <para>Come si può notare, l'adattatore lato host acquisisce il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> chiamando l'adattatore lato componente aggiuntivo <codeEntityReference autoUpgrade="true">m:System.AddIn.Pipeline.ContractBase.QueryContract</codeEntityReference> (metodo) (questo è il punto in cui il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> supera il limite di isolamento).</para> 
            <para>L'adattatore lato host converte quindi il <codeEntityReference autoUpgrade="true">T:System.AddIn.Contract.INativeHandleContract</codeEntityReference> per un <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> chiamando <codeEntityReference autoUpgrade="true">M:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter(System.AddIn.Contract.INativeHandleContract)</codeEntityReference>. Infine, il <codeEntityReference autoUpgrade="true">: System.Windows.FrameworkElement</codeEntityReference> viene impostato come il contenuto della visualizzazione host.</para>
          </content>
        </section>
        <section address="AddIn">
          <title>Implementazione del componente aggiuntivo</title>
          <content>
            <para>con l'adattatore lato componente aggiuntivo e visualizzazione componente aggiuntivo sul posto, il componente aggiuntivo può essere implementato mediante la derivazione dalla visualizzazione componente aggiuntivo, come illustrato nel codice seguente.</para> 
            <code language="xaml">&lt;addInViews:WPFAddInView
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:addInViews="clr-namespace:AddInViews;assembly=AddInViews"
    x:Class="WPFAddIn1.AddInUI"&gt;

    &lt;Grid&gt;
        &lt;Button Click="clickMeButton_Click" Content="Click Me!" /&gt;        
    &lt;/Grid&gt;

&lt;/addInViews:WPFAddInView&gt;</code> 
            <code language="c#">using System.AddIn; // AddInAttribute
using System.Windows; // MessageBox, RoutedEventArgs

using AddInViews; // WPFAddInView

namespace WPFAddIn1
{
    /// &lt;summary&gt;
    /// Implements the add-in by deriving from WPFAddInView
    /// &lt;/summary&gt;
    [AddIn("WPF Add-In 1")]
    public partial class AddInUI : WPFAddInView
    {
        public AddInUI()
        {
            InitializeComponent();
        }

        void clickMeButton_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Hello from WPFAddIn1");
        }
    }
}</code> 
          <code language="vb">Imports System.AddIn ' AddInAttribute
Imports System.Windows ' MessageBox, RoutedEventArgs

Imports AddInViews ' WPFAddInView

Namespace WPFAddIn1
    ''' &lt;summary&gt;
    ''' Implements the add-in by deriving from WPFAddInView
    ''' &lt;/summary&gt;
    &lt;AddIn("WPF Add-In 1")&gt;
    Partial Public Class AddInUI
        Inherits WPFAddInView
        Public Sub New()
            InitializeComponent()
        End Sub

        Private Sub clickMeButton_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            MessageBox.Show("Hello from WPFAddIn1")
        End Sub
    End Class
End Namespace</code> 
            <para>Da questo esempio, è possibile vedere un interessante vantaggio di questo modello: componenti gli sviluppatori devono semplicemente implementare il componente aggiuntivo (poiché si tratta di <token>TLA&#2;tla_ui</token> nonché), anziché una classe di componente aggiuntivo e un componente aggiuntivo <token>TLA&#2;tla_ui</token>.</para>
          </content>
        </section>
        <section address="HostApp">
          <title>Implementazione dell'applicazione Host</title>
          <content>
            <para>con l'adattatore lato host e la visualizzazione host creato, l'applicazione host può utilizzare il <token>dnprdnshort</token> modello componente aggiuntivo per aprire la pipeline e acquisire una visualizzazione host del componente aggiuntivo. Nel codice seguente vengono illustrati i diversi passaggi. </para> 
            <code language="c#">// Get add-in pipeline folder (the folder in which this application was launched from)
string appPath = Environment.CurrentDirectory;

// Rebuild visual add-in pipeline
string[] warnings = AddInStore.Rebuild(appPath);
if (warnings.Length &gt; 0)
{
    string msg = "Could not rebuild pipeline:";
    foreach (string warning in warnings) msg += "\n" + warning;
    MessageBox.Show(msg);
    return;
}

// Activate add-in with Internet zone security isolation
Collection&lt;AddInToken&gt; addInTokens = AddInStore.FindAddIns(typeof(WPFAddInHostView), appPath);
AddInToken wpfAddInToken = addInTokens[0];
this.wpfAddInHostView = wpfAddInToken.Activate&lt;WPFAddInHostView&gt;(AddInSecurityLevel.Internet);

// Display add-in UI
this.addInUIHostGrid.Children.Add(this.wpfAddInHostView);</code> 
          <code language="vb">' Get add-in pipeline folder (the folder in which this application was launched from)
Dim appPath As String = Environment.CurrentDirectory

' Rebuild visual add-in pipeline
Dim warnings() As String = AddInStore.Rebuild(appPath)
If warnings.Length &gt; 0 Then
    Dim msg As String = "Could not rebuild pipeline:"
    For Each warning As String In warnings
        msg &amp;= vbLf &amp; warning
    Next warning
    MessageBox.Show(msg)
    Return
End If

' Activate add-in with Internet zone security isolation
Dim addInTokens As Collection(Of AddInToken) = AddInStore.FindAddIns(GetType(WPFAddInHostView), appPath)
Dim wpfAddInToken As AddInToken = addInTokens(0)
Me.wpfAddInHostView = wpfAddInToken.Activate(Of WPFAddInHostView)(AddInSecurityLevel.Internet)

' Display add-in UI
Me.addInUIHostGrid.Children.Add(Me.wpfAddInHostView)</code> 
            <para>L'applicazione host usa tipico <token>dnprdnshort</token> codice del modello di componente aggiuntivo per attivare il componente aggiuntivo, il quale restituisce implicitamente la visualizzazione host per l'applicazione host. L'applicazione host successivamente, viene visualizzata la visualizzazione host (che è un <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.UserControl</codeEntityReference>) da un <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.Grid</codeEntityReference>.</para> 
            <para>Il codice di elaborazione delle interazioni con il componente aggiuntivo <token>TLA&#2;tla_ui</token> viene eseguito nel dominio dell'applicazione del componente aggiuntivo. Queste interazioni includono quanto segue:</para>
            <list class="bullet">
              <listItem>
                <para>gestisce la <codeEntityReference autoUpgrade="true">T:System.Windows.Controls.Button</codeEntityReference> <codeEntityReference autoUpgrade="true">E:System.Windows.Controls.Primitives.ButtonBase.Click</codeEntityReference> evento.</para> 
              </listItem> 
              <listItem> 
                <para>Che mostra il <codeEntityReference autoUpgrade="true">: System.Windows.MessageBox</codeEntityReference>.</para> 
              </listItem> 
            </list> 
            <para>Questa attività è completamente isolata dall'applicazione host.</para>
          </content>
        </section>
      </sections>
    </legacy>
  </codeExample>
  <relatedTopics>
\<legacyLink xlink:href="8dd45b02-7218-40f9-857d-40d7b98b850b">Componenti aggiuntivi ed estensibilità</legacyLink>
\<link xlink:href="00b4c776-29a8-4dba-b603-280a0cdc2ade">Cenni preliminari sui componenti aggiuntivi WPF</link>
</relatedTopics>
</developerHowToDocument>
