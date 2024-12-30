---
keywords: -Erweiterung für die Ereignisweiterleitung;Braze;Braze-Erweiterung für die Ereignisweiterleitung
title: Braze-Ereignisweiterleitungserweiterung
description: Diese Adobe Experience Platform-Ereignisweiterleitungserweiterung sendet Edge Network-Ereignisse an Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 3%

---

# [!DNL Braze Track Events API]-Erweiterung zur Ereignisweiterleitung

[[!DNL Braze]](https://www.braze.com) ist eine Plattform zur Kundeninteraktion, die kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit ermöglicht. Mit [!DNL Braze] können Sie Folgendes tun:

- Liefern Sie Daten (z. B. Marketing-Nachrichten) an ausgewählte Benutzer basierend auf deren Sprachpräferenz, Standortpräferenz und mehr, um die Konversionsraten zu erhöhen und wichtige Geschäftsziele zu unterstützen.
- Senden Sie Kundinnen und Kunden personalisierte Nachrichten über mehrere Kanäle hinweg, einschließlich E-Mail, Push-Benachrichtigungen und In-App-Nachrichten, zur richtigen Zeit und in den bevorzugten Sprachen.
- Targeting spezifischer Benutzer für Marketing- und Werbekampagnen, um die Anzahl der Bestandskunden zu erhöhen.
- Untersuchen Sie das Benutzerverhalten und die Muster, um bestimmte Zielgruppen mit benutzerdefinierten Nachrichten anzusprechen, was zu einer Umsatzsteigerung beitragen könnte.

Mit [ Erweiterung [!DNL Braze Track Events API]Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) können Sie die im Adobe Experience Platform-Edge Network erfassten Daten nutzen und in Form von Server-seitigen Ereignissen mithilfe der [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track)-API an [!DNL Braze] senden.

In diesem Dokument werden die Anwendungsfälle der Erweiterung behandelt und beschrieben, wie Sie sie in Ihren Bibliotheken für die Ereignisweiterleitung installieren und wie Sie ihre Funktionen in einer Regel für die [ verwenden](../../../ui/managing-resources/rules.md).

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network verwenden möchten, [!DNL Braze] die Analyse- und Targeting-Funktionen von Customer Journey Analytics zu nutzen.

Nehmen wir zum Beispiel ein Einzelhandelsunternehmen mit einer kanalübergreifenden Präsenz (Website und Mobilgerät), das Transaktions- oder Konversationseingaben als Ereignisdaten von seiner Website und seinen mobilen Plattformen erfasst. Mithilfe verschiedener [Tag](../../../home.md)-Regeln werden diese Daten in Echtzeit an das Edge Network gesendet. Von hier aus sendet die [!DNL Braze]-Erweiterung für die Ereignisweiterleitung automatisch relevante Ereignisse von der Server-Seite an [!DNL Braze].

Nach dem Versand der Daten können die Analyse-Teams des Unternehmens dann [!DNL Braze's] Funktionen nutzen, um die Datensätze zu verarbeiten und geschäftliche Einblicke abzuleiten, um Diagramme, Dashboards oder andere Visualisierungen zu generieren, um geschäftliche Stakeholder zu informieren. Weitere Informationen zu den verschiedenen Anwendungsfällen [[!DNL Braze]  Plattform finden ](https://www.braze.com/customers) auf der Seite „Kunden“.

## [!DNL Braze] Voraussetzungen und Leitlinien {#prerequisites}

Sie müssen über ein [!DNL Braze]-Konto verfügen, um seine Technologien verwenden zu können. Wenn Sie noch kein Konto haben, navigieren Sie zur Seite [Erste Schritte](https://www.braze.com/get-started/) auf [!DNL Braze], um eine Verbindung zu [!DNL Braze Sales] herzustellen und mit der Kontoerstellung zu beginnen.

### API-Leitplanken

Die Erweiterung verwendet zwei APIs von [!DNL Braze] und ihre Einschränkungen sind unten beschrieben:

| API | Ratenbeschränkungen |
| --- | --- |
| [!DNL User Track] | 50.000 Anfragen pro Minute. <br> Informationen finden Sie in der [[!DNL User Track] API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit)Dokumentation. |
| [!DNL User Identify] | 20.000 Anfragen pro Minute. <br> Informationen finden Sie in der [[!DNL User Identify] API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit)Dokumentation. |

>[!NOTE]
>
> Siehe das Handbuch zu [[!DNL Braze] API-Beschränkungen](https://www.braze.com/docs/api/api_limits/) für weitere Informationen zu den Beschränkungen, die sie vorschreiben.

### Fakturierbare Datenpunkte

Das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] kann die Nutzung Ihrer [!DNL Braze]-Datenpunkte erhöhen. Wenden Sie sich an Ihren [!DNL Braze] Account Manager, bevor Sie zusätzliche benutzerdefinierte Attribute senden. Weitere Informationen finden Sie in der [!DNL Braze] Dokumentation [Abrechnungsfähige ](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable)).

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um das Edge Network an [!DNL Braze] anzuschließen, sind folgende Eingaben erforderlich:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Instanz [!DNL Braze] | Der mit dem [!DNL Braze]-Konto verknüpfte REST-Endpunkt. Eine Anleitung finden Sie in der [!DNL Braze] Dokumentation [Instanzen](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) . | `https://rest.iad-03.braze.com` |
| API-Schlüssel | Der mit dem [!DNL Braze]-Konto verknüpfte [!DNL Braze]-API-Schlüssel. <br/>Anleitungen finden Sie in der [!DNL Braze]-Dokumentation zum [REST-API](https://www.braze.com/docs/api/basics/#rest-api-key)Schlüssel. | `YOUR-BRAZE-REST-API-KEY` |

### Erstellen geheimer Daten

Erstellen Sie ein neues [Geheimnis für die Ereignisweiterleitung](../../../ui/event-forwarding/secrets.md) und legen Sie den Wert auf Ihren [[!DNL Braze] -API-Schlüssel ](#configuration-details). Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren und dabei den Wert sicher zu halten.

## Installieren und Konfigurieren der [!DNL Braze] {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft oder ](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der **[!UICONTROL Katalog]**-Registerkarte **[!UICONTROL Installieren]** auf der Karte für die [!DNL Braze] aus.

![Installieren der [!DNL Braze]-Erweiterung.](../../../images/extensions/server/braze/install-extension.png)

Geben Sie im nächsten Bildschirm die folgenden [Konfigurationswerte](#configuration-details) ein, die Sie zuvor aus [!DNL Braze] erfasst haben:

- **[!UICONTROL Braze-REST-Endpunkt]** URL: Sie können den Wert Ihrer [!DNL Braze]-REST-Endpunkt-URL als Nur-Text in die bereitgestellte Eingabe eingeben.
- **[!UICONTROL API-Schlüssel]**: Wählen Sie das zuvor erstellte [Geheime](#create-a-secret)Datenelement aus, das Ihren [!DNL Braze] API-Schlüssel enthält.

Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Konfigurationsseite der [!DNL Braze]-Erweiterung.](../../../images/extensions/server/braze/configure-extension.png)

## Erstellen einer [!DNL Send Event] Regel {#tracking-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL Braze]**-Erweiterung aus und wählen Sie dann **[!UICONTROL Ereignis senden]** für den Aktionstyp aus.

![Fügen Sie eine Regelaktionskonfiguration für die Ereignisweiterleitung hinzu.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lange, zufällige und gut verteilte UUID oder GUID. Wenn Sie eine andere Methode zur Benennung Ihrer Benutzer-IDs auswählen, müssen diese auch lang, zufällig und gut verteilt sein. Weitere Informationen zur [vorgeschlagenen Benennungskonvention für Benutzer-IDs](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze Benutzer-ID] | Braze-Benutzerkennung. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzende über andere Dimensionen als Ihre Hauptbenutzer-ID zu identifizieren. <br><br> Das Alias-Objekt des Benutzers besteht aus zwei Teilen: einem alias_name für den Bezeichner selbst und einem alias_label, das den Alias-Typ angibt. Benutzer können mehrere Aliase mit unterschiedlichen Kennzeichnungen haben, aber nur einen Alias_Namen pro Alias_Label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis an einen Benutzer zu binden, müssen Sie entweder das Feld [!UICONTROL Externe Benutzer-ID] oder das Feld [!UICONTROL Braze-]) oder den Abschnitt [!UICONTROL Benutzeralias] ausfüllen.

**[!UICONTROL Ereignisdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Ereignisname &#x200B;] | Name des Ereignisses. | Ja |
| [!UICONTROL Ereigniszeit] | Datum-Uhrzeit als Zeichenfolge in ISO 8601 oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Ja |
| [!UICONTROL App-Kennung] | Die App-Kennung oder <strong>app_id</strong> ist ein Parameter, der die Aktivität einer bestimmten App in Ihrer App-Gruppe zuordnet. Es gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Weitere Informationen zu den [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Ereigniseigenschaften &#x200B;] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Für **[!UICONTROL Aktion &quot;]** senden“ müssen nur ein **[!UICONTROL Ereignisname]** und **[!UICONTROL Ereigniszeit]** angegeben werden. Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften aufnehmen. Einzelheiten zum [!DNL Braze] Ereignisobjekt finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, mit denen ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellt oder aktualisiert wird. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenketten: „M“, „F“, „O“ (andere), „N“ (nicht zutreffend), „P“ (bitte nicht sagen). |
| [!UICONTROL Stadt] | |
| [!UICONTROL Country] | Land als Zeichenfolge im [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)-Format. |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge im [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)Format. |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format „JJJJ-MM-TT“ (z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Name der Zeitzone aus [IANA-Zeitzonendatenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (z. B. &#39;America/New_York&#39; oder &#39;Eastern Time (US &amp; Kanada)&#39;). |
| [!UICONTROL Facebook] | Hash, der einen der Werte id (Zeichenfolge), likes (Zeichenfolgen-Array), num_friends (Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der einen der Werte id (Ganzzahl), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Ganzzahl), friends_count (Ganzzahl), statuses_count (Ganzzahl) enthält. |

{style="table-layout:auto"}

## Erstellen einer [!DNL Send Purchase Event] Regel {#purchase-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL Braze]**-Erweiterung aus und wählen Sie dann **[!UICONTROL Kaufereignis senden]** für den Aktionstyp aus.

![Fügen Sie eine Aktionskonfiguration für die Ereignisweiterleitungsregel vom Typ „Braze-Kauf“ hinzu.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Benutzeridentifizierung]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Externe Benutzer-ID] | Lange, zufällige und gut verteilte UUID oder GUID. Wenn Sie eine andere Methode zur Benennung Ihrer Benutzer-IDs auswählen, müssen diese auch lang, zufällig und gut verteilt sein. Weitere Informationen zur [vorgeschlagenen Benennungskonvention für Benutzer-IDs](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze Benutzer-ID] | Braze-Benutzerkennung. |
| [!UICONTROL Benutzeralias] | Ein Alias dient als alternative eindeutige Benutzerkennung. Verwenden Sie Aliase, um Benutzende über andere Dimensionen als Ihre Hauptbenutzer-ID zu identifizieren. <br><br> Das Alias-Objekt des Benutzers besteht aus zwei Teilen: einem alias_name für den Bezeichner selbst und einem alias_label, das den Alias-Typ angibt. Benutzer können mehrere Aliase mit unterschiedlichen Kennzeichnungen haben, aber nur einen Alias_Namen pro Alias_Label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Um das Ereignis mit einem Benutzer zu verknüpfen, müssen Sie entweder das Feld [!UICONTROL Externe Benutzer-ID], das Feld [!UICONTROL Braze-Benutzerkennung] oder den Abschnitt [!UICONTROL Benutzeralias] ausfüllen.

**[!UICONTROL Kaufdaten]**

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Produkt-ID &#x200B;] | Kennung für den Kauf. (z. B. Produktname oder Produktkategorie) | Ja |
| [!UICONTROL Kaufzeit] | Datum-Uhrzeit als Zeichenfolge in ISO 8601 oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Ja |
| [!UICONTROL &#x200B;] | Währung als Zeichenfolge im [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217) Alphabetisches Währungscodeformat. | Ja |
| [!UICONTROL Preis &#x200B;] | Preis. | Ja |
| [!UICONTROL &#x200B;] | Wenn kein Wert angegeben wird, ist der Standardwert 1. Der Höchstwert muss kleiner als 100 sein. | |
| [!UICONTROL App-Kennung] | Die App-Kennung oder <strong>app_id</strong> ist ein Parameter, der die Aktivität einer bestimmten App in Ihrer App-Gruppe zuordnet. Es gibt an, mit welcher App innerhalb der App-Gruppe Sie interagieren. Weitere Informationen zu den [API-Kennungstypen](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Kaufeigenschaften &#x200B;] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Kaufs. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Für **[!UICONTROL Aktion &quot;]** senden“ müssen nur ein **[!UICONTROL Ereignisname]** und **[!UICONTROL Ereigniszeit]** angegeben werden, Sie sollten jedoch so viele Informationen wie möglich in das Feld für benutzerdefinierte Eigenschaften aufnehmen. Einzelheiten zum [!DNL Braze] Ereignisobjekt finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Benutzerattribute]**

Benutzerattribute können ein JSON-Objekt sein, das Felder enthält, mit denen ein Attribut mit dem angegebenen Namen und Wert im angegebenen Benutzerprofil erstellt oder aktualisiert wird. Die folgenden Eigenschaften werden unterstützt:

| Benutzerattribut | Beschreibung |
| --- | --- |
| [!UICONTROL Vorname] | |
| [!UICONTROL Nachname] | |
| [!UICONTROL Phone] | |
| [!UICONTROL E-Mail] | |
| [!UICONTROL Geschlecht] | Eine der folgenden Zeichenketten: „M“, „F“, „O“ (andere), „N“ (nicht zutreffend), „P“ (bitte nicht sagen). |
| [!UICONTROL Stadt] | |
| [!UICONTROL Country] | Land als Zeichenfolge im [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)-Format. |
| [!UICONTROL Sprache] | Sprache als Zeichenfolge im [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)Format. |
| [!UICONTROL Geburtsdatum] | Zeichenfolge im Format „JJJJ-MM-TT“ (z. B. 1980-12-21). |
| [!UICONTROL Zeitzone] | Name der Zeitzone aus [IANA-Zeitzonendatenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (z. B. &#39;America/New_York&#39; oder &#39;Eastern Time (US &amp; Kanada)&#39;). |
| [!UICONTROL Facebook] | Hash, der einen der Werte id (Zeichenfolge), likes (Zeichenfolgen-Array), num_friends (Ganzzahl) enthält. |
| [!UICONTROL Twitter] | Hash, der einen der Werte id (Ganzzahl), screen_name (Zeichenfolge, Twitter-Handle), followers_count (Ganzzahl), friends_count (Ganzzahl), statuses_count (Ganzzahl) enthält. |

{style="table-layout:auto"}

## Validieren von Daten in [!DNL Braze] {#validate}

Wenn die Ereignissammlung und [!DNL Adobe Experience Platform] Integration erfolgreich waren, werden bei der Anzeige von Benutzerprofilen Ereignisse in der [!DNL Braze]-Konsole [angezeigt](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Insbesondere die neuen Ereignisdaten, die an [!DNL Braze] gesendet werden, werden im Abschnitt [!DNL Purchases] der Registerkarte [Übersicht“ eines bestimmten Benutzers ](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Braze] senden. Weitere Informationen zu nachgelagerten Anwendungen für Ereignisdaten, die an [!DNL Braze] gesendet werden, finden Sie in der [offiziellen Dokumentation](https://www.braze.com/docs).

Weitere Informationen zu den Ereignisweiterleitungsfunktionen in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
