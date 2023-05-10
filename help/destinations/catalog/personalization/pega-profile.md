---
title: Pega Profile Connector
description: Verwenden Sie den Pega Profile Connector für Amazon S3 in Adobe Experience Platform, um vollständige oder inkrementelle Profildaten oder beides in den Amazon S3-Cloud-Speicher zu exportieren. In Pega Customer Decisioning Hub können Datenaufträge in Customer Profile Designer so geplant werden, dass Profildaten regelmäßig aus dem Amazon S3-Speicher importiert werden.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 52%

---

# Pega Profile Connector

## Übersicht {#overview}

Verwenden Sie die [!DNL Pega Profile Connector] in Adobe Experience Platform , um eine ausgehende Live-Verbindung zu Ihrer [!DNL Amazon Web Services] (AWS) S3-Datenspeicherung , um Profildaten regelmäßig in CSV-Dateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren. In [!DNL Pega Customer Decision Hub] können Sie Datenaufträge planen, um diese Profildaten aus dem S3-Speicher zur Aktualisierung des [!DNL Pega Customer Decision Hub]-Profils importieren.

Dieser Connector hilft beim Einrichten des anfänglichen Exports von Profildaten und hilft auch, neue Profile regelmäßig in zu synchronisieren [!DNL Pega Customer Decision Hub].  Die Verwendung aktueller Daten in Customer Decisioning Hub bietet eine bessere und aktualisierte Ansicht Ihrer Kundenbasis für die Entscheidungsfindung für die nächsten Schritte.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von Pegasystems erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Pega [here](mailto:support@pega.com).

## Anwendungsfälle

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Pega Profile Connector]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall 1

Ein Marketing-Experte möchte zunächst [!DNL Pega Customer Decision Hub] mit Profildaten, die aus Adobe Experience Platform geladen wurden. Hierbei handelt es sich um eine anfängliche Volllast, der Delta-Ladevorgänge auf geplanter Basis folgen.

### Anwendungsfall 2

Ein Marketing-Experte möchte aktuelle Profildaten aus Adobe Experience Platform in [!DNL Pega Customer Decision Hub] das die Pega-Einblicke um Kundenprofile kontinuierlich verbessert.

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Ziel verwenden können, um Daten aus Adobe Experience Platform zu exportieren und Profile in [!DNL Pega Customer Decision Hub]müssen Sie die folgenden Voraussetzungen erfüllen:

* Konfigurieren [!DNL Amazon S3] und den Ordnerpfad, der für den Export und Import von Datendateien verwendet werden soll.
* Konfigurieren Sie die [!DNL Amazon S3] Zugriffsschlüssel und [!DNL Amazon S3] geheimer Schlüssel: In [!DNL Amazon S3], generieren Sie eine `access key - secret access key` , um Platform Zugriff auf Ihre [!DNL Amazon S3] -Konto.
* So verbinden Sie Daten erfolgreich mit Ihren [!DNL Amazon S3] Speicherort speichern, erstellen Sie einen Benutzer für Identity and Access Management (IAM) für [!DNL Platform] in [!DNL Amazon S3] und Berechtigungen zuweisen, z. B. `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Stellen Sie sicher, dass [!DNL Pega Customer Decision Hub] -Instanz auf Version 8.8 oder höher aktualisiert.

## Unterstützte Identitäten {#supported-identities}

[!DNL Pega Customer Decision Hub] unterstützt die Aktivierung von benutzerdefinierten Benutzer-IDs, die in der folgenden Tabelle beschrieben sind. Weitere Informationen finden Sie unter [identities](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| *CustomerID* | Allgemeine Benutzer-ID, die ein Profil eindeutig in [!DNL Pega Customer Decision Hub] und Adobe Experience Platform |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!DNL Amazon S3]Zugriffsschlüssel** und **[!DNL Amazon S3]geheimer Schlüssel**: In [!DNL Amazon S3], generieren Sie eine `access key - secret access key` , um Adobe Experience Platform Zugriff auf Ihre [!DNL Amazon S3] -Konto. Weitere Informationen finden Sie in der [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Ausfüllen der Zieldetails {#destination-details}

Nach der Herstellung der Authentifizierungsverbindung zu [!DNL Amazon S3]Geben Sie die folgenden Informationen für das Ziel an:

![Bild des UI-Bildschirms mit ausgefüllten Feldern für die Zieldetails des Pega Profile Connector-Ziels](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Nächste]**. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Behältername]**: Geben Sie den Namen des [!DNL Amazon S3]-Behälters ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Komprimierungstyp]**: Wählen Sie als Komprimierungstyp GZIP oder KEINE aus.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie einen benutzerdefinierten Ordner in Ihrem Amazon S3-Speicher pro exportierter Segmentdatei erstellen. Anweisungen finden Sie unter [Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort](/help/destinations/catalog/cloud-storage/overview.md#use-macros).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen des Datenexports {#exported-data}

Für [!DNL Pega Profile Connector] Ziele, [!DNL Platform] erstellt eine `.csv` -Datei im Speicherort von Amazon S3, den Sie bereitgestellt haben. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.

Bei einem erfolgreichen Import von Profildaten aus S3 werden Daten in die [!DNL Pega Customer] Profil-Datenspeicher. Die importierten Kundenprofildaten können in [!DNL Pega Customer Profile Designer] , wie in der folgenden Abbildung dargestellt.
![Bild des UI-Bildschirms, auf dem Sie die Profildaten der Adobe in Customer Profile Designer überprüfen können](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

In [!DNL Pega Customer Decision Hub], können Datenadministratoren Datenaufträge in konfigurieren. [!DNL Customer Profile Designer] um Profildaten regelmäßig aus S3 zu importieren, wie in der folgenden Abbildung dargestellt. Siehe [Zusätzliche Ressourcen](#additional-resources) Weitere Informationen zum Konfigurieren von Datenaufträgen für den Import von Profildaten aus [!DNL Amazon S3].
![Bild des UI-Bildschirms zum Konfigurieren von Datenaufträgen in Customer Profile Designer](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Zusätzliche Ressourcen {#additional-resources}

Siehe [Importieren von Datenaufträgen](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
