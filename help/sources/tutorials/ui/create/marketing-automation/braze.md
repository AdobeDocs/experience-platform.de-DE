---
title: Erstellen eines Datenflusses für Braze-Daten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche einen Datenfluss für Ihr Braze-Konto erstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 59600165328181e41750b9b2a1f4fbf162dd1df5
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 17%

---

# Erstellen eines Quell-Connectors für [!DNL Braze Currents] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“.

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen von der Braze-Plattform, der der robusteste und zugleich granularste Export aus der [!DNL Braze]-Plattform ist.

Lesen Sie das folgende Tutorial, um zu erfahren, wie Sie Interaktionsereignisdaten aus Ihrem [!DNL Braze]-Konto über die Benutzeroberfläche an Adobe Experience Platform übertragen.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie Folgendes:

* Eine Anmeldung bei [Adobe Experience Platform ](https://platform.adobe.com) die Berechtigung zum Erstellen einer neuen Streaming-Quellverbindung.
* Eine Anmeldung bei Ihrem [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in), eine nicht verwendete [Aktuelle Connector-](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)) und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie unter [Voraussetzungen für die Einrichtung [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Dieses Tutorial erfordert auch ein Grundverständnis von [[!DNL Braze] Strömungen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Wenn Sie bereits über eine [!DNL Braze] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses ](../../dataflow/marketing-automation.md).

## Erstellen eines XDM-Schemas

>[!TIP]
>
>Sie müssen ein Experience-Datenmodell-Schema (XDM) erstellen, wenn Sie zum ersten Mal eine [!DNL Braze Currents] Verbindung erstellen. Wenn Sie bereits ein Schema für [!DNL Braze Currents] erstellt haben, können Sie diesen Schritt überspringen und mit dem Schritt &quot;[ Ihres Kontos mit Experience Platform verbinden](#connect) fortfahren.

Verwenden Sie in der Platform-Benutzeroberfläche die linke Navigation und wählen Sie dann **[!UICONTROL Schemata]** aus, um auf den Arbeitsbereich [!UICONTROL Schemata] zuzugreifen. Wählen Sie anschließend **[!UICONTROL Schema erstellen]** und dann **[!UICONTROL Erlebnisereignis]** aus. Um fortzufahren, klicken Sie auf **[!UICONTROL Weiter]**.

![Ein abgeschlossenes Schema.](../../../../images/tutorials/create/braze/schema.png)

Geben Sie einen Namen und eine Beschreibung für Ihr Schema an. Verwenden Sie dann das Bedienfeld [!UICONTROL Komposition], um Ihre Schemaattribute zu konfigurieren. Wählen [!UICONTROL  unter ]Feldergruppen“ die Option **[!UICONTROL Hinzufügen]** aus und fügen Sie die Feldergruppe [!UICONTROL Benutzerereignis „Braze-]&quot; hinzu. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

Weitere Informationen zu Schemata finden Sie im Handbuch zu [Erstellen von Schemata in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md).

## Verbinden Ihres [!DNL Braze] mit Experience Platform {#connect}

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Marketing* die Option **[!UICONTROL Braze-Ströme]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Quelle für Braze-Ströme.](../../../../images/tutorials/create/braze/catalog.png)

Laden Sie als Nächstes die bereitgestellte Beispieldatei [Braze-Ströme“ ](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Diese Datei enthält alle möglichen Felder, die Braze im Rahmen eines Ereignisses senden könnte.

![Der Bildschirm „Daten hinzufügen“.](../../../../images/tutorials/create/braze/select-data.png)

Nach dem Hochladen der Datei müssen Sie Ihre Datenflussdetails angeben, einschließlich Informationen zu Ihrem Datensatz und dem Schema, dem Sie zuordnen.  Wenn dies das erste Mal ist, dass Sie eine Braze-Stromquelle verbinden, erstellen Sie einen neuen Datensatz.  Andernfalls können Sie einen beliebigen vorhandenen Datensatz verwenden, der auf das Braze-Schema verweist.  Wenn Sie einen neuen Datensatz erstellen, verwenden Sie das Schema , das wir im vorherigen Abschnitt erstellt haben.
![ Bildschirm „Datenflussdetails“ mit hervorgehobener Option „Datensatzdetails“](../../../../images/tutorials/create/braze/dataflow-detail.png)

Konfigurieren Sie dann die Zuordnung für Ihre Daten mithilfe der Zuordnungsschnittstelle.

![Der Bildschirm „Zuordnung“.](../../../../images/tutorials/create/braze/mapping_errors.png)

Die Zuordnung weist die folgenden Probleme auf, die gelöst werden müssen.

In den Quelldaten wird *id* fälschlicherweise *_braze.appID* zugeordnet. Sie müssen das Zielgruppen-Mapping-Feld auf der *des Schemas in*_id ändern. Stellen Sie als Nächstes sicher *dass &quot;.is_amp*&quot; *_braze.messaging.email.isAMP* zugeordnet ist.

Löschen Sie als Nächstes die Zuordnung *Zeit* zu *Zeitstempel*, klicken Sie dann auf das Symbol „Hinzufügen (`+`)“ und wählen Sie **[!UICONTROL Berechnetes Feld hinzufügen]**. Geben Sie in das bereitgestellte Feld *time \* 1000* ein und wählen Sie **[!UICONTROL Speichern]**.

Nachdem das neue berechnete Feld hinzugefügt wurde, wählen Sie **[!UICONTROL Zielfeld zuordnen]** neben dem neuen Quellfeld aus und ordnen Sie es *Zeitstempel* auf der Stammebene des Schemas zu. Wählen Sie dann **[!UICONTROL Validieren]** aus, um sicherzustellen, dass Sie keine Fehler mehr haben.

>[!IMPORTANT]
>
>Braze-Zeitstempel werden nicht in Millisekunden, sondern in Sekunden ausgedrückt. Damit die Zeitstempel im Experience Platform genau wiedergegeben werden, müssen Sie berechnete Felder in Millisekunden erstellen. Eine Berechnung von „time * 1000“ wird korrekt in Millisekunden konvertiert, passend für die Zuordnung zu einem Zeitstempelfeld innerhalb von Experience Platform.
>
>![Erstellen eines berechneten Felds für Zeitstempel ](../../../../images/tutorials/create/braze/create-calculated-field.png)

![Die Zuordnung ohne Fehler.](../../../../images/tutorials/create/braze/completed_mapping.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus. Bestätigen Sie auf der Seite Überprüfen die Details Ihres Datenflusses und wählen Sie dann **[!UICONTROL Beenden]**.

### Sammeln erforderlicher Anmeldedaten

Nachdem Ihre Verbindung erstellt wurde, müssen Sie die folgenden Werte für die Anmeldeinformationen erfassen, die Sie dann im Braze-Dashboard angeben, um Daten an Experience Platform zu senden. Weitere Informationen finden Sie im [!DNL Braze] ([ zum Navigieren zu Strömen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Client-ID. |
| Client-Geheimnis | Das mit Ihrer Experience Platform-Quelle verknüpfte Client-Geheimnis. |
| Mandanten-ID | Die Mandanten-ID, die mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Datenfluss-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der mit Ihrer Experience Platform-Quelle verknüpfte Streaming-Endpunkt. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

### Konfigurieren von [!DNL Braze Currents] zum Streamen von Daten an Ihre Datenquelle

Navigieren Sie in der [!DNL Braze Dashboard] zu Partnerintegrationen **->Datenexport** und klicken Sie dann auf **[!DNL Create New Current]**. Sie werden aufgefordert, einen Namen für den Connector, Kontaktinformationen für Benachrichtigungen über den Connector und die oben aufgeführten Anmeldeinformationen anzugeben. Wählen Sie die Ereignisse aus, die Sie empfangen möchten, konfigurieren Sie optional die gewünschten Feldausschlüsse/-transformationen und wählen Sie dann **[!DNL Launch Current]** aus.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Braze]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten zur Marketing-Automatisierung in zu importieren [!DNL Platform]](../../dataflow/marketing-automation.md).
