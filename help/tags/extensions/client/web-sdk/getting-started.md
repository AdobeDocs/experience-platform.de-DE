---
title: Erste Schritte mit der Tag-Erweiterung „Web SDK"
description: Senden von Ereignisdaten an Adobe Experience Platform Edge Network mithilfe der Tag-Erweiterung „Web SDK".
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 5%

---

# Erste Schritte mit der Tag-Erweiterung „Web SDK&quot;

Verwenden Sie die **Tags** von Adobe Experience Platform (früher Launch), um Ereignisdaten von Ihrer Website an Edge Network und nachgelagerte Adobe-Lösungen zu senden.

Bevor Sie diese Schritte ausführen, stellen Sie sicher, dass Sie auf die folgenden [Eigenschaftsrechte“ zugreifen &#x200B;](/help/tags/ui/administration/user-permissions.md):

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Stellen Sie außerdem sicher, dass Sie alle [Berechtigungen](/help/access-control/home.md#permissions) unter den folgenden Kategorien haben:

* Datenmodellierung
* Identitäten

## Erstellen eines XDM-Schemas {#schema}

Das [Experience-Datenmodell (XDM](/help/xdm/home.md) ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen für Daten in Form von Schemas bereitstellt. Beim Senden von Daten an die Edge Network wird dringend empfohlen, ein Schema zu konfigurieren.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Wählen Sie **[!UICONTROL Create schema]** aus.
1. Wählen Sie **[!UICONTROL Experience Event]** und dann **[!UICONTROL Next]** aus.
1. Geben Sie dem Schema einen gewünschten Namen und wählen Sie dann **[!UICONTROL Finish]** aus.
1. (Optional) Sie können weitere Felder oder [Feldergruppen](/help/xdm/ui/resources/field-groups.md) für alle zusätzlichen Daten hinzufügen, die Sie erfassen möchten.

![Arbeitsfläche des Schemas](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>Nach dem Speichern lassen Schemata nur *additive* Änderungen zu. Weitere Informationen finden [&#x200B; unter &#x200B;](/help/xdm/schema/composition.md#evolution)Schemaentwicklung“.

## Erstellen eines Datenspeichers {#datastream}

Ein [Datenstrom](/help/datastreams/overview.md) ist eine Konfiguration, die dem Edge Network mitteilt, wie die gesendeten Daten verarbeitet werden sollen. Wenn Sie einen Datenstrom so konfigurieren, dass Daten an ein bestimmtes Produkt gesendet werden, übergibt der Datenstrom relevante Daten automatisch auf eine Weise an jedes jeweilige Produkt, die das jeweilige Produkt versteht.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Wählen Sie **[!UICONTROL New datastream]** aus.
1. Benennen Sie den Datenstrom und wählen Sie das kürzlich erstellte Schema unter **[!UICONTROL Mapping schema]** aus.
1. Wählen Sie **[!UICONTROL Save]** aus.

![Liste der Datenströme](assets/getting-started/datastreams.png)

## Erstellen einer Tag-Eigenschaft

Nachdem Sie ein Schema und einen Datenstrom erstellt haben, können Sie eine Tag-Eigenschaft erstellen und konfigurieren.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie **[!UICONTROL New property]** aus.
1. Geben Sie der Tag-Eigenschaft den gewünschten Namen und die gewünschte Domain und wählen Sie dann **[!UICONTROL Save]** aus.

## Installieren der Tag-Erweiterung

Die Web SDK-Tag-Erweiterung wird in einer bestimmten Tag-Eigenschaft installiert.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Wählen Sie die Registerkarte **[!UICONTROL Catalog]** aus.
1. Verwenden Sie die Suche, um die **[!UICONTROL Adobe Experience Platform Web SDK]**-Erweiterung zu finden.
1. Klicken Sie auf die Erweiterungskarte und dann auf der rechten Seite auf **[!UICONTROL Install]** .

![Installieren von SDK](assets/getting-started/install-sdk.png)

## Konfigurieren der Tag-Erweiterung

Wenn Sie die Tag-Erweiterung „Web SDK&quot; installieren, werden Sie automatisch zur Seite [Konfiguration](configure/config-overview.md) weitergeleitet.

1. Wählen [&#x200B; im Abschnitt &#x200B;](configure/datastreams.md) den gewünschten Datenstrom für jede Umgebung aus.

Alle anderen Konfigurationseinstellungen sind entweder für Sie ausgefüllt oder optional. Legen Sie die gewünschten Konfigurationseinstellungen fest und klicken Sie dann auf **[!UICONTROL Save]**.

## Erstellen eines variablen Datenelements

Adobe empfiehlt die Verwendung von [Variable](data-element-types.md#variable)-Datenelementen zum Speichern der Payload, die Sie an Adobe senden möchten. XDM-Objekte sind ebenfalls verfügbare Datenelemente, sind jedoch in Anwendungsfällen älter und eingeschränkter.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Wählen Sie **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]** aus.
1. Weisen Sie dem Datenelement links die folgenden Eigenschaften zu:
   * **[!UICONTROL Name]**: Beliebiger Name
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Legen Sie die folgenden Eigenschaften auf der rechten Seite fest:
   **Variablentyp**: XDM
   **[!UICONTROL Sandbox]**: Die Sandbox, in der Sie Ihr Schema erstellt haben
   **[!UICONTROL Schema]**: Das gewünschte Schema
1. Wählen Sie **[!UICONTROL Save]** aus.

## Erstellen einer Regel

Regeln bestimmen, wann Sie einen Trigger vornehmen oder Variablen festlegen möchten. Durch das Erstellen einer Regel, die immer dann ausgeführt wird, wenn die Bibliothek geladen wird, können Sie auf jeder Seite einfach Variablen ausfüllen, die einen Wert enthalten sollen.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Wählen Sie **[!UICONTROL Rules]** > **[!UICONTROL Add rule]** aus.
1. Geben Sie der Regel einen gewünschten Namen.
1. Klicken Sie auf das Symbol &quot;`+`&quot; neben **[!UICONTROL Events]**.
1. Geben Sie dem Ereignis die folgenden Einstellungen:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Wählen Sie **[!UICONTROL Keep changes]** aus.

Mit den oben genannten Schritten wird der Kriterienteil der Regel festgelegt, der nach dem Laden der Bibliothek in den Trigger aufgenommen wird. Mit den folgenden Schritten wird festgelegt, welche Maßnahmen zu ergreifen sind, wenn diese Kriterien erfüllt sind.

1. Klicken Sie auf das Symbol &quot;`+`&quot; neben **[!UICONTROL Actions]**.
1. Geben Sie der Aktion auf der linken Seite die folgenden Einstellungen:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Legen Sie die folgenden Felder rechts fest:
   * **[!UICONTROL XDM]**: Das XDM-Variablendatenelement
1. Wählen Sie **[!UICONTROL Keep changes]** aus.

![Aktionskonfiguration](assets/getting-started/action-config.png)

## Veröffentlichen

Die Tag-Eigenschaft enthält alle Komponenten, die zum Senden von Daten an Edge Network erforderlich sind.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Wählen Sie **[!UICONTROL Add library]** aus.
1. Geben Sie der Bibliothek einen gewünschten Namen. Betrachten Sie diesen Namen als ähnlich wie einen Commit-Namen, wenn Sie mit Versionskontrollsoftware arbeiten.
1. Stellen Sie das Dropdown-Menü Umgebung auf **[!UICONTROL Development]** ein.
1. Wählen Sie **[!UICONTROL Add all changed resources]** aus.
1. Wählen Sie **[!UICONTROL Save & build to Development]** aus.

Ihre Änderungen werden jetzt in Ihrer Entwicklungsumgebung bereitgestellt.

1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Wählen Sie das Installationssymbol neben der Entwicklungsumgebung aus
1. Installieren Sie den Einbettungs-Code innerhalb einer Test-Web-Seite auf Ihrer Site.

Nachdem Sie überprüft haben, ob das Tag in Ihrer Entwicklungsumgebung funktioniert, können Sie über die [!UICONTROL Publishing flow] die Bibliothek in der Staging- und schließlich in der Produktionsumgebung veröffentlichen.

1. Fügen Sie die Erweiterung und die Regel einer **Bibliothek** hinzu, erstellen Sie sie in einer **Umgebung** und installieren Sie den Einbettungs-Code auf Ihrer Site.
2. Validieren mit **Adobe Experience Platform Debugger**.

Sie verfügen jetzt über eine schlanke Einrichtung, die Ereignisse erfasst und an die Edge Network sendet. Sie können Ihre Implementierung jetzt weiter aufbauen, indem Sie Ihrem Schema Felder hinzufügen, Produkte zu einem Datenstrom hinzufügen oder Datenelemente zu Ihrer Tag-Eigenschaft hinzufügen.
