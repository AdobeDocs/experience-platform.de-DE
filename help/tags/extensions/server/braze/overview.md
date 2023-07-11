---
keywords: Ereignisweiterleitungs-Erweiterung;Ausblenden;Ausblenden der Ereignisweiterleitungs-Erweiterung
title: Braze Event Forwarding-Erweiterung
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Adobe Experience Edge Network-Ereignisse an Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 6%

---

# [!DNL Braze Track Events API]-Erweiterung zur Ereignisweiterleitung

[[!DNL Braze]](https://www.braze.com) ist eine Kundeninteraktionsplattform, die kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit ermöglicht. Verwenden [!DNL Braze]können Sie Folgendes tun:

- Bereitstellen von Daten (z. B. Marketing-Nachrichten) für zielgerichtete Benutzer basierend auf ihrer Sprachpräferenz, Standort-Präferenz und mehr, um Konversionsraten zu erhöhen und wichtige Geschäftsziele zu unterstützen.
- Senden Sie personalisierte Nachrichten an Kunden über verschiedene Kanäle, einschließlich E-Mail, Push-Benachrichtigungen und In-App-Nachrichten, zum richtigen Zeitpunkt und in ihrer bevorzugten Sprache.
- Richten Sie bestimmte Benutzer für Marketing- und Werbekampagnen ein, um die Anzahl der wiederkehrenden Kunden zu erhöhen.
- Untersuchen Sie das Benutzerverhalten und die Muster, um bestimmte Zielgruppen mit personalisierten Nachrichten anzusprechen, was zur Umsatzsteigerung beitragen könnte.

Die [!DNL Braze Track Events API] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) -Erweiterung ermöglicht es Ihnen, die im Adobe Experience Platform Edge Network erfassten Daten zu nutzen und an [!DNL Braze] in Form von serverseitigen Ereignissen, bei denen die [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

In diesem Dokument werden die Anwendungsfälle der Erweiterung, die Installation in Ihren Ereignisweiterleitungsbibliotheken und die Verwendung ihrer Funktionen in der Ereignisweiterleitung behandelt. [Regel](../../../ui/managing-resources/rules.md).

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge-Netzwerk in [!DNL Braze] , um die Analyse- und Targeting-Funktionen der Kunden zu nutzen.

Angenommen, ein Einzelhandelsunternehmen verfügt über eine mehrkanalige Präsenz (Website und Mobilgeräte) und erfasst Transaktions- oder Konversionsdaten als Ereignisdaten von seiner Website und mobilen Plattformen. Verwendung verschiedener [Tag](../../../home.md) Regeln, werden diese Daten in Echtzeit an das Edge-Netzwerk gesendet. Von hier aus kann die [!DNL Braze] Ereignisweiterleitungserweiterung sendet automatisch relevante Ereignisse an [!DNL Braze] vom Server aus.

Sobald die Daten gesendet wurden, können die Analyseteams des Unternehmens [!DNL Braze's] Funktionen zur Verarbeitung der Datensätze und Ableitung von Geschäftsinsights, um Diagramme, Dashboards oder andere Visualisierungen zu generieren, die geschäftliche Stakeholder informieren. Siehe Abschnitt [[!DNL Braze] Kunden](https://www.braze.com/customers) für weitere Informationen zu den verschiedenen Anwendungsfällen der Plattform.

## [!DNL Braze] Voraussetzungen und Limits {#prerequisites}

Sie müssen über eine [!DNL Braze] , um seine Technologien zu nutzen. Wenn Sie kein Konto haben, navigieren Sie zu [Erste Schritte](https://www.braze.com/get-started/) on [!DNL Braze] zur Verbindung mit [!DNL Braze Sales] und starten Sie die Kontoerstellung.

### API-Limits

Die Erweiterung verwendet zwei von [!DNL Braze]Die APIs und ihre Beschränkungen sind unten beschrieben:

| API | Ratenbeschränkungen |
| --- | --- |
| [!DNL User Track] | 50.000 Anfragen pro Minute. <br>Siehe Abschnitt [[!DNL User Track] API-Dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) für Details. |
| [!DNL User Identify] | 20.000 Anfragen pro Minute. <br>Siehe Abschnitt [[!DNL User Identify] API-Dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) für Details. |

>[!NOTE]
>
> Weitere Informationen finden Sie im Handbuch [[!DNL Braze] API-Beschränkungen](https://www.braze.com/docs/api/api_limits/) weitere Einzelheiten zu den von ihnen auferlegten Beschränkungen.

### Abrechenbare Datenpunkte

Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] kann die [!DNL Braze] Datenpunktverbrauch. Wenden Sie sich an Ihre [!DNL Braze] Kundenbetreuer vor dem Senden zusätzlicher benutzerdefinierter Attribute. Siehe Abschnitt [!DNL Braze] Dokumentation zu [Abrechnungsdatenpunkte](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) für weitere Informationen.

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um das Edge-Netzwerk mit [!DNL Braze], sind folgende Eingaben erforderlich:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| [!DNL Braze] Instanz | Der REST-Endpunkt, der mit dem [!DNL Braze] -Konto. Siehe Abschnitt [!DNL Braze] Dokumentation zu [Instanzen](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) für Leitlinien. | `https://rest.iad-03.braze.com` |
| API-Schlüssel | Die [!DNL Braze] API-Schlüssel, der mit dem [!DNL Braze] -Konto. <br/>Siehe Abschnitt [!DNL Braze] Dokumentation zu [REST-API-Schlüssel](https://www.braze.com/docs/api/basics/#rest-api-key) für Leitlinien. | `YOUR-BRAZE-REST-API-KEY` |

### Erstellen geheimer Daten

Erstellen Sie eine neue [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md) und legen Sie den Wert auf Ihre [[!DNL Braze] API-Schlüssel](#configuration-details). Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert sicher bleibt.

## Installieren und konfigurieren Sie die [!DNL Braze] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** Registerkarte, wählen Sie **[!UICONTROL Installieren]** auf der Karte für die [!DNL Braze] -Erweiterung.

![[!DNL Braze]Installieren der Erweiterung.](../../../images/extensions/server/braze/install-extension.png)

Geben Sie im nächsten Bildschirm Folgendes ein: [Konfigurationswerte](#configuration-details) die Sie zuvor aus [!DNL Braze]:

- **[!UICONTROL Rest-Endpunkt-URL löschen]**: Sie können den Wert Ihrer [!DNL Braze] REST-Endpunkt-URL als Nur-Text in der bereitgestellten Eingabe.
- **[!UICONTROL API-Schlüssel]**: Wählen Sie die [Geheimdatenelement](#create-a-secret) die Sie zuvor erstellt haben und die [!DNL Braze] API-Schlüssel.

Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die [!DNL Braze] Erweiterungskonfigurationsseite.](../../../images/extensions/server/braze/configure-extension.png)

## Erstellen Sie eine [!DNL Send Event] Regel {#tracking-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung. [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL Brase]** Erweiterung und wählen Sie **[!UICONTROL Ereignis senden]** für den Aktionstyp.

![Fügen Sie eine Aktionskonfiguration für Ereignisweiterleitungsregeln hinzu.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lange, zufällige und gut verteilte UUID oder GUID. Wenn Sie eine andere Methode wählen, mit der Sie Ihre Benutzer-IDs benennen können, müssen diese auch lang, zufällig und gut verteilt sein. Weitere Informationen [vorgeschlagene Benutzer-ID-Benennungskonvention](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Benutzer-ID speichern] | Anzeigen der Benutzer-ID. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzer anhand anderer Dimensionen als Ihrer Benutzer-ID zu identifizieren. <br><br> Das user alias -Objekt besteht aus zwei Teilen: ein alias_name für die Kennung selbst und ein alias_label, der den Aliastyp angibt. Benutzer können über mehrere Alias mit unterschiedlichen Bezeichnungen verfügen, jedoch nur einen Alias-Namen pro alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis an einen Benutzer zu binden, müssen Sie entweder [!UICONTROL Externe Benutzer-ID] oder das [!UICONTROL Benutzerkennung für Blitzen] oder [!UICONTROL Benutzeralias] Abschnitt.

**[!UICONTROL Ereignisdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Ereignisname &#x200B;] | Name des Ereignisses. | Ja |
| [!UICONTROL Ereigniszeit] | Datum/Uhrzeit als Zeichenfolge in ISO 8601 oder in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` Format. | Ja |
| [!UICONTROL App-Kennung] | App-ID oder <strong>app_id</strong> ist ein Parameter, der die Aktivität mit einer bestimmten App in Ihrer App-Gruppe verknüpft. Sie gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Weitere Informationen zum [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Ereigniseigenschaften &#x200B;] | Ein JSON-Objekt, das benutzerdefinierte Eigenschaften des Ereignisses enthält. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Die **[!UICONTROL Ereignis &quot;Senden&quot;]** -Aktion erfordert nur **[!UICONTROL Ereignisname]** und **[!UICONTROL Ereigniszeit]** angegeben werden. Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften einfügen. Weitere Informationen finden Sie unter [!DNL Braze] event -Objekt, siehe [amtliche Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, die ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellen oder aktualisieren. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Telefon] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenfolgen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (sonstiges), &quot;N&quot; (nicht zutreffend), &quot;P&quot; (es vorziehen, nicht zu sagen). |
| [!UICONTROL Stadt] | |
| [!UICONTROL Country] | Land als Zeichenfolge in [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) Format. |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge in [ISO-639-1](https://de.wikipedia.org/wiki/Liste_der_ISO-639-1-Codes) Format. |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format &quot;JJJ-MM-TT&quot;(z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Zeitzonenname aus [IANA-Zeitzonen-Datenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (z. B. &quot;America/New_York&quot;oder &quot;Eastern Time (US &amp; Canada)&quot;). |
| [!UICONTROL Facebook] | Hash, der eine beliebige ID (Zeichenfolge), &quot;Gefällt mir&quot;(Array von Zeichenfolgen), &quot;num_friends&quot;(Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der ID (Integer), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Integer), friends_count (Integer), statuses_count(Integer) enthält. |

{style="table-layout:auto"}

## Erstellen Sie eine [!DNL Send Purchase Event] Regel {#purchase-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung. [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL Brase]** Erweiterung und wählen Sie **[!UICONTROL Kaufereignis senden]** für den Aktionstyp.

![Fügen Sie die Konfiguration der Ereignisweiterleitungsregel vom Typ Aktion für den Kauf eines Leerlaufs hinzu.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lange, zufällige und gut verteilte UUID oder GUID. Wenn Sie eine andere Methode wählen, mit der Sie Ihre Benutzer-IDs benennen können, müssen diese auch lang, zufällig und gut verteilt sein. Weitere Informationen [vorgeschlagene Benutzer-ID-Benennungskonvention](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Benutzer-ID speichern] | Anzeigen der Benutzer-ID. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzer anhand anderer Dimensionen als Ihrer Benutzer-ID zu identifizieren. <br><br> Das user alias -Objekt besteht aus zwei Teilen: ein alias_name für die Kennung selbst und ein alias_label, der den Aliastyp angibt. Benutzer können über mehrere Alias mit unterschiedlichen Bezeichnungen verfügen, jedoch nur einen Alias-Namen pro alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis mit einem Benutzer zu verknüpfen, müssen Sie entweder [!UICONTROL Externe Benutzer-ID] -Feld, die [!UICONTROL Benutzerkennung für Blitzen] oder das [!UICONTROL Benutzeralias] Abschnitt.

**[!UICONTROL Kaufdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Produkt-ID &#x200B;] | Kennung für den Kauf. (z. B. Produktname oder Produktkategorie) | Ja |
| [!UICONTROL Kaufzeit] | Datum/Uhrzeit als Zeichenfolge in ISO 8601 oder in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` Format. | Ja |
| [!UICONTROL Währung &#x200B;] | Währung als Zeichenfolge in [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217) Alphabetisches Währungscode-Format. | Ja |
| [!UICONTROL Preis &#x200B;] | Preis. | Ja |
| [!UICONTROL Menge &#x200B;] | Wenn kein Wert angegeben wird, ist der Standardwert 1. Der Höchstwert muss unter 100 liegen. | |
| [!UICONTROL App-Kennung] | App-ID oder <strong>app_id</strong> ist ein Parameter, der die Aktivität mit einer bestimmten App in Ihrer App-Gruppe verknüpft. Sie gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Weitere Informationen zum [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL &#x200B;] | Ein JSON-Objekt, das benutzerdefinierte Eigenschaften des Kaufs enthält. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Die **[!UICONTROL Ereignis &quot;Senden&quot;]** -Aktion erfordert nur **[!UICONTROL Ereignisname]** und **[!UICONTROL Ereigniszeit]** angegeben werden. Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften einfügen. Weitere Informationen finden Sie unter [!DNL Braze] event -Objekt, siehe [amtliche Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, die ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellen oder aktualisieren. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Telefon] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenfolgen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (sonstiges), &quot;N&quot; (nicht zutreffend), &quot;P&quot; (es vorziehen, nicht zu sagen). |
| [!UICONTROL Stadt] | |
| [!UICONTROL Country] | Land als Zeichenfolge in [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) Format. |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge in [ISO-639-1](https://de.wikipedia.org/wiki/Liste_der_ISO-639-1-Codes) Format. |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format &quot;JJJ-MM-TT&quot;(z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Zeitzonenname aus [IANA-Zeitzonen-Datenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (z. B. &quot;America/New_York&quot;oder &quot;Eastern Time (US &amp; Canada)&quot;). |
| [!UICONTROL Facebook] | Hash, der eine beliebige ID (Zeichenfolge), &quot;Gefällt mir&quot;(Array von Zeichenfolgen), &quot;num_friends&quot;(Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der ID (Integer), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Integer), friends_count (Integer), statuses_count(Integer) enthält. |

{style="table-layout:auto"}

## Validieren von Daten in [!DNL Braze] {#validate}

Wenn die Ereigniskollektion und [!DNL Adobe Experience Platform] -Integration erfolgreich war, werden Ereignisse im [!DNL Braze] console when [Anzeigen von Benutzerprofilen](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Insbesondere die neuen Ereignisdaten, die an [!DNL Braze] wird im [!DNL Purchases] -Abschnitt eines bestimmten Benutzers [Übersichtsregisterkarte](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse an gesendet werden [!DNL Braze] über die Ereignisweiterleitung. Weitere Informationen zu nachgelagerten Anwendungen für Ereignisdaten, die an gesendet werden [!DNL Braze], siehe [amtliche Dokumentation](https://www.braze.com/docs).

Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
