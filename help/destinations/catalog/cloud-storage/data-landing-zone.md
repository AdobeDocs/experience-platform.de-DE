---
title: Ziel der Data Landing Zone
description: Erfahren Sie, wie Sie eine Verbindung zur Data Landing Zone herstellen, um Segmente zu aktivieren und Datensätze zu exportieren.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 95%

---

# (Beta) Ziel der Data Landing Zone

>[!IMPORTANT]
>
>Diese Funktion befindet sich derzeit in der Beta-Phase und steht nur einer bestimmten Anzahl von Kunden zur Verfügung. Um Zugang zur [!DNL Data Landing Zone]-Verbindung zu erhalten, wenden Sie sich an Ihre Kontaktperson beim Adobe-Support-Mitarbeiter und geben Sie Ihre [!DNL Organization ID] an.


## Übersicht {#overview}

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Platform zu exportieren. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Produkt- und Services-Lizenz von Platform bereitgestellt werden. Alle Kundinnen und Kunden von Platform sowie die zugehörigen Anwendungs-Services wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Real-Time Customer Data Platform] erhalten einen [!DNL Data Landing Zone]-Container pro Sandbox. Sie können Dateien in Ihrem Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder die Befehlszeilenschnittstelle verwenden.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Für die Verwendung Ihres [!DNL Data Landing Zone]-Containers sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren.

Platform erzwingt eine strikte sieben Tage lange Lebensdauer („time-to-live“, TTL) für alle Dateien, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden. Alle Dateien werden nach sieben Tagen gelöscht.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Teile eines Segments zusammen mit den entsprechenden Schemafeldern (wie etwa Ihre PPID), gemäß der Auswahl im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Verwalten des Inhalts Ihrer [!DNL Data Landing Zone]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/de-de/features/storage-explorer/) verwenden, um die Inhalte Ihres [!DNL Data Landing Zone]-Containers zu verwalten.

Wählen Sie in der Benutzeroberfläche von [!DNL Azure Storage Explorer] in der linken Navigationsleiste das Verbindungssymbol aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu Ihrem [!DNL Data Landing Zone]-Speicher herzustellen.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nachdem Sie Ihre Verbindungsmethode ausgewählt haben, müssen Sie einen **Anzeigenamen** und die **[!DNL Blob]Container-SAS-URL** angeben, die mit Ihrem [!DNL Data Landing Zone]-Container übereinstimmt.

>[!IMPORTANT]
>
>Sie müssen die Platform-APIs verwenden, um Ihre Anmeldeinformationen für die Data Landing Zone abzurufen. Vollständige Informationen finden Sie unter [Abrufen von Anmeldeinformationen für die Data Landing Zone](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=de#retrieve-data-landing-zone-credentials).
>
> Um die Anmeldeinformationen abzurufen und auf die exportierten Dateien zuzugreifen, müssen Sie den Abfrageparameter `type=user_drop_zone` mit `type=dlz_destination` in allen HTTP-Aufrufen ersetzen, die auf der obigen Seite beschrieben sind.

Geben Sie Ihre SAS-URL für die [!DNL Data Landing Zone] an und klicken Sie dann auf **Weiter**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung](/help/sources/images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Da Ihr [!DNL Data Landing Zone]-Container jetzt mit [!DNL Azure Storage Explorer] verbunden ist, können Sie damit beginnen, Dateien von Experience Platform in Ihren [!DNL Data Landing Zone]-Container zu exportieren. Um Dateien zu exportieren, müssen Sie eine Verbindung zum [!DNL Data Landing Zone]-Ziel in der Benutzeroberfläche von Experience herstellen, wie im folgenden Abschnitt beschrieben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Da [!DNL Data Landing Zone] ein von Adobe bereitgestellter Speicher ist, müssen Sie keine Schritte ausführen, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Dateityp]**: Wählen Sie die Format-Experience Platform aus, die für die exportierten Dateien verwendet werden soll. Bei der Auswahl der [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den die Experience Platform für die exportierten Dateien verwenden soll.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

### Planung

Im Schritt **[!UICONTROL Planung]** können Sie für Ihr [!DNL Data Landing Zone]-Ziel den [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling), und Sie können dort auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Umfassende Informationen zum Einrichten von Datensatzexporten finden Sie im [Tutorial zum Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Data Landing Zone]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
