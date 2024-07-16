---
title: Google PubSub Source - Überblick
description: Erfahren Sie, wie Sie Google PubSub über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: c8fc447631f5382d49022b525a10edeadbd5ab46
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 19%

---

# [!DNL Google PubSub] source

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Google PubSub]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie [!DNL AWS], [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Daten aus diesen Systemen zur Verwendung in nachgelagerten Services und Zielen in Platform importieren können.

Cloud-Speicher sind eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Platform können Sie Daten aus [!DNL Google PubSub] in Echtzeit importieren.

## Voraussetzungen {#prerequisites}

In diesem Abschnitt werden die erforderlichen Einrichtungsschritte beschrieben, die Sie ausführen müssen, bevor Sie Ihr [!DNL Google PubSub]-Konto mit Experience Platform verbinden.

### Dienstkonto erstellen {#create-service-account}

Ein **Dienstkonto** ist ein Kontotyp, der häufig von einer Anwendung verwendet wird oder den Arbeitsaufwand berechnet, anstatt von einer Person verwendet zu werden. Ein Dienstkonto wird durch seine E-Mail-Adresse identifiziert, die für das Konto eindeutig ist.

* Zum einen sind Dienstkonten **Prinzipale** - Sie können Dienstkonten Zugriff auf [!DNL Google Cloud] -Ressourcen gewähren. Sie können beispielsweise einem Dienstkonto die Rolle &quot;Administrator berechnen&quot;`(roles/compute.admin)` für ein bestimmtes Projekt zuweisen. Dadurch kann das Dienstkonto dann die Ressourcen des Compute Engine in diesem bestimmten Projekt verwalten.
* Andererseits sind Dienstkonten auch Ressourcen. Sie können anderen Prinzipalen Zugriff auf das Dienstkonto gewähren. Sie können einem Benutzer beispielsweise die Benutzerrolle &quot;Dienstkonto-Benutzer&quot;`(roles/iam.serviceAccountUser)` für ein Dienstkonto zuweisen, damit der Benutzer dieses Dienstkonto an Ressourcen anhängen kann. Alternativ können Sie einem Benutzer die Rolle &quot;Dienstkonto-Admin&quot;`(roles/iam.serviceAccountAdmin)` zuweisen, damit der Benutzer Aufgaben wie das Anzeigen, Bearbeiten, Deaktivieren und Löschen des Dienstkontos erledigen kann.

Weitere Informationen zum Bestimmen des richtigen Authentifizierungstyps für Ihren Anwendungsfall finden Sie im [[!DNL Google] Handbuch zu Authentifizierungsmethoden](https://cloud.google.com/docs/authentication).

Gehen Sie wie folgt vor, um ein Dienstkonto zu erstellen:

Navigieren Sie zuerst zur Seite &quot;[!DNL IAM]&quot; des Felds &quot;[!DNL Google Developer Console]&quot; und wählen Sie dann &quot;**[!DNL Create Service Account]**&quot;.

![Das Fenster zum Erstellen eines Dienstkontos in der Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Geben Sie als Nächstes einen Anzeigenamen und eine ID für Ihr Dienstkonto ein und wählen Sie dann **[!DNL Create and Continue]** aus.

![Die Details des Dienstkontos in der Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Generieren von Dienstkontoschlüsseln {#generate-service-account-keys}

Um Schlüssel für Ihr Dienstkonto zu generieren, wählen Sie auf der Seite Dienstkonten die Kopfzeile Schlüssel aus. Wählen Sie dort **[!DNL Add key]** und dann **[!DNL Create new key]** aus dem Dropdown-Menü aus. Sie können dieses Bedienfeld auch verwenden, um einen vorhandenen Schlüssel hochzuladen.

![Das Fenster &quot;Schlüssel hinzufügen&quot;im Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

Bei erfolgreicher Ausführung erhalten Sie eine Nachricht, die angibt, dass der private Schlüssel auf Ihrem Computer gespeichert wurde und eine Datei heruntergeladen wird. Anschließend können Sie den Inhalt dieser Datei als Anmeldeinformationen verwenden, wenn Sie Ihr [!DNL Google PubSub]-Konto auf dem Experience Platform erstellen.

### Gewähren von Berechtigungen auf Themen- und Abonnementebene {#grant-permissions}

Um Berechtigungen auf Themen- und Abonnementebene zu erteilen, navigieren Sie zur Seite &quot;Themenkonsole&quot;und wählen Sie dann **[!DNL Show info panel]** aus. Wählen Sie anschließend auf der Registerkarte [!DNL Permissions] die Option [!DNL Add Principal] aus und fügen Sie dann den Prinzipal des Dienstkontos zusammen mit den Berechtigungen hinzu.

![Das Popup-Fenster in der Google Developer Console, in dem Sie Berechtigungen auf Themen- und Abonnementebene gewähren können](../../images/tutorials/create/google-pubsub/add-principal.png)

## Konfigurationen für optimale [!DNL Google PubSub usage] {#optimal-configurations}

In diesem Abschnitt werden die Konfigurationen beschrieben, die Sie vornehmen sollten, um die Verwendung der [!DNL Google PubSub] -Quelle auf dem Experience Platform zu optimieren.

### Abonnementeigenschaften {#subscription-properties}

Verwenden Sie die [!DNL Google Developer Console] zu **Erhöhen Sie Ihren Bestätigungszeitraum**. Dadurch kann [!DNL Google Publisher] entsprechend der von Ihnen konfigurierten Zeit warten, bevor die Nachricht erneut gesendet wird. Diese Verzögerung trägt dazu bei, unnötige Auslastung auf Abonnentenebene zu verringern.

![Die Benutzeroberfläche für die Bestätigung der Frist in der Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Aktivieren Sie **[!DNL exactly one delivery]**. Diese Konfiguration informiert die [!DNL Google Publisher] darüber, dass sichergestellt wird, dass an das Abonnement gesendete Nachrichten nicht vor Ablauf der Bestätigung erneut gesendet werden. Sie können diese Einstellung verwenden, um sicherzustellen, dass Bestätigungsnachrichten nicht an das Abonnement zurückgesendet werden.

![Die genau eine Bereitstellungskonfigurationsseite in der Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Sie können **[!DNL Retry after exponential backoff delay]** aktivieren, um das Risiko einer weiteren Überlastung des Servers zu verringern. Sie können diese Konfiguration in der [!DNL Google Developer Console] aktivieren, um vorübergehende Fehler (temporäre Fehler, die normalerweise selbst aufgelöst werden) besser zu beheben, indem Sie dem System mehr Zeit zur Wiederherstellung geben, bevor Sie eine andere Verbindung versuchen.

![Das Fenster Richtlinie erneut versuchen in der Google Developer Console](../../images/tutorials/create/google-pubsub/retry-policy.png)

Sie müssen **die Aufbewahrungsdauer der Abonnementnachricht auf 24 Stunden oder mehr festlegen**, um sicherzustellen, dass nicht bestätigte Daten bei Spitzenladevorgängen nicht verloren gehen. Außerdem aktivieren Sie **ein Dead-Letter-Thema**, um sicherzustellen, dass Datenverlust auch in seltenen Edge-Fällen nicht eintritt.

>[!IMPORTANT]
>
>Pro [!DNL Google PubSub] Abonnement kann nur ein Datenfluss erstellt werden. Die Wiederverwendung eines Abonnements, auch über Sandboxes hinweg, führt zum Datenverlust.

## [!DNL Google PubSub] mit Experience Platform verbinden

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google PubSub] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

* [Erstellen einer Google PubSub-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer Quellverbindung für Google PubSub über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
