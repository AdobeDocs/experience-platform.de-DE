---
title: Erstellen einer  [!DNL Oracle NetSuite Activities] -Quellverbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung für Oracle NetSuite-Aktivitäten erstellen.
exl-id: 99ef0b50-c8d6-48d6-895f-46b7ade47520
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 40%

---

# Erstellen eines Quell-Connectors für [!DNL Oracle NetSuite Activities] in der Benutzeroberfläche

Lesen Sie das folgende Tutorial, um zu erfahren, wie Sie Ereignisdaten aus Ihrem [!DNL Oracle NetSuite Activities]-Konto über die Benutzeroberfläche an Adobe Experience Platform übertragen.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Oracle NetSuite]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/marketing-automation.md) fortfahren.

>[!TIP]
>
>Informationen [[!DNL Oracle NetSuite]  Abrufen Ihrer Authentifizierungsdaten finden Sie ](../../../../connectors/marketing-automation/oracle-netsuite.md) „Übersicht“.

## Verbinden Ihres [!DNL Oracle NetSuite]-Kontos {#connect-account}

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *Kategorie* Marketing-Automatisierung“ die Option **[!DNL Oracle NetSuite Activities]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

![Screenshot der Experience Platform-Benutzeroberfläche für den Katalog mit der Karte &quot;Oracle NetSuite-Aktivitäten“](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

Die **[!UICONTROL Oracle NetSuite-Aktivitätskonto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!IMPORTANT]
>
>Das Aktualisierungstoken läuft nach sieben Tagen ab. Sobald Ihr Token abläuft, müssen Sie auf Experience Platform ein Konto mit Ihrem aktualisierten Token erstellen. Wenn Sie kein neues Konto mit Ihrem aktualisierten Token erstellen, wird möglicherweise die folgende Fehlermeldung angezeigt: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Vorhandenes Konto {#existing-account}

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle NetSuite Activities]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Screenshot der Experience Platform-Benutzeroberfläche zum Verbinden des Kontos &quot;Oracle NetSuite-Aktivitäten“ mit einem bestehenden Konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### Neues Konto {#new-account}

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Screenshot der Experience Platform-Benutzeroberfläche, um das Konto &quot;Oracle NetSuite-Aktivitäten“ mit einem neuen Konto zu verbinden](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## Nächste Schritte {#next-steps}

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Oracle NetSuite Activities]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/marketing-automation.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Oracle NetSuite Activities] verweisen können.

### Zuordnung {#mapping}

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Welche Felder angezeigt werden, hängt von den Abonnements ab, auf die Ihr [!DNL Oracle NetSuite]-Konto Zugriff hat. Wenn Sie beispielsweise keinen Zugriff auf die Fakturierung haben, werden die Felder für die Fakturierung nicht angezeigt.

### Planung {#scheduling}

Bei der Planung Ihres [!DNL Oracle NetSuite Activities] Datenflusses für die Aufnahme müssen Sie die folgende Häufigkeit und Intervallkonfiguration auswählen:

| Häufigkeit | Intervall |
| --- | --- |
| `Once` | 1 |

Beim Abrufen von Daten antwortet der [!DNL Oracle NetSuite] mit dem Datum der letzten Änderung oder Erstellung als Datumsformat anstelle eines Zeitstempels. Daher ist die Planung auf einen Tag beschränkt.

Nachdem Sie die Werte für Ihren Zeitplan angegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Planungsschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)
