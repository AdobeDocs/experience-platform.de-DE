---
title: Übersicht über Google PubSub Source
description: Erfahren Sie, wie Sie Google PubSub über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: c8fc447631f5382d49022b525a10edeadbd5ab46
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 19%

---

# [!DNL Google PubSub]

>[!IMPORTANT]
>
>Die [!DNL Google PubSub] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie [!DNL AWS], [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Daten aus diesen Systemen zur Verwendung in nachgelagerten Services und Zielen in Platform importieren können.

Cloud-Speicher sind eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Platform können Sie Daten aus [!DNL Google PubSub] in Echtzeit importieren.

## Voraussetzungen {#prerequisites}

In diesem Abschnitt wird die erforderliche Einrichtung beschrieben, die Sie durchführen müssen, bevor Sie Ihr [!DNL Google PubSub]-Konto mit Experience Platform verbinden.

### Service-Konto erstellen {#create-service-account}

Ein **Dienstkonto** ist ein Kontotyp, der häufig von einer Anwendung oder einem Compute-Workload und nicht von einer Person verwendet wird. Ein Service-Konto wird anhand seiner E-Mail-Adresse identifiziert, die eindeutig für das Konto ist.

* Einerseits sind Dienstkonten **Prinzipale** - Sie können Dienstkonten Zugriff auf [!DNL Google Cloud] Ressourcen gewähren. Beispielsweise können Sie einem Dienstkonto die für ein bestimmtes Projekt `(roles/compute.admin)` Compute-Administratorrolle gewähren. Auf diese Weise kann das Service-Konto Compute-Engine-Ressourcen in diesem bestimmten Projekt verwalten.
* Auf der anderen Seite sind Dienstkonten auch Ressourcen - Sie können anderen Prinzipalen die Berechtigung zum Zugriff auf das Dienstkonto erteilen. Sie können beispielsweise einem Benutzer die Rolle Dienstkonto-Benutzer `(roles/iam.serviceAccountUser)` auf einem Dienstkonto gewähren, damit der Benutzer dieses Dienstkonto mit Ressourcen verknüpfen kann. Alternativ können Sie einem Benutzer die `(roles/iam.serviceAccountAdmin)` „Dienstkonto-Administrator“ gewähren, damit er Aufgaben wie das Anzeigen, Bearbeiten, Deaktivieren und Löschen des Dienstkontos ausführen kann.

Weitere Informationen zur Bestimmung des richtigen Authentifizierungstyps für Ihren Anwendungsfall finden Sie im [[!DNL Google] Handbuch zu Authentifizierungsmethoden](https://cloud.google.com/docs/authentication).

Gehen Sie wie folgt vor, um ein Service-Konto zu erstellen:

Navigieren Sie zunächst zur [!DNL IAM] Seite der [!DNL Google Developer Console] und wählen Sie dann **[!DNL Create Service Account]** aus.

![Das Fenster „Service-Konto erstellen“ in Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Geben Sie als Nächstes einen Anzeigenamen und eine ID für Ihr Service-Konto ein und wählen Sie dann **[!DNL Create and Continue]** aus.

![Die Details des Service-Kontos in der Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Generieren von Service-Kontoschlüsseln {#generate-service-account-keys}

Um Schlüssel für Ihr Service-Konto zu generieren, wählen Sie die Kopfzeile Schlüssel auf der Seite Service-Konten . Wählen Sie dort **[!DNL Add key]** und dann **[!DNL Create new key]** aus dem Dropdown-Menü aus. Sie können dieses Bedienfeld auch verwenden, um einen vorhandenen Schlüssel hochzuladen.

![Das Fenster Schlüssel hinzufügen in der Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

Bei erfolgreicher Ausführung erhalten Sie eine Meldung, die angibt, dass der private Schlüssel auf Ihrem Computer gespeichert wurde und eine Datei heruntergeladen wird. Sie können dann den Inhalt dieser Datei als Anmeldeinformationen verwenden, wenn Sie Ihr [!DNL Google PubSub]-Konto auf Experience Platform erstellen.

### Berechtigungen auf Themen- und Abonnementebene erteilen {#grant-permissions}

Um Berechtigungen auf der Themen- und Abonnementebene zu gewähren, navigieren Sie zur Seite „Themenkonsole“ und wählen Sie dann **[!DNL Show info panel]** aus. Wählen Sie anschließend auf der Registerkarte [!DNL Permissions] die Option [!DNL Add Principal] aus und fügen Sie den Service-Kontoprinzipal zusammen mit den Berechtigungen hinzu.

![Das Popup-Fenster in der Google Developer Console, in dem Sie Berechtigungen auf Themen- und Abonnementebene gewähren können](../../images/tutorials/create/google-pubsub/add-principal.png)

## Konfigurationen für optimale [!DNL Google PubSub usage] {#optimal-configurations}

In diesem Abschnitt werden Konfigurationen beschrieben, die Sie vornehmen sollten, um die Verwendung der [!DNL Google PubSub] auf Experience Platform zu optimieren.

### Abonnementeigenschaften {#subscription-properties}

Verwenden Sie die [!DNL Google Developer Console] , um **die Frist für die Bestätigung zu verlängern**. Dadurch kann der [!DNL Google Publisher] entsprechend der konfigurierten Zeit warten, bevor die Nachricht erneut gesendet wird. Diese Verzögerung trägt dazu bei, unnötige Belastungen auf Teilnehmerebene zu reduzieren.

![Die Benutzeroberfläche zum Bestätigungs-Deadline in Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

**[!DNL exactly one delivery]** aktivieren. Diese Konfiguration informiert die [!DNL Google Publisher], um sicherzustellen, dass an das Abonnement gesendete Nachrichten nicht vor Ablauf der Bestätigungsfrist erneut gesendet werden. Mit dieser Einstellung können Sie sicherstellen, dass Bestätigungsnachrichten nicht erneut an das Abonnement gesendet werden.

![Die genau eine Versandkonfigurationsseite in der Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Sie können **[!DNL Retry after exponential backoff delay]** aktivieren, um das Risiko einer weiteren Überlastung des Servers zu reduzieren. Sie können diese Konfiguration in der [!DNL Google Developer Console] aktivieren, um vorübergehende Fehler (temporäre Fehler, die sich normalerweise selbst beheben) besser zu reduzieren, indem Sie dem System mehr Zeit zum Wiederherstellen geben, bevor Sie eine andere Verbindung versuchen.

![Das Fenster „Richtlinie erneut versuchen“ in Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Sie müssen **die Aufbewahrungsdauer Ihrer Abonnementnachricht auf 24 Stunden oder mehr festlegen** um sicherzustellen, dass nicht quittierte Daten bei Spitzenbelastungen nicht verloren gehen. Zusätzlich sollten Sie **Dead-Letter-Thema aktivieren** um sicherzustellen, dass auch in seltenen Randfällen kein Datenverlust auftritt.

>[!IMPORTANT]
>
>Pro [!DNL Google PubSub]-Abonnement kann nur ein Quelldatenfluss erstellt werden. Die Wiederverwendung eines Abonnements führt selbst über Sandboxes hinweg zu Datenverlust.

## [!DNL Google PubSub] mit Experience Platform verbinden

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google PubSub] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

* [Erstellen einer Google PubSub-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer Quellverbindung für Google PubSub über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
