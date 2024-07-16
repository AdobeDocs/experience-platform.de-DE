---
keywords: Ereignisweiterleitungs-Erweiterung;Ausblenden;Ausblenden der Ereignisweiterleitungs-Erweiterung
title: Braze Event Forwarding-Erweiterung
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Edge Network-Ereignisse an Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 3%

---

# [!DNL Braze Track Events API]-Erweiterung zur Ereignisweiterleitung

[[!DNL Braze]](https://www.braze.com) ist eine Kundeninteraktionsplattform, die kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit ermöglicht. Mit [!DNL Braze] können Sie Folgendes tun:

- Bereitstellen von Daten (z. B. Marketing-Nachrichten) für zielgerichtete Benutzer basierend auf ihrer Sprachpräferenz, Standort-Präferenz und mehr, um Konversionsraten zu erhöhen und wichtige Geschäftsziele zu unterstützen.
- Senden Sie personalisierte Nachrichten an Kunden über verschiedene Kanäle, einschließlich E-Mail, Push-Benachrichtigungen und In-App-Nachrichten, zum richtigen Zeitpunkt und in ihrer bevorzugten Sprache.
- Richten Sie bestimmte Benutzer für Marketing- und Werbekampagnen ein, um die Anzahl der wiederkehrenden Kunden zu erhöhen.
- Untersuchen Sie das Benutzerverhalten und die Muster, um bestimmte Zielgruppen mit personalisierten Nachrichten anzusprechen, was zur Umsatzsteigerung beitragen könnte.

Mit der Erweiterung [!DNL Braze Track Events API] [ Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) können Sie im Adobe Experience Platform-Edge Network erfasste Daten nutzen und in Form von serverseitigen Ereignissen mithilfe der API [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) an [!DNL Braze] senden.

In diesem Dokument werden die Anwendungsfälle der Erweiterung, die Installation in Ihren Ereignisweiterleitungsbibliotheken und die Verwendung ihrer Funktionen in einer Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) behandelt.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network in [!DNL Braze] verwenden möchten, um die Analyse- und Targeting-Funktionen von Kunden nutzen zu können.

Angenommen, ein Einzelhandelsunternehmen verfügt über eine mehrkanalige Präsenz (Website und Mobilgeräte) und erfasst Transaktions- oder Konversionsdaten als Ereignisdaten von seiner Website und mobilen Plattformen. Mithilfe verschiedener [Tag](../../../home.md) -Regeln werden diese Daten in Echtzeit an das Edge Network gesendet. Von hier aus sendet die Ereignisweiterleitungs-Erweiterung [!DNL Braze] automatisch relevante Ereignisse vom Server an [!DNL Braze].

Nachdem die Daten gesendet wurden, können die Analyseteams des Unternehmens die [!DNL Braze's]-Funktionen nutzen, um die Datensätze zu verarbeiten und geschäftliche Einblicke zu gewinnen, um Diagramme, Dashboards oder andere Visualisierungen zu generieren, die geschäftliche Stakeholder informieren. Weitere Informationen zu den verschiedenen Anwendungsfällen der Plattform finden Sie auf der Seite [[!DNL Braze] Kunden](https://www.braze.com/customers) .

## [!DNL Braze] Voraussetzungen und Limits {#prerequisites}

Sie müssen über ein [!DNL Braze] -Konto verfügen, um seine Technologien nutzen zu können. Wenn Sie kein Konto haben, navigieren Sie zur Seite [Erste Schritte](https://www.braze.com/get-started/) auf [!DNL Braze], um eine Verbindung zu [!DNL Braze Sales] herzustellen und den Prozess zur Kontoerstellung zu starten.

### API-Limits

Die Erweiterung verwendet zwei APIs von [!DNL Braze] und ihre Beschränkungen sind unten dargestellt:

| API | Ratenbeschränkungen |
| --- | --- |
| [!DNL User Track] | 50.000 Anfragen pro Minute. Weitere Informationen finden Sie in der [[!DNL User Track] API-Dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) .<br> |
| [!DNL User Identify] | 20.000 Anfragen pro Minute. Weitere Informationen finden Sie in der [[!DNL User Identify] API-Dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) .<br> |

>[!NOTE]
>
> Weitere Informationen zu den von ihnen auferlegten Beschränkungen finden Sie im Handbuch zu [[!DNL Braze] API-Beschränkungen](https://www.braze.com/docs/api/api_limits/) .

### Abrechenbare Datenpunkte

Das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] kann Ihren [!DNL Braze] Datenpunktverbrauch erhöhen. Wenden Sie sich an Ihren [!DNL Braze] -Kundenbetreuer, bevor Sie zusätzliche benutzerdefinierte Attribute senden. Weitere Informationen finden Sie in der Dokumentation zu [!DNL Braze] für [abrechnungsfähige Datenpunkte](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable) .

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um das Edge Network mit [!DNL Braze] zu verbinden, sind die folgenden Eingaben erforderlich:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| [!DNL Braze] Instanz | Der REST-Endpunkt, der mit dem [!DNL Braze] -Konto verknüpft ist. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Braze] für [Instanzen](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) . | `https://rest.iad-03.braze.com` |
| API-Schlüssel | Der [!DNL Braze] API-Schlüssel, der mit dem [!DNL Braze] -Konto verknüpft ist. Die Anleitung für <br/>finden Sie in der [!DNL Braze] -Dokumentation zum [REST-API-Schlüssel](https://www.braze.com/docs/api/basics/#rest-api-key) . | `YOUR-BRAZE-REST-API-KEY` |

### Erstellen geheimer Daten

Erstellen Sie ein neues [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md) und legen Sie den Wert auf Ihren [[!DNL Braze] API-Schlüssel](#configuration-details) fest. Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert sicher bleibt.

## Installieren und Konfigurieren der [!DNL Braze] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Option **[!UICONTROL Installieren]** auf der Karte für die Erweiterung [!DNL Braze] aus.

![Installieren Sie die [!DNL Braze] -Erweiterung.](../../../images/extensions/server/braze/install-extension.png)

Geben Sie im nächsten Bildschirm die folgenden [Konfigurationswerte](#configuration-details) ein, die Sie zuvor aus [!DNL Braze] erfasst haben:

- **[!UICONTROL REST-Endpunkt-URL einblenden]**: Sie können den Wert Ihrer [!DNL Braze] REST-Endpunkt-URL als Nur-Text in die bereitgestellte Eingabe eingeben.
- **[!UICONTROL API-Schlüssel]**: Wählen Sie das zuvor erstellte [geheime Datenelement](#create-a-secret) aus, das Ihren [!DNL Braze]-API-Schlüssel enthält.

Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Konfigurationsseite der [!DNL Braze] Erweiterung.](../../../images/extensions/server/braze/configure-extension.png)

## Erstellen einer [!DNL Send Event] -Regel {#tracking-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen entsprechend Ihren Anforderungen. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung **[!UICONTROL Braze]** und dann für den Aktionstyp **[!UICONTROL Ereignis senden]** aus.

![Fügen Sie eine Aktionskonfiguration für die Ereignisweiterleitungsregel hinzu.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lang, zufällig und gut verteilt UUID oder GUID. Wenn Sie eine andere Methode wählen, mit der Sie Ihre Benutzer-IDs benennen können, müssen diese auch lang, zufällig und gut verteilt sein. Erfahren Sie mehr über [vorgeschlagene Benutzer-ID-Namenskonvention](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Benutzer-ID einblenden] | Anzeigen der Benutzer-ID. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzer anhand anderer Dimensionen als Ihrer Benutzer-ID zu identifizieren. <br><br> Das Benutzeralias-Objekt besteht aus zwei Teilen: einem alias_name für die Kennung selbst und einem alias_label, das den Aliastyp angibt. Benutzer können über mehrere Alias mit unterschiedlichen Bezeichnungen verfügen, jedoch nur einen Alias-Namen pro alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis an einen Benutzer zu binden, müssen Sie entweder das Feld [!UICONTROL Externe Benutzer-ID] oder das Feld [!UICONTROL Benutzer-IDs einblenden] oder den Abschnitt [!UICONTROL Benutzeralias] ausfüllen.

**[!UICONTROL Ereignisdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Ereignisname &#x200B;] | Name des Ereignisses. | Ja |
| [!UICONTROL Ereigniszeit] | Datum/Uhrzeit als Zeichenfolge im ISO 8601- oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`-Format. | Ja |
| [!UICONTROL App-ID] | Die App-ID oder <strong>app_id</strong> ist ein Parameter, der die Aktivität mit einer bestimmten App in Ihrer App-Gruppe verknüpft. Sie gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Erfahren Sie mehr über die [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Ereigniseigenschaften &#x200B;] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Für die Aktion **[!UICONTROL Ereignis-Versand durchführen]** müssen nur ein **[!UICONTROL Ereignisname]** und eine **[!UICONTROL Ereigniszeit]** angegeben werden. Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften aufnehmen. Weitere Informationen zum [!DNL Braze]-Ereignisobjekt finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, die ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellen oder aktualisieren. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenfolgen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (sonstiges), &quot;N&quot; (nicht zutreffend), &quot;P&quot; (es empfiehlt sich, nicht zu sagen). |
| [!UICONTROL Ort] | |
| [!UICONTROL Country] | Land als Zeichenfolge im Format [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) . |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge im Format [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format &quot;JJJ-MM-TT&quot;(z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Zeitzonenname aus der Zeitzonendatenbank [IANA (z. B. &quot;America/New_York&quot;oder &quot;Eastern Time (US &amp; Canada)&quot;).](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) |
| [!UICONTROL Facebook] | Hash, der eine beliebige ID (Zeichenfolge), &quot;Gefällt mir&quot;(Array von Zeichenfolgen), &quot;num_friends&quot;(Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der ID (Integer), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Integer), friends_count (Integer), statuses_count(Integer) enthält. |

{style="table-layout:auto"}

## Erstellen einer [!DNL Send Purchase Event] -Regel {#purchase-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen entsprechend Ihren Anforderungen. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung **[!UICONTROL Braze]** und dann für den Aktionstyp **[!UICONTROL Kaufereignis senden]** aus.

![Fügen Sie die Konfiguration der Ereignisweiterleitungsregel für den Aktionstyp &quot;Kauf bremsen&quot;hinzu.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lang, zufällig und gut verteilt UUID oder GUID. Wenn Sie eine andere Methode wählen, mit der Sie Ihre Benutzer-IDs benennen können, müssen diese auch lang, zufällig und gut verteilt sein. Erfahren Sie mehr über [vorgeschlagene Benutzer-ID-Namenskonvention](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Benutzer-ID einblenden] | Anzeigen der Benutzer-ID. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzer anhand anderer Dimensionen als Ihrer Benutzer-ID zu identifizieren. <br><br> Das Benutzeralias-Objekt besteht aus zwei Teilen: einem alias_name für die Kennung selbst und einem alias_label, das den Aliastyp angibt. Benutzer können über mehrere Alias mit unterschiedlichen Bezeichnungen verfügen, jedoch nur einen Alias-Namen pro alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis mit einem Benutzer zu verknüpfen, müssen Sie entweder das Feld [!UICONTROL Externe Benutzer-ID], das Feld [!UICONTROL Benutzer-ID einblenden] oder den Abschnitt [!UICONTROL Benutzeralias] ausfüllen.

**[!UICONTROL Kaufdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Produkt-ID &#x200B;] | Kennung für den Kauf. (z. B. Produktname oder Produktkategorie) | Ja |
| [!UICONTROL Kaufzeit] | Datum/Uhrzeit als Zeichenfolge im ISO 8601- oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`-Format. | Ja |
| [!UICONTROL &#x200B; ] | Währung als Zeichenfolge im Format [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217) Alphabetischer Währungscode. | Ja |
| [!UICONTROL Preis &#x200B;] | Preis. | Ja |
| [!UICONTROL Quantity &#x200B;] | Wenn kein Wert angegeben wird, ist der Standardwert 1. Der Höchstwert muss unter 100 liegen. | |
| [!UICONTROL App-ID] | Die App-ID oder <strong>app_id</strong> ist ein Parameter, der die Aktivität mit einer bestimmten App in Ihrer App-Gruppe verknüpft. Sie gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Erfahren Sie mehr über die [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Eigenschaften für Kauf &#x200B;] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Kaufs. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Für die Aktion **[!UICONTROL Ereignis-Versand durchführen]** müssen nur ein **[!UICONTROL Ereignisname]** und eine **[!UICONTROL Ereigniszeit]** angegeben werden. Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften aufnehmen. Weitere Informationen zum [!DNL Braze]-Ereignisobjekt finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, die ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellen oder aktualisieren. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenfolgen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (sonstiges), &quot;N&quot; (nicht zutreffend), &quot;P&quot; (es empfiehlt sich, nicht zu sagen). |
| [!UICONTROL Ort] | |
| [!UICONTROL Country] | Land als Zeichenfolge im Format [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) . |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge im Format [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format &quot;JJJ-MM-TT&quot;(z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Zeitzonenname aus der Zeitzonendatenbank [IANA (z. B. &quot;America/New_York&quot;oder &quot;Eastern Time (US &amp; Canada)&quot;).](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) |
| [!UICONTROL Facebook] | Hash, der eine beliebige ID (Zeichenfolge), &quot;Gefällt mir&quot;(Array von Zeichenfolgen), &quot;num_friends&quot;(Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der ID (Integer), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Integer), friends_count (Integer), statuses_count(Integer) enthält. |

{style="table-layout:auto"}

## Daten mit [!DNL Braze] validieren {#validate}

Wenn die Ereigniserfassung und die Integration von [!DNL Adobe Experience Platform] erfolgreich waren, werden Ereignisse in der Konsole [!DNL Braze] angezeigt, wenn [ Benutzerprofile anzeigen](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Insbesondere spiegeln sich die neuen Ereignisdaten, die an [!DNL Braze] gesendet werden, im Abschnitt [!DNL Purchases] auf der Registerkarte [Überblick eines bestimmten Benutzers](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab) wider.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Braze] gesendet werden. Weitere Informationen zu nachgelagerten Anwendungen für Ereignisdaten, die an [!DNL Braze] gesendet werden, finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs).

Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
