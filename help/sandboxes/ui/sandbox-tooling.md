---
title: Sandboxes-Tooling
description: Exportieren und importieren Sie nahtlos Sandbox-Konfigurationen zwischen Sandboxes.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: fea62a2aa3c7d175afbfa808f392c3a93a0d31a0
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 8%

---

# Sandbox-Werkzeuge

>[!NOTE]
>
>Sandbox-Tools sind eine grundlegende Funktion, die beide unterstützt [!DNL Real-Time Customer Data Platform] und [!DNL Journey Optimizer] zur Verbesserung der Effizienz und Konfigurationsgenauigkeit des Entwicklungszyklus.<br><br>Sie benötigen die folgenden beiden rollenbasierten Zugriffssteuerungsberechtigungen, um die Sandbox-Tool-Funktion verwenden zu können:<br>- `manage-sandbox` oder `view-sandbox`<br>- `manage-package`

Verbessern der Konfigurationsgenauigkeit über Sandboxes hinweg und nahtloser Export und Import von Sandbox-Konfigurationen zwischen Sandboxes mit der Sandbox-Tool-Funktion. Verwenden Sie Sandbox-Tools, um die Wertschöpfungszeit für den Implementierungsprozess zu reduzieren und erfolgreiche Konfigurationen über Sandboxes hinweg zu verschieben.

Sie können die Sandbox-Tool-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Ein Paket kann aus einem oder mehreren Objekten bestehen. <!--or an entire sandbox.-->Alle Objekte, die in einem Paket enthalten sind, müssen aus derselben Sandbox stammen.

## Für Sandbox-Tools unterstützte Objekte {#supported-objects}

Die Sandbox-Tool-Funktion bietet Ihnen die Möglichkeit, [!DNL Adobe Real-Time Customer Data Platform] und [!DNL Adobe Journey Optimizer] Objekte in ein Paket.

### Real-time Customer Data Platform-Objekte {#real-time-cdp-objects}

In der folgenden Tabelle sind die [!DNL Adobe Real-Time Customer Data Platform] Objekte, die derzeit für Sandbox-Tools unterstützt werden:

| Plattform | Objekt | Details |
| --- | --- | --- |
| Kundendatenplattform | Quellen | Die Anmeldeinformationen des Quellkontos werden aus Sicherheitsgründen nicht in der Ziel-Sandbox repliziert und müssen daher manuell aktualisiert werden. Der Quelldataflow wird standardmäßig in den Entwurfsstatus kopiert. |
| Kundendatenplattform | Zielgruppen | Nur die **[!UICONTROL Kundenzielgruppe]** type **[!UICONTROL Segmentierungsdienst]** wird unterstützt. Vorhandene Beschriftungen für die Zustimmung und Governance werden im selben Importauftrag kopiert. Das System wählt automatisch die standardmäßige Zusammenführungsrichtlinie in der Ziel-Sandbox mit derselben XDM-Klasse aus, wenn die Abhängigkeiten von Zusammenführungsrichtlinien überprüft werden. |
| Kundendatenplattform | Identitäten | Das System dedupliziert beim Erstellen in der Ziel-Sandbox automatisch Adobe-Standard-Identitäts-Namespaces. Zielgruppen können nur kopiert werden, wenn alle Attribute in Zielgruppenregeln im Vereinigungsschema aktiviert sind. Die erforderlichen Schemata müssen zunächst verschoben und für ein einheitliches Profil aktiviert werden. |
| Kundendatenplattform | Schemata | Vorhandene Beschriftungen für die Zustimmung und Governance werden im selben Importauftrag kopiert. Der Benutzer hat die Flexibilität, Schemas ohne aktivierte Option Unified Profile zu importieren. Die Edge-Groß-/Kleinschreibung für Schemabeziehungen ist nicht im Paket enthalten. |
| Kundendatenplattform | Datensätze | Datensätze werden kopiert, wobei die Einstellung für das einheitliche Profil standardmäßig deaktiviert ist. |
| Kundendatenplattform | Einverständnis und Governance-Richtlinien | Fügen Sie benutzerdefinierte Richtlinien, die von einem Benutzer erstellt wurden, zu einem Paket hinzu und verschieben Sie sie über Sandboxes. |

Die folgenden Objekte werden importiert, befinden sich jedoch im Status Entwurf oder deaktiviert :

| Funktion | Objekt | Status |
| --- | --- | --- |
| Importstatus | Datenfluss der Quelle | Entwurf |
| Importstatus | Journey | Entwurf |
| Unified Profile | Datensatz | Einheitliches Profil deaktiviert |
| Richtlinien | Data Governance-Richtlinien | Deaktiviert |

### Adobe Journey Optimizer-Objekte {#abobe-journey-optimizer-objects}

In der folgenden Tabelle sind die [!DNL Adobe Journey Optimizer] -Objekte, die derzeit für Sandbox-Tools und -Einschränkungen unterstützt werden:

| Plattform | Objekt | Details |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Zielgruppe | Eine Audience kann als abhängiges Objekt des Journey-Objekts kopiert werden. Sie können eine neue Zielgruppe erstellen oder eine vorhandene in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Schema | Die im Journey verwendeten Schemata können als abhängige Objekte kopiert werden. Sie können ein neues Schema erstellen oder ein vorhandenes Schema in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Zusammenführungsrichtlinie | Die im Journey verwendeten Zusammenführungsrichtlinien können als abhängige Objekte kopiert werden. In der Ziel-Sandbox **cannot** eine neue Zusammenführungsrichtlinie erstellen, können Sie nur eine bereits vorhandene nutzen. |
| [!DNL Adobe Journey Optimizer] | Journey – Details der Arbeitsfläche | Die Darstellung der Journey auf der Arbeitsfläche umfasst die Objekte in der Journey, wie z. B. Bedingungen, Aktionen, Ereignisse, Leseregistanzen usw., die kopiert werden. Die Sprungaktivität ist von der Kopie ausgeschlossen. |
| [!DNL Adobe Journey Optimizer] | Ereignis | Die auf der Journey verwendeten Ereignisse und Ereignisdetails werden kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt. |
| [!DNL Adobe Journey Optimizer] | Aktion | E-Mail- und Push-Nachrichten, die auf der Journey verwendet werden, können als abhängige Objekte kopiert werden. Die in den Journey-Feldern verwendeten Kanalaktionsaktivitäten, die zur Personalisierung in der Nachricht verwendet werden, werden nicht auf Vollständigkeit überprüft. Inhaltsbausteine werden nicht kopiert.<br><br>Die auf der Journey verwendete Profilaktion kann kopiert werden. Benutzerdefinierte Aktionen und Aktionsdetails, die auf der Journey verwendet werden, werden ebenfalls kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt. |

Oberflächen (z. B. Vorgaben) werden nicht kopiert. Das System wählt basierend auf dem Nachrichtentyp und dem Oberflächennamen automatisch die nächstmögliche Übereinstimmung in der Ziel-Sandbox aus. Wenn keine Oberflächen in der Ziel-Sandbox gefunden werden, schlägt die Oberflächenkopie fehl, was dazu führt, dass die Nachrichtenkopie fehlschlägt, da für eine Nachricht eine Oberfläche zur Einrichtung verfügbar sein muss. In diesem Fall muss mindestens eine Fläche für den rechten Kanal der Nachricht erstellt werden, damit die Kopie funktioniert.

Benutzerdefinierte Identitätstypen werden beim Exportieren einer Journey nicht als abhängige Objekte unterstützt.

## Exportieren von Objekten in ein Paket {#export-objects}

>[!NOTE]
>
>Alle Exportaktionen werden in den Prüfprotokollen aufgezeichnet.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Entfernen eines Objekts"
>abstract="Um ein Objekt aus dem Paket zu entfernen, wählen Sie die zu entfernende Zeile aus und verwenden Sie dann die Löschoption, die bei der Auswahl zur Verfügung gestellt wird. Beachten Sie, dass Sie keine Objekte aus veröffentlichten Paketen entfernen können."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Ablaufeinstellungen des Pakets"
>abstract="Pakete laufen nach einiger Zeit der Inaktivität im Entwurfsstatus ab. Das standardmäßige Datum ist auf 90 Tage ab heute festgelegt. Dieses Datum verändert sich, bis das Paket veröffentlicht wird. Wenn Sie das Paket morgen im Entwurfsstatus besuchen, wird das Datum um +1 Tag verschoben (es sei denn, Sie legen es manuell fest)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Paketstatus"
>abstract="Standardmäßig ist der Status auf „Entwurf“ gesetzt. Sobald das Paket veröffentlicht wurde, wird der Status in „veröffentlicht“ geändert. Nach der Veröffentlichung des Pakets können keine Änderungen vorgenommen werden."

>[!NOTE]
>
>Sie können ein Package nur importieren, wenn Sie Zugriff auf die Objekte haben.

In diesem Beispiel wird der Export eines Schemas und dessen Hinzufügen zu einem Package dokumentiert. Sie können denselben Prozess verwenden, um andere Objekte zu exportieren, z. B. Datensätze, Journey und viele andere.

### Objekt zu einem neuen Paket hinzufügen {#add-object-to-new-package}

Auswählen **[!UICONTROL Schemas]** aus der linken Navigation und wählen Sie dann die **[!UICONTROL Durchsuchen]** -Tab, in dem die verfügbaren Schemas aufgelistet werden. Wählen Sie als Nächstes die Auslassungszeichen (`...`) neben dem ausgewählten Schema und eine Dropdown-Liste zeigt Steuerelemente an. Auswählen **[!UICONTROL Zu Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata, die das Dropdown-Menü anzeigen, in dem die [!UICONTROL Zu Paket hinzufügen] Kontrolle.](../images/ui/sandbox-tooling/add-to-package.png)

Aus dem **[!UICONTROL Zu Paket hinzufügen]** wählen Sie das **[!UICONTROL Neues Paket erstellen]** -Option. Stellen Sie eine [!UICONTROL Name] für Ihr Paket und optional [!UICONTROL Beschreibung], wählen Sie **[!UICONTROL Hinzufügen]**.

![Die [!UICONTROL Zu Paket hinzufügen] Dialogfeld mit [!UICONTROL Neues Paket erstellen] ausgewählte und hervorgehobene Elemente [!UICONTROL Hinzufügen].](../images/ui/sandbox-tooling/create-new-package.png)

Sie kehren zum **[!UICONTROL Schemas]** Umgebung. Sie können dem von Ihnen erstellten Package jetzt zusätzliche Objekte hinzufügen, indem Sie die folgenden Schritte ausführen.

### Hinzufügen eines Objekts zu einem vorhandenen Paket und Veröffentlichen {#add-object-to-existing-package}

Um eine Liste der verfügbaren Schemata anzuzeigen, wählen Sie **[!UICONTROL Schemas]** aus der linken Navigation und wählen Sie dann die **[!UICONTROL Durchsuchen]** Registerkarte. Wählen Sie als Nächstes die Auslassungszeichen (`...`) neben dem ausgewählten Schema, um die Kontrolloptionen in einem Dropdown-Menü anzuzeigen. Auswählen **[!UICONTROL Zu Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata, die das Dropdown-Menü anzeigen, in dem die [!UICONTROL Zu Paket hinzufügen] Kontrolle.](../images/ui/sandbox-tooling/add-to-package.png)

Die **[!UICONTROL Zu Paket hinzufügen]** angezeigt. Wählen Sie die **[!UICONTROL Vorhandenes Paket]** und wählen Sie anschließend die **[!UICONTROL Paketname]** und wählen Sie das gewünschte Paket aus. Wählen Sie abschließend **[!UICONTROL Hinzufügen]** um Ihre Auswahl zu bestätigen.

![[!UICONTROL Zu Paket hinzufügen] angezeigt, um ein ausgewähltes Paket aus der Dropdown-Liste anzuzeigen.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Die Liste der dem Paket hinzugefügten Objekte wird aufgelistet. Um das Paket zu veröffentlichen und es für den Import in Sandboxes verfügbar zu machen, wählen Sie **[!UICONTROL Veröffentlichen]**.

![Eine Liste der Objekte im Paket, die die [!UICONTROL Veröffentlichen] -Option.](../images/ui/sandbox-tooling/publish-package.png)

Auswählen **[!UICONTROL Veröffentlichen]** zur Bestätigung der Veröffentlichung des Pakets.

![Veröffentlichen Sie das Bestätigungsdialogfeld für das Paket, indem Sie die [!UICONTROL Veröffentlichen] -Option.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nach der Veröffentlichung kann der Inhalt des Pakets nicht mehr geändert werden. Um Kompatibilitätsprobleme zu vermeiden, stellen Sie sicher, dass alle erforderlichen Assets ausgewählt wurden. Wenn Änderungen vorgenommen werden müssen, müssen Sie ein neues Paket erstellen.

Sie kehren zum **[!UICONTROL Pakete]** im [!UICONTROL Sandboxes] Umgebung, in der das neue veröffentlichte Paket angezeigt wird.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/published-packages.png)

## Importieren eines Pakets in eine Ziel-Sandbox {#import-package-to-target-sandbox}

>[!NOTE]
>
>Alle Importaktionen werden in den Prüfprotokollen aufgezeichnet.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zu den Sandboxes . **[!UICONTROL Durchsuchen]** und wählen Sie das Pluszeichen (+) neben dem Sandbox-Namen aus.

![Die Sandboxes **[!UICONTROL Durchsuchen]** -Tab, der die Auswahl des Importpakets markiert.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Wählen Sie im Dropdown-Menü die **[!UICONTROL Paketname]** Sie möchten in die Ziel-Sandbox importieren. Hinzufügen einer **[!UICONTROL Auftragsname]**, der für die künftige Überwachung verwendet wird. Standardmäßig wird das einheitliche Profil beim Importieren der Schemata des Pakets deaktiviert. Umschalten **Aktivieren von Schemata für Profile** Um dies zu aktivieren, wählen Sie **[!UICONTROL Nächste]**.

![Auf der Seite mit den Importdetails wird die [!UICONTROL Paketname] Dropdown-Auswahl](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

Die [!UICONTROL Paketobjekt und Abhängigkeiten] -Seite enthält eine Liste aller in diesem Paket enthaltenen Assets. Das System erkennt automatisch abhängige Objekte, die für den erfolgreichen Import ausgewählter übergeordneter Objekte erforderlich sind. Alle fehlenden Attribute werden oben auf der Seite angezeigt. Auswählen **[!UICONTROL Details anzeigen]** für eine detailliertere Aufschlüsselung.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] -Seite zeigt fehlende Attribute an.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Abhängige Objekte können in der Ziel-Sandbox durch vorhandene ersetzt werden, sodass Sie vorhandene Objekte wiederverwenden können, anstatt eine neue Version zu erstellen. Wenn Sie beispielsweise ein Paket mit Schemas importieren, können Sie vorhandene benutzerdefinierte Feldergruppen und Identitäts-Namespaces in der Ziel-Sandbox wiederverwenden. Alternativ können Sie beim Importieren eines Pakets mit Journey bestehende Segmente in der Ziel-Sandbox wiederverwenden.

Um ein vorhandenes Objekt zu verwenden, wählen Sie das Stiftsymbol neben dem abhängigen Objekt aus.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] zeigt eine Liste der im Paket enthaltenen Assets an.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Die Optionen zum Erstellen neuer oder Verwenden vorhandener Elemente werden angezeigt. Auswählen **[!UICONTROL Vorhandene verwenden]**.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite mit abhängigen Objektoptionen [!UICONTROL Neu erstellen] und [!UICONTROL Vorhandene verwenden].](../images/ui/sandbox-tooling/use-existing-object.png)

Die **[!UICONTROL Feldergruppe]** zeigt eine Liste von Feldergruppen an, die für das Objekt verfügbar sind. Wählen Sie die erforderlichen Feldergruppen aus und klicken Sie auf **[!UICONTROL Speichern]**.

![Eine Liste der Felder, die im [!UICONTROL Feldergruppe] Dialog, das die [!UICONTROL Speichern] auswählen. ](../images/ui/sandbox-tooling/field-group-list.png)

Sie kehren zum [!UICONTROL Paketobjekt und Abhängigkeiten] Seite. Wählen Sie von hier aus **[!UICONTROL Beenden]** , um den Package-Import abzuschließen.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite zeigt eine Liste der im Paket enthaltenen Assets, die hervorgehoben werden [!UICONTROL Beenden].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportieren und Importieren einer gesamten Sandbox

>[!NOTE]
>
>Derzeit werden beim Exportieren oder Importieren einer gesamten Sandbox nur Real-time Customer Data Platform-Objekte unterstützt. Adobe Journey Optimizer-Objekte wie Journey werden derzeit nicht unterstützt.

Sie können alle unterstützten Objekttypen in ein vollständiges Sandbox-Paket exportieren und dann das Paket über verschiedene Sandboxes importieren, um Objektkonfigurationen zu replizieren. Diese Funktion ermöglicht beispielsweise Folgendes:

- Importieren Sie eine Sandbox erneut, um alle Objektkonfigurationen zu reproduzieren, wenn Sie die Sandbox zurücksetzen müssen.
- Importieren Sie das Paket in andere Sandboxes und nutzen Sie es als Blueprint-Sandbox, um den Entwicklungsprozess zu beschleunigen.

### Gesamte Sandbox exportieren {#export-entire-sandbox}

Um eine gesamte Sandbox zu exportieren, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** Registerkarte und wählen Sie **[!UICONTROL Package erstellen]**.

![Die [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** Tabulatorhervorhebung [!UICONTROL Package erstellen].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Auswählen **[!UICONTROL Gesamte Sandbox]** für die [!UICONTROL Package-Typ] im [!UICONTROL Package erstellen] angezeigt. Stellen Sie eine [!UICONTROL Paketname] für Ihr neues Paket und wählen Sie die **[!UICONTROL Sandbox]** aus dem Dropdown-Menü aus. Wählen Sie abschließend **[!UICONTROL Erstellen]** um Ihre Einträge zu bestätigen.

![Die [!UICONTROL Package erstellen] Dialogfeld mit ausgefüllten Feldern und Markierung [!UICONTROL Erstellen].](../images/ui/sandbox-tooling/create-package-dialog.png)

Das Paket wurde erfolgreich erstellt, wählen Sie **[!UICONTROL Veröffentlichen]** um das Paket zu veröffentlichen.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Sie kehren zum **[!UICONTROL Pakete]** im [!UICONTROL Sandboxes] Umgebung, in der das neue veröffentlichte Paket angezeigt wird.

### Importieren des gesamten Sandbox-Pakets {#import-entire-sandbox-package}

>[!NOTE]
>
>Alle Objekte werden als neue Objekte in die Ziel-Sandbox importiert. Es empfiehlt sich, ein vollständiges Sandbox-Paket in eine leere Sandbox zu importieren.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Durchsuchen]** und wählen Sie das Pluszeichen (+) neben dem Sandbox-Namen aus.

![Die Sandboxes **[!UICONTROL Durchsuchen]** -Tab, der die Auswahl des Importpakets markiert.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Wählen Sie über das Dropdown-Menü die vollständige Sandbox mithilfe der **[!UICONTROL Paketname]** Dropdown. Hinzufügen einer **[!UICONTROL Auftragsname]**, die für die künftige Überwachung verwendet wird, und ein optionales **[!UICONTROL Auftragsbeschreibung]**, wählen Sie **[!UICONTROL Nächste]**.

![Auf der Seite mit den Importdetails wird die [!UICONTROL Paketname] Dropdown-Auswahl](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Sie müssen über vollständige Berechtigungen für alle im Paket enthaltenen Objekte verfügen. Wenn Sie keine Berechtigungen haben, schlägt der Importvorgang fehl und es werden Fehlermeldungen angezeigt.

Sie werden zum [!UICONTROL Paketobjekt und Abhängigkeiten] -Seite, auf der Sie die Anzahl der Objekte und Abhängigkeiten sehen können, die importiert und ausgeschlossen werden. Wählen Sie von hier aus **[!UICONTROL Import]** , um den Package-Import abzuschließen.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite zeigt die Inline-Meldung der nicht unterstützten Objekttypen an, Hervorhebung [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Warten Sie etwas, bis der Import abgeschlossen ist. Die Zeit zum Abschließen kann je nach der Anzahl der Objekte im Paket variieren. Sie können den Importauftrag über die [!UICONTROL Sandboxes] **[!UICONTROL Aufträge]** Registerkarte.

## Importdetails überwachen {#view-import-details}

Um die importierten Details anzuzeigen, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Aufträge]** und wählen Sie das Paket aus der Liste aus. Alternativ können Sie die Suchleiste verwenden, um nach dem Paket zu suchen.

![Die Sandboxes [!UICONTROL Aufträge] markiert die Auswahl des Importpakets.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Auswählen **[!UICONTROL Importzusammenfassung anzeigen]** im rechten Detailbereich im **[!UICONTROL Aufträge]** in der Sandbox-Umgebung.

![Die Sandboxes [!UICONTROL Importe] hervorgehobene Registerkarte [!UICONTROL Importdetails anzeigen] Auswahl im rechten Bereich.](../images/ui/sandbox-tooling/view-import-details.png)

Die **[!UICONTROL Importzusammenfassung]** zeigt eine Aufschlüsselung der Importe mit Fortschritt in Prozent an.

>[!NOTE]
>
>Sie können eine Liste von Objekten anzeigen, indem Sie zu bestimmten Inventarseiten navigieren.

![Die [!UICONTROL Importdetails] -Dialogfeld mit einer detaillierten Aufschlüsselung der Importe.](../images/ui/sandbox-tooling/import-details.png)

Nach Abschluss des Imports wird eine Benachrichtigung in der Platform-Benutzeroberfläche empfangen. Sie können auf diese Benachrichtigungen über das Warnungssymbol zugreifen. Sie können von hier aus zur Fehlerbehebung navigieren, wenn ein Auftrag nicht erfolgreich war.

## Video-Tutorial

Das folgende Video soll Ihnen dabei helfen, die Sandbox-Tools zu verstehen, und beschreibt, wie Sie ein neues Paket erstellen, ein Paket veröffentlichen und ein Paket importieren.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Nächste Schritte

In diesem Dokument erfahren Sie, wie Sie die Sandbox-Tool-Funktion in der Experience Platform-Benutzeroberfläche verwenden. Informationen zu Sandboxes finden Sie unter [Sandbox-Benutzerhandbuch](../ui/user-guide.md).

Anweisungen zum Ausführen verschiedener Vorgänge mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md). Eine allgemeine Übersicht über Sandboxes im Experience Platform finden Sie im Abschnitt [Übersichtsdokumentation](../home.md).
