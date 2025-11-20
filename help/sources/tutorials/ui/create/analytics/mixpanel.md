---
title: Erstellen einer Mixpanel-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Mixpanel-Quellverbindung erstellen.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 30%

---

# Erstellen eines Quell-Connectors für [!DNL Mixpanel] in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Mixpanel]-Quellverbindung mithilfe der Benutzeroberfläche von Adobe Experience Platform Experience Platform beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Mixpanel] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Benutzername | Der Benutzername des Service-Kontos, der Ihrem [!DNL Mixpanel] entspricht. Weitere Informationen finden [[!DNL Mixpanel]  in der ](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) zu Service-Konten . | `Test8.6d4ee7.mp-service-account` |
| Passwort | Das Passwort des Service-Kontos, das Ihrem [!DNL Mixpanel]-Konto entspricht. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| Projekt-ID | Ihre [!DNL Mixpanel]-Projekt-ID. Diese ID ist erforderlich, um eine Quellverbindung zu erstellen. Weitere Informationen finden [[!DNL Mixpanel]  in der ](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) zu Projekteinstellungen und [[!DNL Mixpanel] Handbuch ](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) Erstellen und Verwalten von Projekten). | `2384945` |
| Zeitzone | Die Zeitzone, die Ihrem [!DNL Mixpanel] Projekt entspricht. Die Zeitzone ist erforderlich, um eine Quellverbindung zu erstellen. Weitere Informationen finden [ in der Dokumentation ](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) Mixpanel-Projekteinstellungen . | `Pacific Standard Time` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Mixpanel] finden Sie unter [[!DNL Mixpanel] Quelle - Übersicht](../../../../connectors/analytics/mixpanel.md).

## Verbinden Ihres [!DNL Mixpanel]-Kontos

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste **[!UICONTROL Sources]** aus, um auf den [!UICONTROL Sources]-Arbeitsbereich zuzugreifen. Der Bildschirm [!UICONTROL Catalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *Kategorie* Analytics“ die Option [!DNL Mixpanel] und dann **[!UICONTROL Add data]** aus.

![Katalog](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Die Seite **[!UICONTROL Connect Mixpanel account]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Mixpanel] Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Next]** , um fortzufahren.

![vorhanden](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL New account]** aus und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Connect to source]** aus und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Auswählen Ihrer Projekt-ID und Zeitzone {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Festlegen der Zeitzone für die Mixpanel-Aufnahme"
>abstract="Die Zeitzone muss mit der Zeitzone Ihres Mixpanel-Profils übereinstimmen, da Experience Platform die angegebene Projektzeitzone verwendet, um von Mixpanel relevante Daten aufzunehmen. Mixpanel passt seine Zeitzone an Ihre Projekt-Zeitzone an, bevor das Ereignis in einem Mixpanel-Datenspeicher festgehalten wird."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=de#project-id-and-timezone" text="Weitere Informationen finden Sie in der Dokumentation"

Geben Sie nach der Authentifizierung Ihrer Quelle Ihre Projekt-ID und Zeitzone an und wählen Sie dann **[!UICONTROL Select]** aus.

Die Zeitzone, die Sie vor der Aufnahme Ihrer [!DNL Mixpanel] in Experience Platform festlegen, muss mit der Zeitzoneneinstellung Ihres [!DNL Mixpanel] Profils übereinstimmen. Alle Änderungen an der Zeitzone Ihrer Daten werden nur auf neue Ereignisse angewendet, und alte Ereignisse verbleiben in der Zeitzone, die Sie zuvor festgelegt haben. [!DNL Mixpanel] berücksichtigt die Sommerzeit und passt Ihren Aufnahmezeitstempel entsprechend an. Weitere Informationen dazu, wie sich Zeitzonen auf Ihre Daten auswirken, finden Sie im [!DNL Mixpanel] Handbuch unter [Verwalten von Zeitzonen für Projekte](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Nach einigen Augenblicken wird die rechte Benutzeroberfläche in ein Vorschaufenster aktualisiert, sodass Sie Ihr Schema überprüfen können, bevor Sie einen Datenfluss erstellen. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Next]** aus.

![Konfiguration](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Mixpanel]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Analysedaten in Experience Platform zu importieren](../../dataflow/analytics.md).

## Weitere Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Mixpanel] verweisen können.

### Validierung {#validation}

Im Folgenden werden die Schritte beschrieben, die Sie unternehmen können, um zu überprüfen, ob Sie Ihre [!DNL Mixpanel] erfolgreich verbunden haben und ob [!DNL Mixpanel] Ereignisse in Experience Platform aufgenommen werden.

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste **[!UICONTROL Datasets]** aus, um auf den [!UICONTROL Datasets]-Arbeitsbereich zuzugreifen. Der [!UICONTROL Dataset Activity] zeigt die Details der Ausführungen an.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Wählen Sie als Nächstes die Datenflussausführungs-ID des Datenflusses aus, den Sie anzeigen möchten, um spezifische Details zu dieser Datenflussausführung anzuzeigen.

![Datenflussüberwachung](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Preview dataset]** aus, um die aufgenommenen Daten anzuzeigen.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Sie können diese Daten mit den Daten auf der Seite [!DNL Mixpanel] > [!DNL Events] vergleichen. Weitere Informationen finden [[!DNL Mixpanel]  im ](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) zu Ereignissen .

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für [!DNL Mixpanel] eingerichtet werden müssen.

>[!TIP]
>
>Weitere [ zur API finden Sie unter ](https://developer.mixpanel.com/reference/raw-event-export)Ereignisexport-API > Herunterladen“.


| Quelle | Typ |
|---|---|
| `distinct_id` | string |
| `event_name` | string |
| `import` | boolean |
| `insert_id` | string |
| `item_id` | string |
| `item_name` | string |
| `item_price` | string |
| `mp_api_endpoint` | string |
| `mp_api_timestamp_ms` | integer |
| `mp_processing_time_ms` | integer |
| `time` | integer |

### Beschränkungen {#limits}

* Sie haben maximal 100 gleichzeitige Abfragen und 60 Abfragen pro Stunde, wie unter [Export API Rate Limits](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints) angegeben.
