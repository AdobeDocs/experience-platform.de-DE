---
title: Adobe Experience Cloud Identity Service-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Experience Cloud Identity Service“ in Adobe Experience Platform vertraut.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 100%

---

# Adobe Experience Cloud Identity Service-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

In dieser Referenz finden Sie Informationen dazu, wie Sie die Adobe Experience Cloud ID-Erweiterung konfigurieren, sowie zu den Optionen, die für die Erstellung einer Regel mithilfe dieser Erweiterung zur Verfügung stehen.

Verwenden Sie diese Erweiterung, um den Experience Cloud Identity Service in Ihre Eigenschaft zu integrieren. Mit dem Experience Cloud Identity Service können Sie eindeutige und dauerhafte Bezeichner für Besucher Ihrer Site erstellen und speichern.

## Experience Cloud ID-Erweiterung konfigurieren

Dieser Abschnitt enthält eine Referenz zu den verfügbaren Optionen beim Konfigurieren der Experience Cloud ID-Erweiterung.

Wenn die Experience Cloud ID-Erweiterung noch nicht installiert ist, öffnen Sie die Eigenschaft, klicken Sie auf **[!UICONTROL Erweiterungen > Katalog]**, bewegen Sie den Mauszeiger über die Experience Cloud ID-Erweiterung und klicken Sie auf **[!UICONTROL Installieren]**.

Öffnen Sie zum Konfigurieren der Erweiterung die Registerkarte „Erweiterungen“, bewegen Sie den Mauszeiger über die Erweiterung und wählen Sie dann **[!UICONTROL Konfigurieren]** aus.

![](../../../images/optin.jpg)

Die folgenden Konfigurationsoptionen sind verfügbar:

### Experience Cloud-Organisations-ID

Die ID für Ihre Experience Cloud-Organisation.

Ihre ID besteht aus einer 24-stelligen alphanumerischen Zeichenfolge gefolgt von `@AdobeOrg`. Wenn Sie diese ID nicht kennen, wenden Sie sich an den Kundendienst.

### Ausschließen spezifischer Pfade

Die Experience Cloud ID wird nicht geladen, wenn die URL mit einem der angegebenen Pfade übereinstimmt.

(Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

Klicken Sie auf **[!UICONTROL Hinzufügen]**, um einen weiteren Pfad auszuschließen.

### Aktivieren

Verwenden Sie die Opt-in-Optionen, um festzulegen, ob für Besucher ein Opt-in für Adobe-Dienste auf Ihrer Site erforderlich ist, was auch die Festlegung beinhaltet, ob Cookies zum Tracking der Besucheraktivität erstellt werden sollen.

Das Opt-in ist der zentrale Bezugspunkt für alle Client-seitigen Bibliotheken, wenn es darum geht, festzulegen, ob Cookies beim Besuch Ihrer Site auf dem Gerät oder Browser eines Benutzers erstellt werden können. Das Opt-in bietet keine Unterstützung für die Erfassung oder Speicherung von Voreinstellungen bezüglich der Benutzerzustimmung.

**Opt-in aktivieren?**

Die ausgewählte Option bestimmt, ob Ihre Website auf die Zustimmung zum Tracking der Aktivitäten eines Besuchers auf Ihrer Website wartet.

Es gibt drei Möglichkeiten:

* **Nein:** Wartet nicht auf die Zustimmung zum Tracking des Besuchers. Dies ist das Standardverhalten, wenn Sie keine Option auswählen.
* **Ja:** Wartet auf die Zustimmung zum Tracking des Besuchers.
* **Bestimmt zur Laufzeit mit Funktion:** Legen Sie programmgesteuert fest, ob der Wert zur Laufzeit „true“ oder „false“ ist. Wenn Sie diese Option auswählen, ist das Feld „Datenelement auswählen“ verfügbar. Wählen Sie ein Datenelement aus, das bestimmen kann, ob auf die Zustimmung gewartet werden soll. Dieses Datenelement wird in einen booleschen Wert aufgelöst. Sie können beispielsweise ein Datenelement für die Zustimmung auswählen, je nachdem, ob sich das Land des Besuchers in der EU befindet.

**Ist Opt-in-Speicher aktiviert?**

Sofern aktiviert, wird die Zustimmung in einem Erstanbieter-Cookie in Ihrer Domain gespeichert. Wenn die Option nicht aktiviert ist, werden die Einstellungen zur Zustimmung im CMP oder in einem von Ihnen verwalteten Cookie bewahrt.

**Opt-in-Cookie-Domain?**

Verwenden Sie diese optionale Einstellung, um die Domain anzugeben, in der das Opt-in-Cookie gespeichert wird, wenn die Speicherung aktiviert ist. Sie können eine Domain eingeben oder ein Datenelement auswählen, das die Domain enthält.

**Ablaufdatum des Opt-in-Speichers?**

Geben Sie in Sekunden an, wann das Opt-in-Cookie abläuft, wenn die Speicherung aktiviert ist.

Geben Sie eine Zahl ein und wählen Sie dann eine Zeiteinheit aus dem Dropdown-Menü. Geben Sie beispielsweise „2“ ein und wählen Sie **[!UICONTROL Wochen]**. Der Standardwert ist 13 Monate.

**Berechtigungen?**

Bisherige Zustimmung an die Opt-in-Bibliothek übergeben. Wählen Sie ein Datenelement, das die Zustimmung enthält. Der Elementtyp muss ein Objekt oder eine JSON-Zeichenfolge sein. Überschreibt Vorab-Opt-in-Genehmigungen.

Beispiel:

`"{"aa":true,"aam":true,"ecid":true}"`

**Vorab-Opt-in-Genehmigungen?**

Definieren Sie, welche Kategorien genehmigt oder abgelehnt werden, wenn vom Besucher keine Voreinstellung festgelegt wurde. Von einer Zustimmung wird für die ausgewählten Lösungen ab dem Ladezeitpunkt der Seite ausgegangen. Der Elementtyp muss ein Objekt oder eine JSON-Zeichenfolge sein (Beispiel: `{aam: true}`).

### Variablen

Legen Sie Name-Wert-Paare als Experience Cloud ID-Instanzeigenschaften fest. Wählen Sie mithilfe des Dropdown-Menüs eine Variable aus. Geben Sie dann einen Wert ein oder wählen Sie einen Wert aus. Informationen zu den einzelnen Variablen finden Sie in der [Dokumentation zum Experience Cloud Identity Service](https://experiencecloud.adobe.com/resources/help/de_DE/mcvid/mcvid-overview.html).

## Aktionstypen für die Experience Cloud ID-Erweiterung

In diesem Abschnitt werden die in der Experience Cloud ID-Erweiterung verfügbaren Aktionstypen beschrieben.

### Aktionstypen

#### Festlegen von Kunden-IDs

Legen Sie eine oder mehrere Kunden-IDs fest.

1. Geben Sie den Integrationscode ein.

   Der Integrationscode sollte den Wert enthalten, der im Audience Manager oder in Kundenattributen als Datenquelle festgelegt wurde.

1. Wählen Sie einen Wert aus.

   Bei dem Wert sollte es sich um eine Benutzer-ID handeln. Datenelemente sind am besten für dynamische Werte wie IDs von einem clientspezifischen internen System geeignet.

1. Wählen Sie einen Authentifizierungsstatus aus.

   Verfügbare Optionen sind:

   * „Unbekannt“
   * Authentifiziert
   * Abgemeldet

1. (Optional) Klicken Sie auf **[!UICONTROL Hinzufügen]**, um weitere Kunden-IDs festzulegen.
1. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus.
