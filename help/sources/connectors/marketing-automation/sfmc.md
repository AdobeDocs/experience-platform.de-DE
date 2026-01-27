---
title: Übersicht über Salesforce Marketing Cloud (v2) Source
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud (V2) mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Übersicht über die [!DNL Salesforce Marketing Cloud] (V2)-Quelle

>[!IMPORTANT]
>
>Die ursprüngliche [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md)-Quelle wird seit Januar 2026 nicht mehr unterstützt. Für diese veraltete Quelle sind keine Migrationen verfügbar und Sie müssen Ihre Daten mit der neuen [!DNL Salesforce Marketing Cloud] (V2)-Quelle erneut implementieren.

Die Integration zwischen Adobe [Real-Time CDP](../../../rtcdp/overview.md) und [!DNL Salesforce Marketing Cloud] wurde entwickelt, um aufgrund der Flexibilität und Kontrolle, die sie bieten, Datenerweiterungen zu nutzen. Im Gegensatz zu standardmäßigen Systemtabellen (Datenansichten und integrierte Objekte), die auf vordefinierte Felder beschränkt sind und hauptsächlich der Nachverfolgung auf Systemebene dienen, können Sie Datenerweiterungen verwenden, um benutzerdefinierte Felder zu definieren, eine Vielzahl von geschäftsspezifischen Daten zu organisieren und Ihre Datenstrukturen an individuelle Anforderungen anzupassen.

Aufgrund dieses Maßes an Anpassung und Skalierbarkeit beruht die Integration zwischen Real-Time CDP und [!DNL Salesforce Marketing Cloud] auf Datenerweiterungen und nicht auf standardmäßigen Systemtabellen. Dieser Ansatz bietet eine flexiblere, skalierbarere und besser integrierte Grundlage für die Verwaltung von Daten und stellt sicher, dass sie mit Ihren Geschäftszielen übereinstimmen

Sie können die [!DNL Salesforce Marketing Cloud] verwenden, um Ihr [!DNL Salesforce Marketing Cloud]-Konto mit Real-Time CDP und Adobe Experience Platform zu verbinden. Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie beginnen.

## Anwendungsbeispiele {#use-case-examples}

### E-Mail-Kampagnen mit Kontaktdaten personalisieren

Eine Einzelhandelsmarke möchte E-Mail-Kampagnen basierend auf den Lebenszyklusphasen des Kunden personalisieren (z. B. Neukunde, wiederkehrender Käufer, treuer Kunde). Dazu erstellen sie eine Kontaktdatenerweiterung, in der wichtige Kundeninformationen, einschließlich Name, E-Mail, Lebenszyklus-Phase und Kaufverhalten, gespeichert werden. Diese Daten werden dann in Experience Platform aufgenommen, um eine tiefere Segmentierung und Zielgruppenbestimmung zu ermöglichen.

Durch die Aufnahme der Daten aus der Kontaktdatenerweiterung in Experience Platform kann die Marke Kundinnen und Kunden basierend auf ihrer Lebenszyklusphase und ihrem Kaufverhalten segmentieren. Sie können beispielsweise ein Willkommensangebot an neue Kunden, eine Treueprämie für Wiederholungskäufer oder sogar inaktive Kunden erneut mit zielgerichteten Angeboten interagieren. Dieser Ansatz stellt eine personalisierte Kommunikation sicher und ermöglicht eine relevantere und effektivere Kundeninteraktion.

### Aufnahme von Campaign-Daten für die personalisierte Segmentierung

Ein Marketing-Team möchte seine E-Mail-Kampagnen optimieren, indem es Kunden entsprechend ihrer Interaktion mit vorherigen Kampagnen anspricht. Dazu erstellen sie eine Campaign-Datenerweiterung, [!DNL Salesforce Marketing Cloud] Kundeninteraktionsdaten wie E-Mail-Öffnungen, Klicks und Kampagnenantworten zu speichern. Diese Daten werden dann in Experience Platform zur weiteren Segmentierung und Personalisierung aufgenommen.

Durch die Aufnahme dieser Daten aus der Campaign-Datenerweiterung in Experience Platform kann das Marketing-Team Kundinnen und Kunden basierend auf früheren Interaktionen segmentieren, z. B. solche, die auf Produktangebote geklickt haben oder positiv geantwortet haben. Kunden, die mit interagiert haben, können in zukünftigen E-Mails zielgerichtete Promotions erhalten, während Kunden, die negativ reagiert haben, Follow-ups des Kundendienstes gesendet werden können. Durch diese Integration mit Experience Platform kann das Marketing-Team je nach Kundenverhalten personalisiertere und relevantere Inhalte bereitstellen.

### Auf Aktivitätsdaten basierende Zielgruppenbestimmung von Kunden

Ein Marketing-Team möchte Kundinnen und Kunden auf der Grundlage ihrer Aktivitäten ansprechen, z. B. Website-Besuche, Formularübermittlungen oder Interaktionen mit vorherigen E-Mail-Kampagnen. Dazu erstellen sie eine Datenerweiterung für Aktivitäten , um Informationen über die Interaktionsaktivitäten jedes Kunden zu speichern. Diese Daten werden dann in Experience Platform aufgenommen, um eine weitere Segmentierung und ein personalisiertes Kampagnen-Targeting zu ermöglichen.

Durch die Aufnahme der Daten aus der Aktivitäts-Datenerweiterung in Experience Platform kann das Marketing-Team Kundinnen und Kunden basierend auf ihrem Interaktionsverlauf segmentieren. Kunden, die kürzlich die Website besucht haben, aber keinen Kauf getätigt haben, können beispielsweise Erinnerungs-E-Mails mit speziellen Angeboten erhalten. Ebenso können Kunden, die ein Formular ausgefüllt haben, personalisierte Folgenachrichten erhalten. Dieser Ansatz stellt sicher, dass alle Kundinnen und Kunden relevante Inhalte erhalten, die auf ihren jüngsten Aktivitäten basieren, und verbessert Interaktions- und Konversionsraten.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung vorzunehmen, die Sie durchführen müssen, bevor Sie Ihre Quelle mit Experience Platform verbinden können.

### Einrichten der Anwendung für die Authentifizierung {#set-up-application-for-authentication}

Beim Erstellen einer Integration mit [!DNL Salesforce Marketing Cloud] besteht einer der ersten Schritte darin, in **ein** Installiertes Paket[!DNL Salesforce Marketing Cloud] zu erstellen. Das installierte Paket generiert die Client-Anmeldeinformationen, die zum Authentifizieren von API-Aufrufen erforderlich sind, definiert den Integrationstyp und die zugehörigen Berechtigungsbereiche. Darüber hinaus stellt das installierte Paket die richtigen API-Endpunkte für Ihren Mandanten bereit. Sie dient auch als verwalteter Container für die Verwaltung, Überwachung und Sperrung des Zugriffs, um sicherzustellen, dass alle Integrationen sicher und überprüfbar sind und mit dem von Salesforce empfohlenen Authentifizierungsmodell übereinstimmen.

Um ein installiertes Paket zu erstellen, verwenden Sie die [!DNL Salesforce Marketing Cloud]-Benutzeroberfläche, navigieren Sie zu **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** und klicken Sie auf **[!DNL New]**. Verwenden Sie die [!DNL New Package Details], um einen Namen und Informationen für Ihr Paket anzugeben. Wenn Sie fertig sind, wählen Sie **[!DNL Save]** aus.

![Die neue Paketschnittstelle der Benutzeroberfläche von Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/new-package.png)

Nachdem das neue Paket erstellt wurde, wählen Sie **[!DNL Add Component]** aus.

![Die Benutzeroberfläche „Komponente hinzufügen“ der Salesforce Marketing Cloud-Benutzeroberfläche.](../../images/tutorials/create/sfmc/add-component.png)

Wählen Sie **[!DNL API Integration]** als Komponententyp aus.

![Das Komponentenauswahl-Fenster mit ausgewählter Option „API-Integration“](../../images/tutorials/create/sfmc/api-integration.png)

Wählen Sie **[!DNL Server-to-Server]** als Integrationstyp aus.

![Das Auswahlfenster für Integrationstypen](../../images/tutorials/create/sfmc/server-to-server.png)

Navigieren Sie abschließend zu **[!DNL Scope]** > **[!DNL Data]**. Wählen Sie unter **[!DNL Data Extensions]** die Option **[!DNL Read]**.

![Der Abschnitt zu Datenerweiterungen von Scope in Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Wählen Sie **[!DNL Save]** und kopieren und speichern Sie Ihr **Client-Geheimnis**. Wenn Sie fertig sind, wählen Sie **[!DNL Finish]** aus.

![Das Salesforce Marketing Cloud-Fenster zum Generieren eines Client-Geheimnisses.](../../images/tutorials/create/sfmc/generate-secret.png)

Kopieren Sie vor dem Verlassen der [!DNL Salesforce Marketing Cloud]-Benutzeroberfläche **Client-ID** und **eindeutiges Basis-URI-Präfix**, da Sie beide Werte verwenden werden, um eine Verbindung zu Experience Platform herzustellen. Für den Authentifizierungsbasis-URI müssen Sie sicherstellen, dass Sie alles nach dem `.auth.marketingcloudapis.com/` entfernen

![Die Salesforce Marketing Cloud-Komponentenschnittstelle, über die die Client-ID und der eindeutige Basis-URI abgerufen werden können.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Ausführliche Anweisungen zum Erstellen eines installierten Pakets finden Sie in der [[!DNL Salesforce] Dokumentation](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Sammeln erforderlicher Anmeldedaten {#gather-required-credentials}

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL Salesforce Marketing Cloud] mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Client-ID | Die öffentlich zugängliche Kennung, die von [!DNL Salesforce Marketing Cloud] zur Identifizierung Ihres Kontos bei der Autorisierung für Experience Platform verwendet wird. Die Client-ID kann über das Bedienfeld „Komponenten“ der [!DNL Salesforce Marketing Cloud]-Benutzeroberfläche abgerufen werden. |
| Client-Geheimnis | Der vertrauliche Schlüssel, der nur der Client-Anwendung und dem Autorisierungsserver bekannt ist. Sie können Ihr Client-Geheimnis generieren, indem Sie die [oben beschriebenen Schritte zum Einrichten der Anwendung](#set-up-application-for-authentication) befolgen. |
| Basis-Endpunkt | Das Präfix Ihres Authentifizierungsbasis-URI für [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform

Fahren Sie mit der Konfiguration Ihrer [!DNL Salesforce Marketing Cloud]-Quellverbindung in Experience Platform fort. Eine schrittweise Anleitung zum Einrichten der Verbindung über die Benutzeroberfläche finden Sie im [Tutorial hier](../../tutorials/ui/create/marketing-automation/sfmc.md). Lesen Sie dieses Tutorial, um mehr über das Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos, das Auswählen von Daten, das Zuordnen von Feldern, das Planen von Aufnahmen und das Überwachen Ihrer Datenflüsse zu erfahren.
