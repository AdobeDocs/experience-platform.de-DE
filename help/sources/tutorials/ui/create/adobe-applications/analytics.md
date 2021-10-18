---
keywords: Experience Platform; Startseite; beliebte Themen; Analytics-Quell-Connector; Analytics-Connector; Analytics-Quelle; Analytics
solution: Experience Platform
title: Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Adobe Analytics-Quellverbindung in der Benutzeroberfläche erstellen, um Verbraucherdaten in Adobe Experience Platform zu importieren.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: e28158bbd4e89e5fcf19f4dc89f266d737b34e65
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 7%

---

# Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie in der Benutzeroberfläche eine Adobe Analytics-Quellverbindung erstellen, um [!DNL Analytics] Report Suite-Daten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Wichtige Terminologie

Es ist wichtig, die folgenden Schlüsselbegriffe zu verstehen, die in diesem Dokument verwendet werden:

* **Standardattribut**: Standardattribute sind alle Attribute, die von Adobe vordefiniert sind. Sie enthalten dieselbe Bedeutung für alle Kunden und sind in den [!DNL Analytics] Quelldaten und den [!DNL Analytics] Schemafeldgruppen verfügbar.
* **Benutzerdefiniertes Attribut**: Benutzerdefinierte Attribute sind beliebige Attribute in der Hierarchie der benutzerdefinierten Variablen in  [!DNL Analytics]. Benutzerdefinierte Attribute werden innerhalb einer Adobe Analytics-Implementierung verwendet, um bestimmte Informationen in einer Report Suite zu erfassen. Sie können sich bei ihrer Verwendung von Report Suite zu Report Suite unterscheiden. Zu den benutzerdefinierten Attributen gehören eVars, Props und Listen. Weitere Informationen zu eVars finden Sie in der folgenden [[!DNL Analytics] Dokumentation zu Konversionsvariablen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .
* **Jedes Attribut in benutzerdefinierten Feldergruppen**: Attribute, die aus von Kunden erstellten Feldergruppen stammen, sind alle benutzerdefiniert und gelten weder als Standard- noch als benutzerdefinierte Attribute.
* **Anzeigenamen**: Anzeigenamen sind von Menschen bereitgestellte Beschriftungen für benutzerdefinierte Variablen in einer  [!DNL Analytics] Implementierung. Weitere Informationen zu Anzeigenamen finden Sie in der folgenden [[!DNL Analytics] Dokumentation zu Konversionsvariablen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .

## Erstellen einer Quellverbindung mit Adobe Analytics

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Quellen einzugrenzen.

Wählen Sie unter der Kategorie **[!UICONTROL Adobe Applications]** die Option **[!UICONTROL Adobe Analytics]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/analytics/catalog.png)

### Daten auswählen

Der Schritt **[!UICONTROL Analytics source add data]** wird angezeigt. Wählen Sie **[!UICONTROL Report Suite]** aus, um eine Quellverbindung für Analytics Report Suite-Daten zu erstellen, und wählen Sie dann die Report Suite aus, die Sie aufnehmen möchten. Report Suites, die nicht auswählbar sind, wurden bereits aufgenommen, entweder in dieser Sandbox oder in einer anderen Sandbox. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

>[!NOTE]
>
>Es können mehrere eingehende Verbindungen hergestellt werden, um mehrere Report Suites einzuführen. Es kann jedoch jeweils nur eine Report Suite mit Real-time Customer Data Platform verwendet werden.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Zuordnung

>[!IMPORTANT]
>
>Die Funktion zur Datenvorbereitung-Unterstützung für die [!DNL Analytics]-Quelle befindet sich in der Beta-Phase.

Die Seite [!UICONTROL Mapping] bietet eine Schnittstelle zum Zuordnen von Quellfeldern zu den entsprechenden Zielschemafeldern. Von hier aus können Sie benutzerdefinierte Variablen neuen Schemafeldgruppen zuordnen und Berechnungen anwenden, wie von der Datenvorbereitung unterstützt. Wählen Sie ein Zielschema aus, um den Zuordnungsprozess zu starten.

>[!TIP]
>
>Im Menü der Schemaauswahl werden nur Schemata angezeigt, die die Vorlagenfeldgruppe [!DNL Analytics] aufweisen. Andere Schemata werden weggelassen. Wenn für Ihre Report Suite-Daten keine geeigneten Schemata verfügbar sind, müssen Sie ein neues Schema erstellen. Ausführliche Anweisungen zum Erstellen von Schemas finden Sie im Handbuch zum Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md).[

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

Im Abschnitt [!UICONTROL Standardfelder zuordnen] werden Bedienfelder für [!UICONTROL angewendete Standardzuordnungen], [!UICONTROL Nicht übereinstimmende Standardzuordnungen] und [!UICONTROL Benutzerdefinierte Zuordnungen] angezeigt. In der folgenden Tabelle finden Sie spezifische Informationen zu den einzelnen Kategorien:

| Standardfelder zuordnen | Beschreibung |
| --- | --- |
| [!UICONTROL Angewandte Standard-Zuordnungen] | Das Bedienfeld [!UICONTROL Angewandte Standardzuordnungen] zeigt die Gesamtzahl der zugeordneten Attribute an. Standardzuordnungen beziehen sich auf Zuordnungssätze zwischen allen Attributen in den Quelldaten [!DNL Analytics] und den entsprechenden Attributen in der Feldergruppe [!DNL Analytics]. Diese sind vorab zugeordnet und können nicht bearbeitet werden. |
| [!UICONTROL Nicht übereinstimmende Standardzuordnungen] | Das Bedienfeld [!UICONTROL Nicht übereinstimmende Standardzuordnungen] bezieht sich auf die Anzahl der zugeordneten Attribute, die Konflikte mit Anzeigenamen enthalten. Diese Konflikte treten auf, wenn Sie ein Schema wiederverwenden, das bereits über einen befüllten Satz von Felddeskriptoren aus einer anderen Report Suite verfügt. Sie können mit Ihrem [!DNL Analytics]-Datenfluss fortfahren, auch mit benutzerfreundlichen Namenskonflikten. |
| [!UICONTROL Benutzerdefinierte Zuordnungen] | Im Bedienfeld [!UICONTROL Benutzerdefinierte Zuordnungen] wird die Anzahl der zugeordneten benutzerdefinierten Attribute angezeigt, einschließlich eVars, Props und Listen. Benutzerdefinierte Zuordnungen beziehen sich auf Zuordnungssätze zwischen benutzerdefinierten Attributen in den Quelldaten [!DNL Analytics] und Attributen in benutzerdefinierten Feldergruppen, die im ausgewählten Schema enthalten sind. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Um eine Vorschau der Feldergruppe [!DNL Analytics] ExperienceEvent-Vorlagenschema anzuzeigen, wählen Sie **[!UICONTROL Ansicht]** im Bedienfeld [!UICONTROL Angewendete Standardzuordnungen] aus.

![view](../../../../images/tutorials/create/analytics/view.png)

Die Seite [!UICONTROL Adobe Analytics ExperienceEvent-Vorlagenfeldgruppe] bietet eine Benutzeroberfläche zum Prüfen der Schemastruktur. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Close]** aus.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform erkennt Ihre Zuordnungssätze automatisch für Konflikte mit benutzerfreundlichen Namen. Wenn keine Konflikte mit Ihren Zuordnungssätzen auftreten, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Mapping](../../../../images/tutorials/create/analytics/mapping.png)

Wenn Konflikte mit benutzerfreundlichen Namen zwischen Ihrer Quell-Report Suite und Ihrem ausgewählten Schema auftreten, können Sie weiterhin mit Ihrem [!DNL Analytics]-Datenfluss fortfahren, wobei bestätigt wird, dass die Felddeskriptoren nicht geändert werden. Alternativ können Sie auch ein neues Schema mit einem leeren Satz von Deskriptoren erstellen.

Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Warnung](../../../../images/tutorials/create/analytics/caution.png)

#### Benutzerdefinierte Zuordnungen

Um Datenvorgangsfunktionen zu verwenden und neue Zuordnungsfelder oder berechnete Felder für benutzerdefinierte Attribute hinzuzufügen, wählen Sie **[!UICONTROL Benutzerdefinierte Zuordnungen anzeigen]** aus.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Wählen Sie als Nächstes **[!UICONTROL Neues Mapping hinzufügen]** aus.

Je nach Bedarf können Sie aus den angezeigten Optionen entweder **[!UICONTROL Neues Mapping hinzufügen]** oder **[!UICONTROL Berechnetes Feld]** hinzufügen auswählen.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Ein leerer Zuordnungssatz wird angezeigt. Wählen Sie das Zuordnungssymbol aus, um ein Quellfeld hinzuzufügen.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Sie können die Benutzeroberfläche verwenden, um durch die Struktur des Quellschemas zu navigieren und das neue Quellfeld zu identifizieren, das Sie verwenden möchten. Nachdem Sie das Quellfeld ausgewählt haben, das Sie zuordnen möchten, wählen Sie **[!UICONTROL Wählen Sie]** aus.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Wählen Sie anschließend das Zuordnungssymbol unter [!UICONTROL Zielfeld] aus, um das ausgewählte Quellfeld dem entsprechenden Zielfeld zuzuordnen.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Ähnlich wie das Quellschema können Sie über die Benutzeroberfläche durch die Zielschemastruktur navigieren und das Zielfeld auswählen, dem Sie zuordnen möchten. Nachdem Sie das entsprechende Zielfeld ausgewählt haben, wählen Sie **[!UICONTROL Wählen Sie]** aus.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Nachdem Sie den benutzerdefinierten Zuordnungssatz abgeschlossen haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

Die folgende Dokumentation enthält weitere Ressourcen zum Verständnis der Datenvorbereitung, berechneten Feldern und Zuordnungsfunktionen:

* [Datenvorbereitung – Übersicht](../../../../../data-prep/home.md)
* [Zuordnungsfunktionen für Datenvorbereitung](../../../../../data-prep/functions.md)
* [Berechnete Felder hinzufügen](../../../../../data-prep/calculated-fields.md)

### Datenflussdetails angeben

Der Schritt **[!UICONTROL Datenfluss-Detail]** wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenfluss angeben müssen. Klicken Sie auf **[!UICONTROL Weiter]**, wenn Sie fertig sind.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Überprüfung

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, mit dem Sie Ihren neuen Analytics-Datenfluss überprüfen können, bevor er erstellt wird. Details der Verbindung werden nach Kategorien gruppiert, darunter:

* [!UICONTROL Verbindung]: Zeigt die Quellplattform der Verbindung an.
* [!UICONTROL Datentyp]: Zeigt die ausgewählte Report Suite und die zugehörige Report Suite-ID an.

![Überprüfung](../../../../images/tutorials/create/analytics/review.png)

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn erfasst werden. Wählen Sie im Bildschirm [!UICONTROL Katalog] die Option **[!UICONTROL Datenflüsse]** aus, um eine Liste der mit Ihrem Analytics-Konto verbundenen etablierten Flüsse anzuzeigen.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Der Bildschirm **Datenflüsse** wird angezeigt. Auf dieser Seite finden Sie ein Paar von Datensatzflüssen, einschließlich Informationen zu ihrem Namen, Quelldaten, Erstellungszeit und Status.

Der Connector instanziiert zwei Datensatzflüsse. Ein Fluss stellt Aufstockungsdaten dar, der andere für Live-Daten. Aufstockungsdaten werden nicht für Profile konfiguriert, sondern für analytische und datenwissenschaftliche Anwendungsfälle an den Data Lake gesendet.

Weitere Informationen zur Aufstockung, zu Live-Daten und ihren jeweiligen Latenzen finden Sie in der [Übersicht über Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Wählen Sie in der Liste den gewünschten Datensatzfluss aus.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Die Seite **[!UICONTROL Datensatzaktivität]** wird angezeigt. Auf dieser Seite wird die Rate der Nachrichten angezeigt, die in Form eines Diagramms konsumiert werden. Wählen Sie **[!UICONTROL Data Governance]** aus der oberen Kopfzeile aus, um auf die Beschriftungsfelder zuzugreifen.

![dataset-activity](../../../../images/tutorials/create/analytics/dataset-activity.png)

Sie können die geerbten Bezeichnungen eines Datensatzflusses im Bildschirm [!UICONTROL Data Governance] anzeigen. Weitere Informationen zur Beschriftung von Daten aus Analytics finden Sie im [Handbuch zu Datennutzungsbezeichnungen](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Um einen Datenfluss zu löschen, rufen Sie die Seite [!UICONTROL Datenflüsse] auf, wählen Sie dann die Auslassungszeichen (`...`) neben dem Datenflusennamen aus und klicken Sie auf [!UICONTROL Löschen].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Nächste Schritte und zusätzliche Ressourcen

Nach der Erstellung der Verbindung wird der Datenfluss automatisch erstellt, um die eingehenden Daten zu enthalten und einen Datensatz mit Ihrem ausgewählten Schema zu füllen. Darüber hinaus werden bis zu 13 Monate historischer Daten aufgefüllt und erfasst. Wenn die erste Aufnahme abgeschlossen ist, können [!DNL Analytics] Daten von nachgelagerten Platform-Diensten wie [!DNL Real-time Customer Profile] und Segmentation Service verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] – Übersicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] – Übersicht](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] – Übersicht](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] – Übersicht](../../../../../query-service/home.md)

Das folgende Video soll Ihnen helfen, Daten mithilfe des Adobe Analytics Source Connectors zu erfassen:

>[!WARNING]
>
> Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. In der obigen Dokumentation finden Sie die neuesten Screenshots und Funktionen der Benutzeroberfläche.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
