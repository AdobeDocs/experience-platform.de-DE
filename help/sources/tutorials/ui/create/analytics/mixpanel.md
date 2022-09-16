---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: (Beta) Erstellen einer Mixpanel-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie eine Quellverbindung für Mixpanel mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: bee13becb59e3277921549e6db027ce864bba28b
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 34%

---

# (Beta) Erstellen Sie eine [!DNL Mixpanel] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Mixpanel] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Mixpanel] Quellverbindung über die Benutzeroberfläche von Adobe Experience Platform Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL Mixpanel] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Benutzername | Der Benutzername des Dienstkontos, der Ihrer [!DNL Mixpanel] -Konto. Siehe [[!DNL Mixpanel] Dokumentation zu Dienstkonten](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) für weitere Informationen. | `Test8.6d4ee7.mp-service-account` |
| Passwort | Das Dienstkontokennwort, das Ihrer [!DNL Mixpanel] -Konto. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| Projekt-ID | Ihre [!DNL Mixpanel] Projekt-ID. Diese ID ist erforderlich, um eine Quellverbindung zu erstellen. Siehe [[!DNL Mixpanel] Dokumentation zu den Projekteinstellungen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) und [[!DNL Mixpanel] Handbuch zum Erstellen und Verwalten von Projekten](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) für weitere Informationen. | `2384945` |
| Zeitzone | Die Zeitzone, die Ihrer [!DNL Mixpanel] Projekt. Zum Erstellen einer Quellverbindung ist eine Zeitzone erforderlich. Siehe [Dokumentation zu den Projekteinstellungen in Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) für weitere Informationen. | `Pacific Standard Time` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Mixpanel] -Quelle, siehe [[!DNL Mixpanel] Quellübersicht](../../../../connectors/analytics/mixpanel.md).

## Verbinden Ihres [!DNL Mixpanel]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *Analytics* category, select [!DNL Mixpanel]und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Die **[!UICONTROL Mixpanel-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Mixpanel]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Projekt-ID und Zeitzone auswählen {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Zeitzone für die Mixpanel-Erfassung festlegen"
>abstract="Die Zeitzone muss mit der Zeitzone Ihres Mixpanel-Profils übereinstimmen, da Platform die dafür vorgesehene Zeitzone des Projekts verwendet, um relevante Daten aus Mixpanel zu erfassen. Mixpanel passt seine Zeitzone an die Koordination mit Ihrer Projekt-Zeitzone an, bevor das Ereignis in einem Mixpanel-Datenspeicher aufgezeichnet wird."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=en#project-id-and-timezone" text="Weitere Informationen finden Sie in der Dokumentation"

Geben Sie nach der Authentifizierung Ihrer Quelle Ihre Projekt-ID und Zeitzone ein und wählen Sie **[!UICONTROL Auswählen]**.

Die Zeitzone, die Sie vor der Aufnahme Ihrer [!DNL Mixpanel] -Daten in Platform müssen mit den Daten in Ihrer [!DNL Mixpanel] Zeitzone des Profils. Änderungen an der Zeitzone Ihrer Daten werden nur auf neue Ereignisse angewendet und alte Ereignisse bleiben in der zuvor festgelegten Zeitzone. [!DNL Mixpanel] berücksichtigt die Sommerzeit und passt den Zeitstempel der Aufnahme entsprechend an. Weitere Informationen dazu, wie Zeitzonen Ihre Daten beeinflussen, finden Sie unter [!DNL Mixpanel] Handbuch zu [Zeitzonen für Projekte verwalten](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Nach einigen Augenblicken wird die richtige Oberfläche in ein Vorschaufenster aktualisiert, sodass Sie Ihr Schema vor der Erstellung eines Datenflusses überprüfen können. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Konfiguration](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Mixpanel]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Analysedaten in Platform zu importieren](../../dataflow/analytics.md).

## Weitere Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei der Verwendung der Variablen [!DNL Mixpanel] -Quelle.

### Validierung {#validation}

In den folgenden Schritten wird beschrieben, wie Sie überprüfen können, ob Sie Ihre [!DNL Mixpanel] und [!DNL Mixpanel] -Ereignisse in Platform erfasst werden.

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Datensätze]** über die linke Navigationsleiste, um auf die [!UICONTROL Datensätze] Arbeitsbereich. Die [!UICONTROL Datensatzaktivität] zeigt die Details der Ausführungen an.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Wählen Sie anschließend die Datenfluss-Start-ID des Datenflusses aus, den Sie anzeigen möchten, um bestimmte Details zu diesem Datenfluss anzuzeigen.

![dataflow-monitoring](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Vorschau des Datensatzes anzeigen]** , um die erfassten Daten anzuzeigen.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Sie können diese Daten anhand der Daten auf der [!DNL Mixpanel] > [!DNL Events] Seite. Siehe [[!DNL Mixpanel] Dokument zu Ereignissen](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) für weitere Informationen.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für [!DNL Mixpanel].

>[!TIP]
>
>Siehe [Ereignis-Export-API > Download](https://developer.mixpanel.com/reference/raw-event-export) für weitere Informationen zur API.


| Quelle | Typ |
|---|---|
| `distinct_id` | string |
| `event_name` | Zeichenfolge |
| `import` | boolean |
| `insert_id` | Zeichenfolge |
| `item_id` | Zeichenfolge |
| `item_name` | Zeichenfolge |
| `item_price` | Zeichenfolge |
| `mp_api_endpoint` | Zeichenfolge |
| `mp_api_timestamp_ms` | integer |
| `mp_processing_time_ms` | integer |
| `time` | integer |

### Beschränkungen {#limits}

* Sie haben maximal 100 gleichzeitige Abfragen und 60 Abfragen pro Stunde, wie in [API-Ratenbeschränkungen exportieren](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
