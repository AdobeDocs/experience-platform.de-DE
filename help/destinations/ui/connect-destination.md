---
title: Erstellen einer neuen Zielverbindung
type: Tutorial
description: Erfahren Sie, wie Sie in Adobe Experience Platform eine Verbindung mit einem Ziel herstellen, Warnhinweise aktivieren und Marketing-Aktionen für Ihr verbundenes Ziel einrichten.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: ec6f055de02610e23f30051c4fed4f362e9fbc53
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 64%

---

# Erstellen einer neuen Zielverbindung

>[!IMPORTANT]
> 
>* Um eine Verbindung mit einem Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um eine Verbindung mit einem Ziel herzustellen, das Datensatzexporte unterstützt, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage and Activate Dataset Destinations]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Übersicht {#overview}

Bevor Sie Zielgruppendaten an ein Ziel senden können, müssen Sie eine Verbindung mit Ihrer Zielplattform einrichten. In diesem Artikel erfahren Sie, wie Sie eine neue Zielverbindung einrichten, für die Sie dann Zielgruppen aktivieren oder Datensätze über die Benutzeroberfläche von Adobe Experience Platform exportieren können.

## Suchen des gewünschten Ziels im Katalog {#setup}

1. Wechseln Sie zu **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** und wählen Sie die Registerkarte **[!UICONTROL Catalog]** aus.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit der Zielkatalogseite.](../assets/ui/connect-destinations/catalog.png)

2. Zielkarten im Katalog verfügen möglicherweise über verschiedene Aktionssteuerelemente, je nachdem, ob Sie über eine bestehende Verbindung mit dem Ziel verfügen und ob die Ziele das Aktivieren von Zielgruppen, den Export von Datensätzen oder beides unterstützen. Möglicherweise werden die folgenden Steuerelemente für Zielkarten angezeigt:

   * **[!UICONTROL Set up]**. Bevor Sie Zielgruppen aktivieren oder Datensätze exportieren können, muss zunächst eine Verbindung zu diesem Ziel eingerichtet werden.
   * **[!UICONTROL Activate]**. Für dieses Ziel wurde bereits eine Verbindung eingerichtet. Dieses Ziel unterstützt die Zielgruppenaktivierung und den Export von Datensätzen.
   * **[!UICONTROL Activate audiences]**. Für dieses Ziel wurde bereits eine Verbindung eingerichtet. Dieses Ziel unterstützt nur die Zielgruppenaktivierung.

   Weitere Informationen zum Unterschied zwischen diesen Steuerelementen finden Sie auch im Abschnitt [Katalog](../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

   Wählen Sie entweder **[!UICONTROL Set up]**, **[!UICONTROL Activate]** oder **[!UICONTROL Activate audiences]** aus, je nachdem, welches Steuerelement Ihnen zur Verfügung steht.

   ![Screenshot der Experience Platform-Benutzeroberfläche, auf der die Zielkatalogseite mit dem hervorgehobenen Steuerelement „Einrichten“ dargestellt ist.](../assets/ui/connect-destinations/set-up.png)

   ![Screenshot der Experience Platform-Benutzeroberfläche, auf der die Zielkatalogseite mit dem hervorgehobenen Steuerelement „Zielgruppen aktivieren“ dargestellt ist.](../assets/ui/connect-destinations/activate-segments.png)

3. Wenn Sie **[!UICONTROL Set up]** ausgewählt haben, springen Sie zum nächsten Schritt, um [Authentifizieren](#authenticate) zum Ziel zu gelangen.

   Wenn Sie **[!UICONTROL Activate]**, **[!UICONTROL Activate audiences]** oder **[!UICONTROL Export datasets]** ausgewählt haben, können Sie jetzt eine Liste der vorhandenen Zielverbindungen sehen.

   Wählen Sie **[!UICONTROL Configure new destination]** aus, um eine neue Verbindung mit dem Ziel herzustellen.

   ![Screenshot der Experience Platform-Benutzeroberfläche, auf der eine Liste der verfügbaren Ziele und das hervorgehobene Steuerelement „Neues Ziel konfigurieren“ dargestellt sind.](../assets/ui/connect-destinations/configure-new-destination.png)

## Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_account_name"
>title="Kontoname"
>abstract="Geben Sie einen Namen ein, der Ihnen hilft, dieses Zielkonto in Zukunft leicht zu identifizieren. Dies ist besonders nützlich, wenn Sie mehrere Verbindungen mit demselben Ziel haben."

Der erste Schritt beim Herstellen einer Verbindung mit einem Ziel besteht darin, sich bei der Zielplattform zu authentifizieren.

Je nach Ziel, mit dem Sie eine Verbindung herstellen, gelangen Sie möglicherweise zur Seite des Zielpartners, um sich zu authentifizieren. Möglicherweise werden Sie aber auch direkt im Experience Platform-Workflow aufgefordert, Anmeldeinformationen zur Authentifizierung einzugeben.

Beim Einrichten einer neuen Zielverbindung müssen Sie eine **[!UICONTROL Account name]** und optional eine **[!UICONTROL Description]** angeben. Diese Felder sind für alle Ziele verfügbar.

* **[!UICONTROL Account name]**: Geben Sie einen Namen ein, der Ihnen hilft, dieses Zielkonto in Zukunft einfach zu identifizieren. Dies ist besonders nützlich, wenn Sie mehrere Verbindungen mit demselben Ziel haben.
* **[!UICONTROL Description]** (optional): Fügen Sie zusätzliche Details hinzu, die Ihnen oder Ihrem Team helfen, zwischen Konten zu unterscheiden, z. B. den Zweck der Verbindung oder den relevanten Geschäftskontext.

Wenn Sie klare und beschreibende Informationen in diesen Feldern bereitstellen, können Sie beim Aktivieren von Zielgruppen das richtige Zielkonto leichter verwalten und auswählen.

Nachfolgend finden Sie ein Beispiel für die erforderliche Eingabe zur Authentifizierung bei einem [!DNL Amazon S3]-Ziel. Detaillierte Anweisungen zur erforderlichen Eingabe finden Sie auf jeder Zieldokumentationsseite (lesen Sie beispielsweise den Abschnitt zur Authentifizierung für [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) und für [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

Für **[!DNL Amazon S3]erforderliche und optionale Authentifizierungsparameter**

![Abbildung mit den erforderlichen und optionalen Eingabeparametern bei der Authentifizierung für ein Amazon S3-Ziel.](../assets/ui/connect-destinations/s3-new-acc.png)

## Einrichten von Verbindungsparametern {#set-up-connection-parameters}

Wenn Sie die Authentifizierung für das Ziel bereits eingerichtet haben, können Sie mit dem vorhandenen Konto fortfahren oder ein neues Konto einrichten.

Je nach Ziel, mit dem Sie eine Verbindung herstellen, werden Sie möglicherweise aufgefordert, unterschiedliche Typen von Verbindungsparametern einzugeben. Wenn Sie beispielsweise eine Verbindung mit einem [!DNL Amazon S3]-Ziel herstellen, werden Sie aufgefordert, Details zum [!DNL Amazon S3]-Behälternamen und -Ordnerpfad anzugeben, in dem Dateien abgelegt werden. Nachfolgend finden Sie zwei Beispiele für erforderliche Eingaben für ein [!DNL Amazon S3]-Ziel und ein [!DNL Trade Desk]-Ziel. Detaillierte Anweisungen zur erforderlichen Eingabe finden Sie auf jeder Zieldokumentationsseite.

>[!IMPORTANT]
>
>Die folgenden Bilder dienen nur zur Veranschaulichung. Die Details der Zielverbindung variieren je nach Ziel. Detaillierte Informationen zu den Verbindungsdetails für Ihr Ziel finden Sie im Abschnitt **Verbinden mit dem Ziel** auf jeder Seite [Zielkatalog](../catalog/overview.md) (z. B. [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect) oder [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

Für **[!DNL Amazon S3]erforderliche und optionale Eingabeparameter**

![Bild, das die erforderlichen und optionalen Eingabeparameter beim Herstellen einer Verbindung mit einem Amazon S3-Ziel zeigt.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

Für **[!DNL The Trade Desk]erforderliche und optionale Eingabeparameter**

![Bild, das die erforderlichen und optionalen Eingabeparameter beim Herstellen einer Verbindung mit einem Trade Desk-Ziel zeigt.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Einrichten von Dateiformatierungsoptionen für exportierte Dateien {#file-formatting-and-compression-options}

Für dateibasierte Ziele können Sie verschiedene Einstellungen für die Formatierung und Komprimierung der exportierten Dateien konfigurieren. Weitere Informationen zu allen verfügbaren Formatierungs- und Komprimierungsoptionen finden Sie im [Tutorial zum Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Bild, das die Auswahl des Dateityps und verschiedene Optionen für CSV-Dateien zeigt.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Einrichten der Zielverbindung für Zielgruppenaktivierung, Kontoaktivierung, Interessentenaktivierung oder Datensatzexporte {#segment-activation-or-dataset-exports}

Einige dateibasierte Ziele unterstützen die Zielgruppenaktivierung für bekannte Kundinnen und Kunden, Account-Kundinnen und -Kunden oder Interessenten sowie den Export von Datensätzen. Für diese Ziele können Sie auswählen, ob eine Verbindung erstellt werden soll, mit der Sie [Zielgruppen aktivieren](/help/destinations/ui/activate-batch-profile-destinations.md), [Konten](/help/destinations/ui/activate-account-audiences.md), [Interessenten](/help/destinations/ui/activate-prospect-audiences.md) oder [&#x200B; Datensätze exportieren](/help/destinations/ui/export-datasets.md).

>[!WARNING]
>
>Beachten Sie beim Exportieren von Datensätzen, dass Exporte in JSON-Dateien nur in einem komprimierten Modus unterstützt werden. Exporte in [!DNL Parquet]-Dateien werden im komprimierten und unkomprimierten Modus unterstützt.

![Abbildung der Datentypauswahl-Steuerung, mit der Benutzende zwischen Zielgruppenaktivierung und Datensatzexporten wählen können.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Aktivieren von Ziel-Warnhinweisen {#enable-alerts}

1. (Optional) Wählen Sie die Ziel-Datenfluss-Warnhinweise aus, die Sie abonnieren möchten. Sie können jetzt beim Erstellen eines Ziel-Datenflusses Warnhinweise abonnieren, um Benachrichtigungen zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Die verfügbaren Warnhinweise unterscheiden sich je nach Zieltyp (dateibasiert oder Streaming), mit dem Sie eine Verbindung herstellen. Lesen Sie [Kontextabhängige Ziel-Warnhinweise abonnieren](alerts.md), um detaillierte Informationen zu Ziel-Datenfluss-Warnhinweisen zu erhalten.

   ![Das Dialogfeld „Neues Ziel konfigurieren“ mit hervorgehobenen Abonnementoptionen für kontextabhängige Ziel-Warnhinweise.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Wählen Sie **[!UICONTROL Next]** aus.

   ![Das Dialogfeld „Neues Ziel konfigurieren“ mit hervorgehobener Option „Nächstes Steuerelement“, mit der der Benutzer zum nächsten Schritt im Workflow fortfahren kann.](../assets/ui/connect-destinations/next.png)

## Auswählen von Marketing-Aktionen {#select-marketing-actions}

1. Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Marketing-Aktionen geben an, mit welcher Absicht Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Datennutzungsrichtlinien – Übersicht](../../data-governance/policies/overview.md).

   ![Das Dialogfeld „Neues Ziel konfigurieren“ mit Hervorhebung der verfügbaren Marketing-Aktionen. Die verfügbaren Steuerelemente zum Abschließen des Workflows „Mit Ziel verbinden“ sind ebenfalls hervorgehoben.](../assets/ui/connect-destinations/governance.png)

2. Wählen Sie **[!UICONTROL Save & Exit]** aus, um die Zielkonfiguration zu speichern, oder wählen Sie **[!UICONTROL Next]** aus, um mit den Zielgruppendaten [Aktivierungsfluss) &#x200B;](activation-overview.md).

## Nächste Schritte {#next-steps}

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der Experience Platform-Benutzeroberfläche eine Verbindung zu einem Ziel herstellen können. Zur Erinnerung: Die verfügbaren und erforderlichen Verbindungsparameter variieren von Ziel zu Ziel. Sie sollten auch die Seite zur Zieldokumentation im [Zielkatalog](/help/destinations/catalog/overview.md) konsultieren, um spezifische Informationen zu den erforderlichen Eingaben und verfügbaren Optionen pro Zieltyp zu erhalten.

Als Nächstes können Sie mit dem [Aktivieren von Zielgruppen](/help/destinations/ui/activation-overview.md) oder [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md) zu Ihrem Ziel fortfahren.