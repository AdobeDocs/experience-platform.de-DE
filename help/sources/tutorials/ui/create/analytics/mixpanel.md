---
title: Erstellen einer Source-Verbindung aus dem Mixpanel in der Benutzeroberfläche
description: Erfahren Sie, wie Sie eine Quellverbindung für Mixpanel mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 40%

---

# Erstellen eines Quell-Connectors für [!DNL Mixpanel] in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen einer 0-Quell-Verbindung mithilfe der Benutzeroberfläche von Adobe Experience Platform Platform beschrieben.[!DNL Mixpanel]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL Mixpanel] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Benutzername | Der Benutzername des Dienstkontos, der Ihrem [!DNL Mixpanel] -Konto entspricht. Weitere Informationen finden Sie in der Dokumentation zu [[!DNL Mixpanel] Dienstkonten](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) . | `Test8.6d4ee7.mp-service-account` |
| Kennwort | Das Dienstkontokennwort, das Ihrem [!DNL Mixpanel] -Konto entspricht. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| Projekt-ID | Ihre [!DNL Mixpanel] Projekt-ID. Diese ID ist erforderlich, um eine Quellverbindung zu erstellen. Weitere Informationen finden Sie in der Dokumentation zu den [[!DNL Mixpanel] Projekteinstellungen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) und im [[!DNL Mixpanel] Handbuch zum Erstellen und Verwalten von Projekten](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) . | `2384945` |
| Zeitzone | Die Zeitzone, die Ihrem [!DNL Mixpanel] -Projekt entspricht. Zum Erstellen einer Quellverbindung ist eine Zeitzone erforderlich. Weitere Informationen finden Sie in der Dokumentation zu den [Projekteinstellungen für Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) . | `Pacific Standard Time` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Mixpanel]-Quelle finden Sie in der [[!DNL Mixpanel] Quellübersicht](../../../../connectors/analytics/mixpanel.md).

## Verbinden Ihres [!DNL Mixpanel]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Analytics* die Option [!DNL Mixpanel] und dann **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Die Seite **[!UICONTROL Mixpanel-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Mixpanel]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Auswählen Ihrer Projekt-ID und Zeitzone {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Festlegen der Zeitzone für die Mixpanel-Aufnahme"
>abstract="Die Zeitzone muss mit der Zeitzone Ihres Mixpanel-Profils übereinstimmen, da Platform die angegebene Projektzeitzone verwendet, um von Mixpanel relevante Daten aufzunehmen. Mixpanel passt seine Zeitzone an Ihre Projekt-Zeitzone an, bevor das Ereignis in einem Mixpanel-Datenspeicher festgehalten wird."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=de#project-id-and-timezone" text="Weitere Informationen finden Sie in der Dokumentation"

Geben Sie nach der Authentifizierung Ihrer Quelle Ihre Projekt-ID und Zeitzone ein und wählen Sie dann **[!UICONTROL Auswählen]** aus.

Die Zeitzone, die Sie vor der Aufnahme Ihrer [!DNL Mixpanel] -Daten in Platform festlegen, muss mit der Zeitzone Ihres [!DNL Mixpanel]-Profils übereinstimmen. Änderungen an der Zeitzone Ihrer Daten werden nur auf neue Ereignisse angewendet und alte Ereignisse bleiben in der zuvor festgelegten Zeitzone. [!DNL Mixpanel] berücksichtigt die Sommerzeit und passt den Zeitstempel der Aufnahme entsprechend an. Weitere Informationen dazu, wie Zeitzonen Ihre Daten beeinflussen, finden Sie im [!DNL Mixpanel]-Handbuch unter [Verwalten von Zeitzonen für Projekte](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Nach einigen Augenblicken wird die richtige Oberfläche in ein Vorschaufenster aktualisiert, sodass Sie Ihr Schema vor der Erstellung eines Datenflusses überprüfen können. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![configuration](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Mixpanel]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Analysedaten in Platform](../../dataflow/analytics.md) zu importieren.

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der Quelle [!DNL Mixpanel] verweisen können.

### Validierung {#validation}

Im Folgenden werden die Schritte beschrieben, die Sie ausführen können, um zu überprüfen, ob Sie Ihre [!DNL Mixpanel] -Quelle erfolgreich verbunden haben und ob [!DNL Mixpanel] -Ereignisse in Platform aufgenommen werden.

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste **[!UICONTROL Datensätze]** aus, um auf den Arbeitsbereich [!UICONTROL Datensätze] zuzugreifen. Im Bildschirm [!UICONTROL Datensatzaktivität] werden die Details der Ausführungen angezeigt.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Wählen Sie anschließend die Datenfluss-Start-ID des Datenflusses aus, den Sie anzeigen möchten, um bestimmte Details zu diesem Datenfluss anzuzeigen.

![dataflow-monitoring](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Vorschau des Datensatzes anzeigen]** aus, um die erfassten Daten anzuzeigen.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Sie können diese Daten anhand der Daten auf der Seite [!DNL Mixpanel] > [!DNL Events] überprüfen. Weitere Informationen finden Sie im Dokument [[!DNL Mixpanel] für Ereignisse](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) .

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für [!DNL Mixpanel] eingerichtet werden müssen.

>[!TIP]
>
>Weitere Informationen zur API finden Sie unter [Ereignis-Export-API > Download](https://developer.mixpanel.com/reference/raw-event-export) .


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

* Sie haben maximal 100 gleichzeitige Abfragen und 60 Abfragen pro Stunde, wie unter [API-Ratenbeschränkungen exportieren](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints) angegeben.
