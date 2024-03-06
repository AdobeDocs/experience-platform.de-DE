---
title: Erstellen eines Datenflusses für Braze-Daten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche einen Datenfluss für Ihr Braze-Konto erstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: bfcea2a30a0ecadcafaddf7660eef90952dcade6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 23%

---

# Erstellen eines Quell-Connectors für [!DNL Braze Currents] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen von der Braze-Plattform, die den robusten, aber granularsten Export aus der [!DNL Braze] Plattform.

Lesen Sie das folgende Tutorial , um zu erfahren, wie Sie Interaktionsereignisdaten aus Ihrem [!DNL Braze] -Konto in der -Benutzeroberfläche zu Adobe Experience Platform hinzufügen.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie:

* Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und Berechtigung zum Erstellen einer neuen Streaming-Quell-Verbindung.
* Melden Sie sich bei Ihrer [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in)nicht verwendete [Aktuelle Connector-Lizenz](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie im Abschnitt [Anforderungen für die Einrichtung [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Dieses Tutorial setzt auch ein grundlegendes Verständnis der [[!DNL Braze] Aktuelles](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Wenn Sie bereits über eine [!DNL Braze] Verbindung nutzen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/marketing-automation.md).

## Verbinden Sie [!DNL Braze] Experience Platform

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *Marketing-Automatisierung* category, select **[!UICONTROL Blitze Ströme]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter Quelle Aktuelles reduzieren .](../../../../images/tutorials/create/braze/catalog.png)

Laden Sie als Nächstes die bereitgestellte [Beispiel-Datei &quot;Braze Currency&quot;](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Diese Datei enthält alle möglichen Felder, die Braze im Rahmen eines Ereignisses senden kann.

![Der Bildschirm &quot;Daten hinzufügen&quot;.](../../../../images/tutorials/create/braze/select-data.png)

Nach dem Hochladen Ihrer Datei müssen Sie Ihre Datenflussdetails angeben, einschließlich Informationen zu Ihrem Datensatz und dem Schema, dem Sie zuordnen.
![Der Bildschirm &quot;Datenflussdetails&quot;zeigt &quot;Datensatzdetails&quot;an.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Konfigurieren Sie dann die Zuordnung für Ihre Daten über die Zuordnungsschnittstelle.

![Der Bildschirm &quot;Zuordnung&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Zeitstempel mit Braze werden nicht in Millisekunden, sondern in Sekunden ausgedrückt. Damit die Zeitstempel in Experience Platform korrekt dargestellt werden können, müssen berechnete Felder in Millisekunden erstellt werden. Eine Berechnung von &quot;Zeit * 1000&quot;wird ordnungsgemäß in Millisekunden konvertiert, die für die Zuordnung zu einem Zeitstempelfeld innerhalb von Experience Platform geeignet sind.
>
>![Berechnetes Feld für Zeitstempel erstellen ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Sammeln erforderlicher Anmeldeinformationen

Nachdem die Verbindung erstellt wurde, müssen Sie die folgenden Anmeldewerte erfassen, die Sie dann im Dashboard &quot;Braze&quot;bereitstellen, um Daten an Experience Platform zu senden. Weitere Informationen finden Sie im Abschnitt [!DNL Braze] [Handbuch zum Navigieren zu aktuellen Elementen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die Client-ID, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Client-Geheimnis | Das Client-Geheimnis, das mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Mandanten-ID | Die Mandantenkennung, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Dataflow-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der Streaming-Endpunkt, der Ihrer Experience Platform-Quelle zugeordnet ist. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

### Konfigurieren [!DNL Braze Currents] , um Daten an Ihre Datenquelle zu streamen

Innerhalb der [!DNL Braze Dashboard], navigieren Sie zu Partnerintegrationen . **->** Datenexport und wählen Sie **[!DNL Create New Current]**. Sie werden aufgefordert, einen Namen für den Connector, Kontaktinformationen für Benachrichtigungen über den Connector und die oben aufgeführten Anmeldeinformationen anzugeben. Wählen Sie die Ereignisse aus, die Sie empfangen möchten, konfigurieren Sie optional alle gewünschten Feldausschlüsse/-transformationen und wählen Sie dann **[!DNL Launch Current]**.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Braze]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus dem Marketing-Automatisierungssystem in [!DNL Platform]](../../dataflow/marketing-automation.md).