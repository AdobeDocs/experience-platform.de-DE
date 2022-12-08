---
title: Data Landing Zone Ziel
description: Erfahren Sie, wie Sie eine Verbindung zur Data Landing Zone herstellen, um Segmente zu aktivieren und Datensätze zu exportieren.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 25%

---

# (Beta) Data Landing Zone Ziel

>[!IMPORTANT]
>
>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. Um Zugang zur [!DNL Data Landing Zone]-Verbindung zu erhalten, wenden Sie sich an Ihre Kontaktperson beim Adobe-Support und geben Sie Ihre [!DNL Organization ID] an.


## Übersicht {#overview}

[!DNL Data Landing Zone] ist [!DNL Azure Blob] von Adobe Experience Platform bereitgestellte Speicherschnittstelle, über die Sie Zugriff auf eine sichere, Cloud-basierte Dateispeicheranlage erhalten, über die Dateien aus Platform exportiert werden können. Sie haben Zugriff auf eine [!DNL Data Landing Zone] Behälter pro Sandbox und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Platform-Produkte- und -Services-Lizenz bereitgestellt werden. Alle Kunden von Platform und die zugehörigen Anwendungsdienste wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]und [!DNL Real-time Customer Data Platform] mit einem [!DNL Data Landing Zone] Container pro Sandbox. Sie können Dateien in Ihren Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder der Befehlszeilenschnittstelle.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung und die Daten sind durch Standard geschützt [!DNL Azure Blob] Sicherheitsmechanismen für die Lagerung im Ruhezustand und im Transit. Mit der SAS-basierten Authentifizierung können Sie sicher auf Ihre [!DNL Data Landing Zone] Container über eine öffentliche Internetverbindung. Es sind keine Netzwerkänderungen erforderlich, damit Sie auf Ihre [!DNL Data Landing Zone] -Container verwenden, müssen Sie also keine Zulassungslisten oder regionenübergreifenden Setups für Ihr Netzwerk konfigurieren.

Platform erzwingt für alle Dateien, die in eine [!DNL Data Landing Zone] Container. Alle Dateien werden nach sieben Tagen gelöscht.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den entsprechenden Schemafeldern (z. B. Ihre PPID), wie im Bildschirm Profilattribute auswählen der [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Verwalten des Inhalts Ihrer [!DNL Data Landing Zone]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) die Inhalte Ihrer [!DNL Data Landing Zone] Container.

Im [!DNL Azure Storage Explorer] Wählen Sie in der linken Navigationsleiste das Verbindungssymbol aus. Die **Ressource auswählen** -Fenster angezeigt, mit dem Sie eine Verbindung herstellen können. Auswählen **[!DNL Blob container]** um eine Verbindung zu Ihrer [!DNL Data Landing Zone] Speicher.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und wählen Sie dann **Nächste**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nach Auswahl der Verbindungsmethode müssen Sie eine **Anzeigename** und **[!DNL Blob]Container-SAS-URL** , die Ihrer [!DNL Data Landing Zone] Container.

>[!IMPORTANT]
>
>Sie müssen die Platform-APIs verwenden, um Ihre Data Landing Zone-Anmeldedaten abzurufen. Vollständige Informationen finden Sie unter [Einstiegszonen-Anmeldeinformationen für Daten abrufen](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> Um die Anmeldeinformationen abzurufen und auf die exportierten Dateien zuzugreifen, müssen Sie den Abfrageparameter ersetzen `type=user_drop_zone` mit `type=dlz_destination` in allen HTTP-Aufrufen, die auf der obigen Seite beschrieben sind.

Geben Sie Ihre [!DNL Data Landing Zone] SAS-URL und dann **Nächste**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Die **Zusammenfassung** -Fenster angezeigt, das Ihnen einen Überblick über Ihre Einstellungen einschließlich Informationen zu Ihrer [!DNL Blob] -Endpunkt und Berechtigungen. Wenn Sie bereit sind, wählen Sie **Verbinden**.

![summary](/help/sources/images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre [!DNL Azure Storage Explorer] Benutzeroberfläche mit [!DNL Data Landing Zone] Container.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Mit [!DNL Data Landing Zone] Container, der mit [!DNL Azure Storage Explorer]können Sie jetzt mit dem Export von Dateien aus Experience Platform in Ihre [!DNL Data Landing Zone] Container. Um Dateien zu exportieren, müssen Sie eine Verbindung zum [!DNL Data Landing Zone] Ziel in der Experience Platform-Benutzeroberfläche, wie im folgenden Abschnitt beschrieben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

weil [!DNL Data Landing Zone] ist ein von der Adobe bereitgestellter Speicher. Sie müssen keine Schritte ausführen, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.
* **[!UICONTROL Dateityp]**: Wählen Sie die Format-Experience Platform aus, die für die exportierten Dateien verwendet werden soll. Bei der Auswahl der [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den die Experience Platform für die exportierten Dateien verwenden soll.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zeitplan

Im **[!UICONTROL Planung]** Schritt, können Sie [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) für Ihre [!DNL Data Landing Zone] Ziel und Sie können auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Zuordnung]** auswählen, können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch auswählen, ob die Header in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden sollen. Weitere Informationen finden Sie unter [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Aktivierung der Batch-Ziele-Benutzeroberfläche .

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Umfassende Informationen zum Einrichten von Datensatzexporten finden Sie in der [Tutorial zum Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Validieren eines erfolgreichen Datenexports {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihre [!DNL Data Landing Zone] speichern und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
