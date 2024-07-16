---
title: Erstellen einer  [!DNL Oracle NetSuite Entities] -Quellverbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Oracle NetSuite Entities-Quellverbindung erstellen.
hide: true
hidefromtoc: true
badge: Beta
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 39%

---

# Erstellen eines Quell-Connectors für [!DNL Oracle NetSuite Entities] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Oracle NetSuite Entities]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

Lesen Sie das folgende Tutorial, um zu erfahren, wie Sie Kontakte und Kundendaten von Ihrem [!DNL Oracle NetSuite Entities]-Konto in der Benutzeroberfläche an Adobe Experience Platform übertragen können.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Oracle NetSuite]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/marketing-automation.md) fortfahren.

>[!TIP]
>
>Informationen zum Abrufen Ihrer Authentifizierungsberechtigungen finden Sie in der [[!DNL Oracle NetSuite] Übersicht](../../../../connectors/marketing-automation/oracle-netsuite.md) .

## Verbinden Ihres [!DNL Oracle NetSuite Activities]-Kontos {#connect-account}

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Marketing-Automatisierung* die Option **[!DNL Oracle NetSuite Entities]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Screenshot der Platform-Benutzeroberfläche für den Katalog mit der Oracle NetSuite-Entitätskarte](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

Die Seite **[!UICONTROL Oracle NetSuite Entitäten-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!IMPORTANT]
>
>Das Aktualisierungs-Token läuft nach sieben Tagen ab. Sobald Ihr Token abläuft, müssen Sie ein Konto auf dem Experience Platform mit Ihrem aktualisierten Token erstellen. Wenn Sie kein neues Konto mit Ihrem aktualisierten Token erstellen, wird möglicherweise die folgende Fehlermeldung angezeigt: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Vorhandenes Konto {#existing-account}

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle NetSuite Entities]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Screenshot der Platform-Benutzeroberfläche zum Verbinden des Oracle NetSuite-Entitätskontos mit einem vorhandenen Konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### Neues Konto {#new-account}

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Screenshot der Platform-Benutzeroberfläche zum Verbinden des Oracle NetSuite-Entitätskontos mit einem neuen Konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### Daten auswählen

Wählen Sie als Nächstes den Objekttyp aus, den Sie auf Experience Platform erfassen möchten.

| Entitätstyp | Beschreibung |
| --- | --- |
| Kontakt | Rufen Sie Kontaktnamen, E-Mails, Telefonnummern und alle benutzerdefinierten Kontaktfelder ab, die mit Kunden verknüpft sind. |
| Kundin bzw. Kunde | Rufen Sie bestimmte Kundendaten ab, einschließlich Details wie Kundennamen, Adressen und Schlüsselkennungen. |

>[!BEGINTABS]

>[!TAB Contact]

![Screenshot der Platform-Benutzeroberfläche für Oracle Netsuite-Entitäten mit ausgewählter Option Konfiguration mit Kontakt](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB Kunde]

![Screenshot der Platform-Benutzeroberfläche für Oracle Netsuite-Entitäten mit ausgewählter Option &quot;Konfiguration mit Kunden&quot;](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## Nächste Schritte {#next-steps}

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Oracle NetSuite Entities]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Daten zur Marketing-Automatisierung in Platform](../../dataflow/marketing-automation.md) zu importieren.

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Oracle NetSuite Entities]-Quelle verweisen können.

### Zuordnung {#mapping}

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Die angezeigten Felder hängen von den Abonnements ab, auf die Ihr [!DNL Oracle NetSuite]-Konto Zugriff hat. Wenn Sie beispielsweise keinen Zugriff auf die Rechnungsstellung haben, werden die entsprechenden Felder nicht angezeigt.

### Planung {#scheduling}

Bei der Planung Ihres [!DNL Oracle NetSuite Entities]-Datenflusses für die Aufnahme müssen Sie die folgende Häufigkeits- und Intervallkonfiguration auswählen:

| Häufigkeit | Intervall |
| --- | --- |
| `Once` | 1 |

Beim Abrufen der Daten antwortet der [!DNL Oracle NetSuite] mit dem zuletzt geänderten oder erstellten Datum als Datumsformat anstelle eines Zeitstempels. Daher ist die Planung auf einen Tag beschränkt.

Nachdem Sie die Werte für Ihren Zeitplan angegeben haben, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Planungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
