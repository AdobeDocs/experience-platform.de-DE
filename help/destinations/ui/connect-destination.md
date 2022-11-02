---
keywords: Ziel verbinden;Zielverbindung;Ziel verbinden;Ziel verbinden
title: Erstellen einer neuen Zielverbindung
type: Tutorial
description: Erfahren Sie, wie Sie in Adobe Experience Platform eine Verbindung zu einem Ziel herstellen, Warnhinweise aktivieren und Marketing-Aktionen für Ihr angeschlossenes Ziel einrichten.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 4%

---

# Erstellen einer neuen Zielverbindung

>[!IMPORTANT]
> 
>* Um eine Verbindung zu einem Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht zur Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Um eine Verbindung zu einem Ziel herzustellen, das Datensatzexporte unterstützt, benötigen Sie die **[!UICONTROL Verwalten und Aktivieren von Datensatzzielen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht zur Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.


## Übersicht {#overview}

Bevor Sie Zielgruppendaten an ein Ziel senden können, müssen Sie eine Verbindung zu Ihrer Zielplattform herstellen. In diesem Artikel erfahren Sie, wie Sie eine neue Zielverbindung einrichten, zu der Sie dann Segmente aktivieren oder Datensätze über die Adobe Experience Platform-Benutzeroberfläche exportieren können.

## Suchen Sie das gewünschte Ziel im Katalog {#setup}

1. Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die **[!UICONTROL Katalog]** Registerkarte.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit der Zielkatalogseite.](../assets/ui/connect-destinations/catalog.png)

2. Zielkarten im Katalog verfügen möglicherweise über unterschiedliche Aktionssteuerelemente, je nachdem, ob Sie über eine bestehende Verbindung zum Ziel verfügen und ob die Ziele die Aktivierung von Segmenten, den Export von Datensätzen oder beides unterstützen. Möglicherweise werden die folgenden Steuerelemente für Zielkarten angezeigt:

   * **[!UICONTROL Setup]**. Bevor Sie Segmente aktivieren oder Datensätze exportieren können, muss zunächst eine Verbindung zu diesem Ziel eingerichtet werden.
   * **[!UICONTROL Aktivieren]**. Für dieses Ziel wurde bereits eine Verbindung eingerichtet. Dieses Ziel unterstützt die Segmentaktivierung und den Export von Datensätzen.
   * **[!UICONTROL Aktivieren von Segmenten]**. Für dieses Ziel wurde bereits eine Verbindung eingerichtet. Dieses Ziel unterstützt nur die Segmentaktivierung.

   Weitere Informationen zum Unterschied zwischen diesen Steuerelementen finden Sie unter [Katalog](../ui/destinations-workspace.md#catalog) Abschnitt der Dokumentation zum Zielarbeitsbereich.

   Wählen Sie entweder **[!UICONTROL Einrichten]**, **[!UICONTROL Aktivieren]** oder **[!UICONTROL Segmente aktivieren]**, je nachdem, welche Kontrolle Ihnen zur Verfügung steht.

   ![Screenshot der Experience Platform-Benutzeroberfläche, auf der die Zielkatalogseite mit dem Steuerelement Einrichten hervorgehoben ist.](../assets/ui/connect-destinations/set-up.png)

   ![Screenshot der Experience Platform-Benutzeroberfläche, auf der die Zielkatalogseite mit hervorgehobenem Steuerelement Segmente aktivieren angezeigt wird.](../assets/ui/connect-destinations/activate-segments.png)

3. Wenn Sie **[!UICONTROL Einrichten]**, überspringen Sie zum nächsten Schritt, um [authentifizieren](#authenticate) zum Ziel.

   Wenn Sie **[!UICONTROL Aktivieren]**, **[!UICONTROL Segmente aktivieren]** oder **[!UICONTROL Exportieren von Datensätzen]** können Sie jetzt eine Liste der vorhandenen Zielverbindungen anzeigen.

   Auswählen **[!UICONTROL Neues Ziel konfigurieren]** , um eine neue Verbindung zum Ziel herzustellen.

   ![Screenshot der Experience Platform-Benutzeroberfläche, in der eine Liste der verfügbaren Ziele und das Steuerelement Neues Ziel konfigurieren hervorgehoben sind.](../assets/ui/connect-destinations/configure-new-destination.png)

## Beim Ziel authentifizieren {#authenticate}

Der erste Schritt beim Herstellen einer Verbindung zu einem Ziel besteht darin, sich bei der Zielplattform zu authentifizieren.

Je nach Ziel, mit dem Sie eine Verbindung herstellen, gelangen Sie möglicherweise zur Seite des Zielpartners, um sich zu authentifizieren, oder Sie werden möglicherweise aufgefordert, Authentifizierungsberechtigungen direkt im Platform-Workflow einzugeben. Nachfolgend finden Sie ein Beispiel für die erforderliche Eingabe zur Authentifizierung bei einem [!DNL Amazon S3] Ziel. Detaillierte Anweisungen zur erforderlichen Eingabe finden Sie auf jeder Zieldokumentationsseite (siehe beispielsweise den Abschnitt zur Authentifizierung für [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) und [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]erforderliche und optionale Authentifizierungsparameter**

![Bild mit den erforderlichen und optionalen Eingabeparametern bei der Authentifizierung für ein Amazon S3-Ziel.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Verbindungsparameter einrichten {#set-up-connection-parameters}

Wenn Sie die Authentifizierung für das Ziel bereits eingerichtet haben, können Sie mit dem vorhandenen Konto fortfahren oder ein neues Konto einrichten.

Je nach Ziel, mit dem Sie eine Verbindung herstellen, werden Sie möglicherweise aufgefordert, verschiedene Typen von Verbindungsparametern einzugeben. Wenn Sie beispielsweise eine Verbindung zu einem [!DNL Amazon S3] Ziel, werden Sie aufgefordert, Details zum [!DNL Amazon S3] Behältername und Ordnerpfad, in dem Dateien abgelegt werden. Nachfolgend finden Sie zwei Beispiele für erforderliche Eingaben für eine [!DNL Amazon S3] Ziel und [!DNL Trade Desk] Ziel. Detaillierte Anweisungen zur erforderlichen Eingabe finden Sie auf jeder Zieldokumentationsseite.

>[!IMPORTANT]
>
>Die unten stehenden Bilder dienen nur zu Veranschaulichungszwecken. Die Details der Zielverbindung variieren je nach Ziel. Detaillierte Informationen zu den Verbindungsdetails für Ihr Ziel finden Sie im Abschnitt **Mit Ziel verbinden** in jedem [Zielkatalog](../catalog/overview.md) Seite (z. B. [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)oder [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]erforderliche und optionale Eingabeparameter**

![Bild, das die erforderlichen und optionalen Eingabeparameter beim Herstellen einer Verbindung zu einem Amazon S3-Ziel anzeigt.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]erforderliche und optionale Eingabeparameter**

![Bild, das die erforderlichen und optionalen Eingabeparameter beim Herstellen einer Verbindung zu einem Trade Desk-Ziel anzeigt.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Dateiformatierungsoptionen für exportierte Dateien einrichten {#file-formatting-and-compression-options}

Bei dateibasierten Zielen können Sie verschiedene Einstellungen für die Formatierung und Komprimierung der exportierten Dateien konfigurieren. Weitere Informationen zu allen verfügbaren Formatierungs- und Komprimierungsoptionen finden Sie im Abschnitt [Tutorial zum Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Bild mit Auswahl des Dateityps und verschiedenen Optionen für CSV-Dateien.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Einrichten der Zielverbindung für die Segmentaktivierung oder für Datensatzexporte {#segment-activation-or-dataset-exports}

Einige dateibasierte Ziele unterstützen die Segmentaktivierung sowie den Export von Datensätzen. Für diese Ziele können Sie auswählen, ob eine Verbindung erstellt werden soll, über die Sie Segmente aktivieren oder Datensätze exportieren können.

![Bild, das das Auswahlsteuerelement für Datentypen anzeigt und Benutzern die Auswahl zwischen Segmentaktivierung und Datensatzexporten ermöglicht.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Zielwarnungen aktivieren {#enable-alerts}

1. (Optional) Wählen Sie die Ziel-Datenfluss-Warnhinweise aus, die Sie abonnieren möchten. Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Die verfügbaren Warnhinweise unterscheiden sich je nach Zieltyp (dateibasiertes oder Streaming), mit dem Sie eine Verbindung herstellen. Lesen [In-Context-Zielwarnungen abonnieren](alerts.md) für detaillierte Informationen zu Ziel-Datenfluss-Warnhinweisen.

   ![Im Dialogfeld Neues Ziel konfigurieren werden die Abonnementoptionen für kontextbezogene Zielwarnungen hervorgehoben.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Wählen Sie **[!UICONTROL Weiter]** aus.

   ![Das Dialogfeld Neues Ziel konfigurieren mit hervorgehobenem Steuerelement Nächste konfigurieren ermöglicht es dem Benutzer, mit dem nächsten Schritt im Workflow fortzufahren.](../assets/ui/connect-destinations/next.png)

## Marketingaktionen auswählen {#select-marketing-actions}

1. Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) Seite.

   ![Im Dialogfeld Neues Ziel konfigurieren werden die verfügbaren Marketing-Aktionen hervorgehoben. Die verfügbaren Steuerelemente zum Abschließen des Workflows Mit Ziel verbinden werden ebenfalls hervorgehoben.](../assets/ui/connect-destinations/governance.png)

2. Auswählen **[!UICONTROL Speichern und beenden]** , um die Zielkonfiguration zu speichern, oder wählen Sie **[!UICONTROL Nächste]** um mit den Zielgruppendaten fortzufahren [Aktivierungsfluss](activation-overview.md).

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der Experience Platform-Benutzeroberfläche eine Verbindung zu einem Ziel herstellen können. Zur Erinnerung: Die verfügbaren und erforderlichen Verbindungsparameter variieren von Ziel zu Ziel. Sie sollten auch die Zieldokumentationsseite im Abschnitt [Zielkatalog](/help/destinations/catalog/overview.md) für spezifische Informationen zu den erforderlichen Eingaben und verfügbaren Optionen pro Zieltyp.

Als Nächstes können Sie mit [Aktivieren von Segmenten](/help/destinations/ui/activation-overview.md) oder [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md) zu Ihrem Ziel hinzu.