---
keywords: Experience Platform;Home;beliebte Themen;ui;UI;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Schema-Editor;Schema-Editor;Schema;Schema;Schemas;Schemas;Erstellen
solution: Experience Platform
title: Erstellen eines Schemas mit dem Schema-Editor
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '3751'
ht-degree: 12%

---

# Erstellen Sie ein Schema mit dem[!DNL Schema Editor]

Die Adobe Experience Platform-Benutzeroberfläche ermöglicht es Ihnen, [!DNL Experience Data Model] (XDM)-Schema in einer interaktiven visuellen Arbeitsfläche zu erstellen und zu verwalten, die als [!DNL Schema Editor] bezeichnet wird. In diesem Lernprogramm wird beschrieben, wie Sie mit dem [!DNL Schema Editor] ein Schema erstellen.

>[!NOTE]
>
>Zu Demonstrationszwecken wird in diesem Lernprogramm ein Schema erstellt, in dem die Mitglieder eines Kundentreue-Programms beschrieben werden. Sie können diese Schritte verwenden, um ein anderes Schema für Ihre eigenen Zwecke zu erstellen. Es wird jedoch empfohlen, zunächst das Schema zu erstellen, um die Funktionen von [!DNL Schema Editor] zu erlernen.

Wenn Sie stattdessen lieber ein Schema mit der API zusammenstellen möchten, lesen Sie den Beginn [[!DNL Schema Registry] Entwicklerhandbuch](../api/getting-started.md), bevor Sie das Lernprogramm [zum Erstellen eines Schemas mit der API](create-schema-api.md) durchführen.[!DNL Schema Registry]

## Erste Schritte

Dieses Tutorial erfordert ein Verständnis der verschiedenen Aspekte der Adobe Experience Platform, die an der Schaffung von Schemas beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie die Dokumentation für die folgenden Konzepte:

* [[!DNL Experience Data Model (XDM)]](../home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../schema/composition.md) des Schemas: Eine Übersicht über XDM-Schema und ihre Bausteine, einschließlich Klassen, Schema-Feldgruppen, Datentypen und Einzelfelder.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Öffnen Sie den Arbeitsbereich [!UICONTROL Schemas] {#browse}

Der Arbeitsbereich [!UICONTROL Schema] in der [!DNL Platform]-Benutzeroberfläche bietet eine Visualisierung des [!DNL Schema Library]-Vorgangs, mit dem Sie die Ansicht haben, die für Ihr Unternehmen verfügbaren Schema zu verwalten. Der Arbeitsbereich enthält auch die Arbeitsfläche [!DNL Schema Editor], auf der Sie ein Schema in diesem Lernprogramm erstellen können.

Nach der Anmeldung bei [!DNL Experience Platform] wählen Sie **[!UICONTROL Schema]** in der linken Navigation aus, um den Arbeitsbereich **[!UICONTROL Schema]** zu öffnen. Auf der Registerkarte **[!UICONTROL Durchsuchen]** wird eine Liste von Schemas (eine Darstellung der [!DNL Schema Library]) angezeigt, die Sie Ansicht und Anpassung vornehmen können. Die Liste umfasst den Namen, den Typ, die Klasse und das Verhalten (Datensatz oder Zeitreihen), auf denen das Schema basiert, sowie das Datum und die Uhrzeit der letzten Änderung des Schemas.

Weitere Informationen finden Sie im Handbuch [Vorhandene XDM-Ressourcen in der Benutzeroberfläche](../ui/explore.md).

## Erstellen und Benennen eines Schemas {#create}

Um mit dem Erstellen eines Schemas zu beginnen, wählen Sie **[!UICONTROL Schema erstellen]** oben rechts im Arbeitsbereich **[!UICONTROL Schema]**. Es wird ein Dropdown-Menü angezeigt, in dem Sie zwischen den Hauptklassen [!UICONTROL XDM Individuelles Profil] und [!UICONTROL XDM ExperienceEvent] wählen können. Wenn diese Klassen Ihren Zwecken nicht entsprechen, können Sie auch **[!UICONTROL Browse]** auswählen, um aus anderen verfügbaren Klassen auszuwählen, oder [eine neue Klasse ](#create-new-class) erstellen.

Wählen Sie für diese Übung **[!UICONTROL XDM Individuelles Profil]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Da Sie eine Standard-XDM-Klasse ausgewählt haben, auf der das Schema basieren soll, wird das Dialogfeld **[!UICONTROL Hinzufügen Feldgruppe]** angezeigt, in dem Sie sofort Beginn zum Hinzufügen von Feldern zum Schema hinzufügen können. Wählen Sie zunächst **[!UICONTROL Abbrechen]**, um das Dialogfeld zu verlassen.

![](../images/tutorials/create-schema/cancel-field-group.png)

Das Symbol [!DNL Schema Editor] wird angezeigt. Dies ist die Arbeitsfläche, auf der Sie Ihr Schema zusammenstellen. Ein unbenanntes Schema wird automatisch im Bereich **[!UICONTROL Struktur]** der Arbeitsfläche erstellt, wenn Sie im Editor ankommen, zusammen mit den Standardfeldern, die in allen Schemas, die auf dieser Klasse basieren, enthalten sind. Die zugewiesene Klasse für das Schema wird auch unter **[!UICONTROL Class]** im Abschnitt **[!UICONTROL Zusammensetzung]** aufgeführt.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
> Sie können [die Klasse eines Schemas](#change-class) jederzeit während des anfänglichen Kompositionsprozesses ändern, bevor das Schema gespeichert wird. Dies sollte jedoch mit größter Vorsicht geschehen. Feldgruppen sind nur mit bestimmten Klassen kompatibel. Wenn Sie die Klasse ändern, werden die Arbeitsfläche und alle hinzugefügten Felder zurückgesetzt.

Verwenden Sie die Felder auf der rechten Seite des Editors, um einen Anzeigenamen und eine optionale Beschreibung für das Schema anzugeben. Sobald ein Name eingegeben wurde, wird die Arbeitsfläche aktualisiert und gibt den neuen Namen des Schemas wieder.

![](../images/tutorials/create-schema/name_schema.png)

Bei der Entscheidung über einen Namen für Ihr Schema sind einige wichtige Aspekte zu beachten:

* Schema-Namen sollten kurz und beschreibend sein, damit das Schema später leicht zu finden ist.
* Die Namen der Schemas müssen eindeutig sein, d. h. sie sollten so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden. Wenn Ihr Unternehmen z. B. über separate Loyalitätsprogramme für verschiedene Marken verfügt, wäre es ratsam, Ihr Schema mit „Loyalitätsmitglieder, Marke A“ zu benennen, damit Sie dieses leicht von anderen Loyalitätsschemas unterscheiden können, die Sie u. U. später definieren.
* Sie können die Beschreibung des Schemas auch verwenden, um zusätzliche Kontextinformationen zum Schema bereitzustellen.

Dieses Tutorial stellt ein Schema zum Erfassen von Daten zu den Mitgliedern eines Treueanschlusses vor, und deshalb heißt das Schema &quot;Treueanwärter&quot;.

## hinzufügen einer Feldgruppe {#field-group}

Sie können nun mit dem Hinzufügen von Feldern zu Ihrem Schema beginnen, indem Sie Feldgruppen hinzufügen. Eine Feldgruppe ist eine Gruppe von Feldern, die häufig zusammen zur Beschreibung eines bestimmten Konzepts verwendet werden. In diesem Lernprogramm werden Feldgruppen verwendet, um die Mitglieder des Programms zu beschreiben und wichtige Informationen wie Name, Geburtstag, Telefonnummer, Adresse und mehr zu erfassen.

Um eine Feldgruppe hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen]** im Unterabschnitt **[!UICONTROL Feldgruppen]** aus.

![](../images/tutorials/create-schema/add-field-group-button.png)

Ein neues Dialogfeld mit einer Liste der verfügbaren Feldgruppen wird angezeigt. Jede Feldgruppe ist nur für die Verwendung mit einer bestimmten Klasse vorgesehen. Daher werden im Dialogfeld nur Feldgruppen Liste, die mit der ausgewählten  kompatibel sind (in diesem Fall mit der [!DNL XDM Individual Profile]-Klasse). Wenn Sie eine Standard-XDM-Klasse verwenden, wird die Liste der Feldgruppen basierend auf der Beliebtheit der Verwendung intelligent sortiert.

![](../images/tutorials/create-schema/field-group-popularity.png)

Wenn Sie eine Feldgruppe aus der Liste auswählen, wird sie in der rechten Leiste angezeigt. Sie können bei Bedarf mehrere Feldgruppen auswählen und diese der Liste in der rechten Leiste hinzufügen, bevor Sie sie bestätigen. Darüber hinaus wird auf der rechten Seite der aktuell ausgewählten Feldgruppe ein Symbol angezeigt, mit dem Sie die Vorschau der Feldstruktur vornehmen können.

![](../images/tutorials/create-schema/preview-field-group-button.png)

Bei der Vorschau einer Feldgruppe wird das Schema der Feldgruppe in der rechten Leiste ausführlich beschrieben. Sie können auch durch die Felder der Feldgruppe in der bereitgestellten Arbeitsfläche navigieren. Wenn Sie verschiedene Felder auswählen, wird die rechte Leiste aktualisiert, um Details zum betreffenden Feld anzuzeigen. Wählen Sie **[!UICONTROL Zurück]**, wenn Sie die Vorschau abgeschlossen haben, um zum Dialogfeld für die Feldgruppenauswahl zurückzukehren.

![](../images/tutorials/create-schema/preview-field-group.png)

Wählen Sie für dieses Lernprogramm die Feldgruppe **[!UICONTROL Demografische Details]** und dann **[!UICONTROL Hinzufügen Feldgruppe]**.

![](../images/tutorials/create-schema/demographic-details.png)

Die Arbeitsfläche des Schemas wird wieder angezeigt. Im Abschnitt **[!UICONTROL Feldgruppen]** werden jetzt Listen &quot;[!UICONTROL Demografische Details]&quot;und im Abschnitt **[!UICONTROL Struktur]** werden die von der Feldgruppe hinzugefügten Felder angezeigt. Sie können den Namen der Feldgruppe im Abschnitt **[!UICONTROL Feldgruppen]** auswählen, um die spezifischen Felder, die sie auf der Arbeitsfläche bereitstellt, hervorzuheben.

![](../images/tutorials/create-schema/demographic-details-structure.png)

Diese Feldgruppe fügt mehrere Felder unter dem Namen der obersten Ebene `person` mit dem Datentyp &quot;[!UICONTROL Person]&quot;ein. Diese Gruppe von Feldern beschreibt Informationen zu einer Person, einschließlich Name, Geburtsdatum und Geschlecht.

>[!NOTE]
>
>Denken Sie daran, dass Felder skalare Typen (wie String, Ganzzahl, Array oder Datum) sowie alle Datentypen (eine Gruppe von Feldern, die ein gemeinsames Konzept darstellen) verwenden können, die in den [!DNL Schema Registry] definiert sind.

Beachten Sie, dass das Feld `name` den Datentyp &quot;[!UICONTROL Personenname]&quot;hat. Das bedeutet, dass es auch ein allgemeines Konzept beschreibt und namensbezogene Unterfelder wie Vorname, Nachname, Höflichkeitstitel und Suffix enthält.

Wählen Sie die verschiedenen Felder auf der Arbeitsfläche aus, um alle weiteren Felder anzuzeigen, die sie zur Schema-Struktur beitragen.

## hinzufügen einer anderen Feldgruppe {#field-group-2}

Sie können jetzt dieselben Schritte wiederholen, um eine weitere Feldgruppe hinzuzufügen. Wenn Sie dieses Mal das Dialogfeld **[!UICONTROL Hinzufügen]** Ansicht haben, beachten Sie, dass die Feldgruppe &quot;[!UICONTROL Demografische Details]&quot;ausgegraut wurde und das Kontrollkästchen daneben nicht aktiviert werden kann. Dadurch wird verhindert, dass Sie versehentlich Feldgruppen duplizieren, die Sie bereits im aktuellen Schema enthalten haben.

Wählen Sie für dieses Lernprogramm die Feldgruppe &quot;[!DNL Personal Contact Details]&quot;im Dialogfeld aus und wählen Sie dann **[!UICONTROL Hinzufügen Feldgruppe]** aus, um sie dem Schema hinzuzufügen.

![](../images/tutorials/create-schema/personal-contact-details.png)

Nach dem Hinzufügen wird die Arbeitsfläche wieder angezeigt. &quot;[!UICONTROL Persönliche Kontaktdaten]&quot;wird jetzt unter **[!UICONTROL Feldgruppen]** im Abschnitt **[!UICONTROL Zusammensetzung]** aufgelistet. Die Felder für die Homepage, das Handy und weitere wurden unter **[!UICONTROL Struktur]** hinzugefügt.

Ähnlich wie im Feld `name` stellen die soeben hinzugefügten Felder Konzepte für mehrere Felder dar. Beispiel: `homeAddress` hat den Datentyp &quot;[!UICONTROL Postadresse]&quot;und `mobilePhone` hat den Datentyp &quot;[!UICONTROL Telefonnummer]&quot;. Sie können jedes dieser Felder auswählen, um sie zu erweitern und die zusätzlichen Felder anzuzeigen, die im Datentyp enthalten sind.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## Definieren einer benutzerspezifischen Feldgruppe {#define-field-group}

Das Schema &quot;[!UICONTROL Treuemitglieder]&quot;dient zum Erfassen von Daten, die mit den Mitgliedern eines Treuebereichs in Verbindung stehen. Es erfordert daher einige spezifische treuebezogene Programme.

Es gibt eine Standardfeldgruppe [!UICONTROL Treuedetails], die Sie dem Schema hinzufügen können, um allgemeine Felder im Zusammenhang mit einem Treuefeld zu erfassen. Es wird dringend empfohlen, Standardfeldgruppen zur Darstellung von Begriffen zu verwenden, die von Ihren Schemas erfasst werden. Die Standardfeldgruppe für Loyalität kann jedoch möglicherweise nicht alle relevanten Daten für Ihr bestimmtes Treuhandfeld erfassen. In diesem Szenario können Sie eine neue benutzerspezifische Feldgruppe definieren, um diese Felder stattdessen zu erfassen.

Öffnen Sie das Dialogfeld **[!UICONTROL Hinzufügen]** erneut, wählen Sie dieses Mal jedoch **[!UICONTROL Neue Feldgruppe]** oben erstellen. Anschließend werden Sie aufgefordert, einen Anzeigenamen und eine Beschreibung für Ihre Feldgruppe anzugeben.

![](../images/tutorials/create-schema/create-new-field-group.png)

Wie bei Klassennamen sollte der Feldgruppenname kurz und einfach sein und beschreiben, welchen Beitrag die Feldgruppe zum Schema leisten wird. Auch diese sind eindeutig, sodass Sie den Namen nicht wiederverwenden können und daher sicherstellen müssen, dass er spezifisch genug ist.

Benennen Sie für dieses Lernprogramm die neue Feldgruppe &quot;Treuedetails&quot;.

Wählen Sie **[!UICONTROL Hinzufügen Feldgruppe]** aus, um zum [!DNL Schema Editor] zurückzukehren. &quot;[!UICONTROL Kundentreuedetails]&quot;sollten jetzt links auf der Arbeitsfläche unter **[!UICONTROL Feldgruppen]** angezeigt werden. Es sind jedoch noch keine Felder verknüpft, sodass unter **[!UICONTROL Struktur]** keine neuen Felder angezeigt werden.

## hinzufügen Felder zur Feldgruppe {#field-group-fields}

Nachdem Sie die Feldgruppe &quot;Treuedetails&quot;erstellt haben, ist es an der Zeit, die Felder zu definieren, die die Feldgruppe zum Schema beitragen soll.

Wählen Sie zunächst den Feldgruppennamen im Abschnitt **[!UICONTROL Feldgruppen]** aus. Danach werden die Eigenschaften der Feldgruppe auf der rechten Seite des Editors angezeigt und unter **[!UICONTROL Struktur]** wird ein **Pluszeichen (+)** neben dem Namen des Schemas angezeigt.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Wählen Sie das Symbol **plus (+)** neben &quot;[!DNL Loyalty Members]&quot;aus, um einen neuen Knoten in der Struktur zu erstellen. Dieser Knoten (in diesem Beispiel `_tenantId` genannt) stellt die Mandant-ID Ihres IMS-Unternehmens dar, der ein Unterstrich vorangestellt ist. Das Vorhandensein der Mandanten-ID zeigt an, dass die Felder, die Sie hinzufügen, im Namensraum Ihres Unternehmens enthalten sind.

Mit anderen Worten, die Felder, die Sie hinzufügen, sind für Ihr Unternehmen eindeutig und werden in einem bestimmten Bereich gespeichert, der nur für Ihr Unternehmen zugänglich ist. [!DNL Schema Registry] Felder, die Sie definieren, müssen immer Ihrem Pächter-Namensraum hinzugefügt werden, um Kollisionen mit Namen anderer Standardklassen, Feldgruppen, Datentypen und Felder zu vermeiden.

Innerhalb dieses Namespaced-Knotens befindet sich ein &quot;[!UICONTROL Neues Feld]&quot;. Dies ist der Anfang der Feldgruppe &quot;[!UICONTROL Treuedetails]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Beginn erstellen mithilfe der Steuerelemente auf der rechten Seite des Editors ein `loyalty`-Feld mit dem Typ &quot;[!UICONTROL Objekt]&quot;, das zur Speicherung Ihrer treuebezogenen Felder verwendet wird. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Die Änderungen werden angewendet und das neu erstellte `loyalty`-Objekt wird angezeigt. Klicken Sie auf das Symbol **plus (+)** neben dem Objekt, um weitere treuebezogene Felder hinzuzufügen. Ein &quot;[!UICONTROL Neues Feld]&quot;wird angezeigt und der Abschnitt **[!UICONTROL Feldeigenschaften]** ist auf der rechten Seite der Arbeitsfläche sichtbar.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Für jedes Feld sind die folgenden Informationen erforderlich:

* **[!UICONTROL Feldname]:** Der Name des Felds, in Kamelschreibung geschrieben. Beispiel: LoyalitätsStufe
* **[!UICONTROL Anzeigename]:** Der Name des Felds, in Titelschrift geschrieben. Beispiel: Loyalitäts-Stufe
* **[!UICONTROL Typ]:** Der Datentyp des Felds. Dazu gehören grundlegende Skalartypen und alle Datentypen, die in [!DNL Schema Registry] definiert sind. Beispiele: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Adresse], [!UICONTROL Telefonnummer] usw.
* **[!UICONTROL Beschreibung]:** Eine optionale Beschreibung des Felds sollte mit maximal 200 Zeichen in Satzform eingefügt werden.

Das erste Feld für das `Loyalty`-Objekt ist eine Zeichenfolge mit dem Namen `loyaltyId`. Wenn Sie den Typ des neuen Felds auf &quot;[!UICONTROL String]&quot;festlegen, werden im Abschnitt **[!UICONTROL Feldeigenschaften]** mehrere Optionen zum Anwenden von Einschränkungen angezeigt, einschließlich Standardwert, Format und maximale Länge.

![](../images/tutorials/create-schema/string_constraints.png)

Je nach ausgewähltem Datentyp stehen verschiedene Einschränkungsoptionen zur Verfügung. Da `loyaltyId` eine E-Mail-Adresse sein wird, wählen Sie &quot;[!UICONTROL email]&quot;aus dem Dropdownmenü **[!UICONTROL Format]**. Wählen Sie **[!UICONTROL Übernehmen]**, um Ihre Änderungen anzuwenden.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## hinzufügen Sie weitere Felder zur Feldgruppe {#field-group-fields-2}

Nachdem Sie das Feld `loyaltyId` hinzugefügt haben, können Sie weitere Felder hinzufügen, um treuitätsbezogene Informationen zu erfassen, z. B.:

* Punkte (Ganzzahl)
* Mitglied seit (Datum)

Um die einzelnen Felder dem Schema hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Objekt `loyalty` aus und geben Sie die erforderlichen Informationen ein.

Nach Abschluss des Vorgangs enthält das Treueobjekt die Felder für die Loyalität-ID, die Punkte und das Mitglied-seit.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## hinzufügen ein Enum-Feld für die Feldgruppe {#enum}

Beim Definieren von Feldern in [!DNL Schema Editor] gibt es einige zusätzliche Optionen, die Sie auf einfache Feldtypen anwenden können, um weitere Einschränkungen für die Daten bereitzustellen, die das Feld enthalten kann. Die Anwendungsfälle für diese Beschränkungen werden in der folgenden Tabelle erläutert:

| Constraint | Beschreibung |
| --- | --- |
| [!UICONTROL Erforderlich] | Gibt an, dass das Feld für die Datenerfassung erforderlich ist. Daten, die auf Grundlage dieses Schemas in einen Datensatz hochgeladen wurden und dieses Feld nicht enthalten, schlagen bei der Aufnahme fehl. |
| [!UICONTROL Array] | Gibt an, dass das Feld ein Array von Werten mit jeweils dem angegebenen Datentyp enthält. Wenn Sie diese Einschränkung beispielsweise für ein Feld mit dem Datentyp &quot;[!UICONTROL String]&quot;verwenden, gibt das Feld ein Zeichenfolgenarray an. |
| [!UICONTROL Enum] | Gibt an, dass dieses Feld einen der Werte aus einer nummerierten Liste möglicher Werte enthalten muss. |
| [!UICONTROL Identität] | Gibt an, dass dieses Feld ein Identitätsfeld ist. Weitere Informationen zu Identitätsfeldern finden Sie [weiter unten in diesem Tutorial](#identity-field). |
| [!UICONTROL Beziehung] | Während Schema-Beziehungen durch die Verwendung des Vereinigung-Schemas und [!DNL Real-time Customer Profile] abgeleitet werden können, gilt dies nur für Schema, die dieselbe Klasse gemeinsam haben. Die [!UICONTROL Relationship]-Beschränkung gibt an, dass dieses Feld auf die primäre Identität eines Schemas verweist, das auf einer anderen Klasse basiert, was eine Beziehung zwischen den beiden Schemas impliziert. Weitere Informationen finden Sie im Tutorial zu [Definieren einer Beziehung](./relationship-ui.md). |

>[!NOTE]
>
>Alle erforderlichen Identitäts- oder Beziehungsfelder werden in der linken Leiste angezeigt, sodass Sie diese Felder unabhängig von der Komplexität des Schemas leicht finden können.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Für dieses Lernprogramm ist für das [!DNL "loyalty"]-Objekt im Schema ein neues Enum-Feld erforderlich, das die &quot;Treuestufe&quot;eines Kunden beschreibt, bei dem der Wert nur eine von vier möglichen Optionen sein kann. Um dieses Feld zum Schema hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Objekt `loyalty` aus und füllen Sie die erforderlichen Felder für **[!UICONTROL Feldname]** und **[!UICONTROL Anzeigename]** aus. Wählen Sie für **[!UICONTROL Typ]** &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Zusätzliche Kontrollkästchen werden für das Feld angezeigt, nachdem der Typ ausgewählt wurde, einschließlich der Kontrollkästchen für **[!UICONTROL Array]**, **[!UICONTROL Enum]** und **[!UICONTROL Identity]**.

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Enum]**, um den Abschnitt **[!UICONTROL Enum values]** zu öffnen. Hier können Sie für jede akzeptable Loyalitätsstufe den **[!UICONTROL Wert]** (in Binnenmajuskel-Schreibweise) und die **[!UICONTROL Bezeichnung]** (einen optionalen, leserfreundlichen Namen in der Titelschreibweise) eingeben.

Wenn Sie alle Feldeigenschaften abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]**, um dem `loyalty`-Objekt das Feld &quot;[!DNL loyaltyLevel]&quot;hinzuzufügen.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#datatype}

Das `loyalty`-Objekt enthält jetzt mehrere treuespezifische Felder und stellt eine gemeinsame Datenstruktur dar, die in anderen Schemas nützlich sein könnte. Mit dem [!DNL Schema Editor] können Sie wiederverwendbare Objekte mit mehreren Feldern einfach anwenden, indem Sie die Struktur dieser Objekte in Datentypen konvertieren.

Datentypen ermöglichen den konsistenten Einsatz von Strukturen mit mehreren Feldern und bieten mehr Flexibilität als Feldgruppen, da sie überall in einem Schema verwendet werden können. Dazu legen Sie den Wert **[!UICONTROL Type]** des Felds auf den Wert eines Datentyps fest, der in [!DNL Schema Registry] definiert ist.

Um das `loyalty`-Objekt in einen Datentyp zu konvertieren, wählen Sie unter **[!UICONTROL Struktur]** das Feld `loyalty` und dann **[!UICONTROL In neuen Datentyp]** konvertieren auf der rechten Seite des Editors unter **[!UICONTROL Feldeigenschaften]**. Es wird ein grünes Popup angezeigt, das bestätigt, dass das Objekt erfolgreich konvertiert wurde.

![](../images/tutorials/create-schema/convert-data-type.png)

Wenn Sie jetzt unter **[!UICONTROL Struktur]** nachsehen, können Sie sehen, dass das `loyalty`-Feld einen Datentyp von &quot;[!DNL Loyalty]&quot;hat und die Felder kleine Sperrsymbole neben ihnen haben, was darauf hinweist, dass es sich nicht mehr um einzelne Felder, sondern um Bereiche eines Multi-field-Datentyps handelt.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In einem zukünftigen Schema können Sie nun ein Feld als &quot;[!DNL Loyalty]&quot;zuweisen und es enthält automatisch Felder für ID, Treuestufe, Member-Seitenzahlen und Punkte.

>[!NOTE]
>
>Sie können benutzerdefinierte Datentypen auch unabhängig von der Bearbeitung von Schemas erstellen und bearbeiten. Weitere Informationen finden Sie im Handbuch [Erstellen und Bearbeiten von Datentypen](../ui/resources/data-types.md).

## Suchen und Filtern von Schema-Feldern

Ihr Schema enthält jetzt zusätzlich zu den von der Basisklasse bereitgestellten Feldern mehrere Feldgruppen. Wenn Sie mit größeren Schemas arbeiten, können Sie die Kontrollkästchen neben den Feldgruppennamen in der linken Leiste aktivieren, um die angezeigten Felder auf diejenigen zu filtern, die von den Feldgruppen bereitgestellt werden, die Sie interessieren.

![](../images/tutorials/create-schema/filter-by-field-group.png)

Wenn Sie ein bestimmtes Feld in Ihrem Schema suchen, können Sie die angezeigten Felder auch über die Suchleiste nach Namen filtern, unabhängig davon, unter welcher Feldgruppe sie angezeigt werden.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>Bei der Suchfunktion werden alle Filter der Feldgruppe berücksichtigt, wenn die entsprechenden Felder angezeigt werden. Wenn in einer Abfrage der Suche nicht die erwarteten Ergebnisse angezeigt werden, müssen Sie ggf. die Dublette prüfen, ob Sie keine relevanten Feldgruppen herausfiltern.

## Festlegen eines Schemafelds als Identitätsfeld {#identity-field}

Die Standarddatenstruktur, die Schema bereitstellen, kann genutzt werden, um Daten zu identifizieren, die über mehrere Quellen hinweg zu einer Person gehören. Dies ermöglicht verschiedene nachgelagerte Anwendungsfälle wie Segmentierung, Berichte, Analyse der Datenwissenschaften und mehr. Um Daten basierend auf individuellen Identitäten zu verknüpfen, müssen Schlüsselfelder in den entsprechenden Schemas als [!UICONTROL Identitätsfelder] markiert werden.

[!DNL Experience Platform] erleichtert die Identifizierung eines Identitätsfelds mithilfe eines  **** Identitäts-Kontrollkästchens im  [!DNL Schema Editor]. Sie müssen jedoch festlegen, welches Feld basierend auf der Art Ihrer Daten am besten als Identität verwendet werden soll.

Es kann z. B. Tausende von Treuemitgliedern geben, die zur gleichen Treuestufe gehören, aber jedes Programm des Treueanschlusses hat eine eindeutige `loyaltyId` (in diesem Fall die E-Mail-Adresse des jeweiligen Mitglieds). Die Tatsache, dass `loyaltyId` ein eindeutiger Bezeichner für jedes Mitglied ist, macht es zu einem guten Kandidaten für ein Identitätsfeld, `loyaltyLevel` nicht.

>[!IMPORTANT]
>
>Die folgenden Schritte beschreiben, wie einem vorhandenen Schema-Feld ein Identitätsdeskriptor hinzugefügt wird. Als Alternative zum Definieren von Identitätsfeldern innerhalb der Struktur des Schemas können Sie stattdessen auch ein `identityMap`-Feld verwenden, um Identitätsinformationen zu enthalten.
>
>Wenn Sie `identityMap` verwenden möchten, sollten Sie bedenken, dass dadurch alle primären Identitäten außer Kraft gesetzt werden, die Sie direkt zum Schema hinzufügen. Weitere Informationen finden Sie im Abschnitt zu `identityMap` im [Grundlegendes zum Erstellen von Schemas](../schema/composition.md#identityMap).

Wählen Sie im Abschnitt **[!UICONTROL Struktur]** des Editors das Feld `loyaltyId` und das Kontrollkästchen **[!UICONTROL Identität]** wird unter **[!UICONTROL Feldeigenschaften]** angezeigt. Markieren Sie das Feld und die Option, um dies als **[!UICONTROL Primär identity]** festzulegen. Wählen Sie auch dieses Kontrollkästchen aus.

>[!NOTE]
>
>Jedes Schema darf nur ein primäres Identitätsfeld enthalten. Nachdem ein Schema als primäre Identität festgelegt wurde, erhalten Sie eine Fehlermeldung, wenn Sie später versuchen, ein anderes Identitätsfeld im Schema als primäre Identität festzulegen.

Als Nächstes müssen Sie einen **[!UICONTROL Identity-Namensraum]** aus der Liste vordefinierter Namensraum im Dropdown-Menü angeben. Da `loyaltyId` die E-Mail-Adresse des Kunden ist, wählen Sie &quot;[!UICONTROL E-Mail]&quot;aus der Dropdownliste. Wählen Sie **[!UICONTROL Apply]**, um die Aktualisierungen für das Feld `loyaltyId` zu bestätigen.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Eine Liste der Standarddefinitionen und -definitionen finden Sie in der [[!DNL Identity Service] Dokumentation](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Nach dem Anwenden der Änderung zeigt das Symbol für `loyaltyId` ein Fingerabdrucksymbol an, das angibt, dass es sich jetzt um ein Identitätsfeld handelt.

![](../images/tutorials/create-schema/identity-applied.png)

Jetzt werden alle Daten, die in das Feld `loyaltyId` eingegeben werden, verwendet, um diese Person zu identifizieren und eine Ansicht des Kunden zusammenzufügen. Weitere Informationen zum Arbeiten mit Identitäten in [!DNL Experience Platform] finden Sie in der [[!DNL Identity Service]](../../identity-service/home.md) Dokumentation.

## Schema zur Verwendung in [!DNL Real-time Customer Profile] {#profile} aktivieren

[[!DNL Real-time Customer Profile]](../../profile/home.md) nutzt Identitätsdaten,  [!DNL Experience Platform] um eine ganzheitliche Ansicht der einzelnen Kunden zu ermöglichen. Der Dienst erstellt robuste 360° Profil von Kundenattributen sowie Zeitstempelkonten für jede Interaktion, die Kunden über ein mit [!DNL Experience Platform] integriertes System hatten.

Damit ein Schema für die Verwendung mit [!DNL Real-time Customer Profile] aktiviert werden kann, muss eine primäre Identität definiert sein. Sie erhalten eine Fehlermeldung, wenn Sie versuchen, ein Schema zu aktivieren, ohne vorher eine primäre Identität zu definieren.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Um das Schema &quot;Treuemitglieder&quot;zur Verwendung in [!DNL Profile] zu aktivieren, wählen Sie zunächst &quot;[!DNL Loyalty Members]&quot;im Abschnitt **[!UICONTROL Struktur]**&quot;des Editors aus.

Auf der rechten Seite des Editors werden Informationen zum Schema angezeigt, einschließlich Anzeigename, Beschreibung und Typ. Zusätzlich zu diesen Informationen gibt es eine Umschalter **[!UICONTROL Profil]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Wählen Sie **[!UICONTROL Profil]** aus und es wird ein Popup angezeigt, in dem Sie aufgefordert werden zu bestätigen, dass Sie das Schema für [!DNL Profile] aktivieren möchten.

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Nachdem ein Schema für [!DNL Real-time Customer Profile] aktiviert und gespeichert wurde, kann es nicht deaktiviert werden.

Wählen Sie **[!UICONTROL Aktivieren]**, um Ihre Auswahl zu bestätigen. Sie können den Umschalter **[!UICONTROL Profil]** erneut aktivieren, um das Schema zu deaktivieren, wenn Sie es wünschen. Sobald das Schema jedoch gespeichert wurde, während [!DNL Profile] aktiviert ist, kann es nicht mehr deaktiviert werden.

## Nächste Schritte und zusätzliche Ressourcen

Nachdem Sie das Schema fertig gestellt haben, können Sie das komplette Schema auf der Arbeitsfläche sehen. Wählen Sie **[!UICONTROL Save]** aus, und das Schema wird im Ordner [!DNL Schema Library] gespeichert, damit es über das [!DNL Schema Registry] barrierefrei wird.

Ihr neues Schema kann jetzt verwendet werden, um Daten in [!DNL Platform] zu erfassen. Denken Sie daran, dass nach Verwendung des Schemas zur Datenaufnahme nur noch Ergänzungen vorgenommen werden können. Weitere Informationen zur Schemaversionierung finden Sie in den [Grundlagen der Schema-Komposition](../schema/composition.md).

Sie können nun dem Tutorial [zum Definieren einer Schema-Beziehung in der Benutzeroberfläche](./relationship-ui.md) folgen, um dem Schema &quot;Treuemitglieder&quot;ein neues Beziehungsfeld hinzuzufügen.

Das Schema &quot;Treuemitglieder&quot;steht auch zur Ansicht und Verwaltung mit der [!DNL Schema Registry]-API zur Verfügung. Um mit der API zu arbeiten, lesen Sie den Beginn im [[!DNL Schema Registry API] Entwicklerhandbuch](../api/getting-started.md).

### Videoressourcen

>[!WARNING]
>
>Die in den folgenden Videos dargestellte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

Das folgende Video zeigt, wie Sie ein einfaches Schema in der [!DNL Platform]-Benutzeroberfläche erstellen.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Das folgende Video soll Ihr Verständnis für die Arbeit mit Feldgruppen und -klassen verbessern.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Verwendung von [!DNL Schema Editor].

### Neue Klasse erstellen {#create-new-class}

[!DNL Experience Platform] bietet die Flexibilität, ein Schema auf der Grundlage einer Klasse zu definieren, die eindeutig für Ihr Unternehmen ist. Informationen zum Erstellen einer neuen Klasse finden Sie im Handbuch zum Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche[.](../ui/resources/classes.md#create)

### Klasse eines Schemas ändern {#change-class}

Sie können die Klasse eines Schemas jederzeit während des anfänglichen Kompositionsprozesses ändern, bevor das Schema gespeichert wurde.

>[!WARNING]
>
>Die erneute Zuweisung der Klasse zu einem Schema sollte mit größter Vorsicht erfolgen. Feldgruppen sind nur mit bestimmten Klassen kompatibel. Wenn Sie die Klasse ändern, werden die Arbeitsfläche und alle hinzugefügten Felder zurückgesetzt.

Informationen zum Ändern der Klasse eines Schemas finden Sie im Handbuch [Verwalten von Schemas in der Benutzeroberfläche](../ui/resources/schemas.md).
