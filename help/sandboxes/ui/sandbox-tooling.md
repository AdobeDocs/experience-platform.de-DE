---
title: Sandbox-Tooling
description: Exportieren und importieren Sie nahtlos Sandbox-Konfigurationen zwischen Sandboxes.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 209aaaf0c2bfdb321f75257309980c7a48cb1eb4
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 8%

---

# Sandbox-Werkzeuge

>[!NOTE]
>
>Sandbox-Tools sind eine grundlegende Funktion, die sowohl [!DNL Real-Time Customer Data Platform] als auch [!DNL Journey Optimizer] unterstützt, um die Effizienz und Konfigurationsgenauigkeit des Entwicklungszyklus zu verbessern.<br><br>Sie müssen über die folgenden beiden rollenbasierten Zugriffssteuerungsberechtigungen verfügen, um die Sandbox-Tool-Funktion verwenden zu können:<br>- `manage-sandbox` oder `view-sandbox`<br>- `manage-package`

Verbessern der Konfigurationsgenauigkeit über Sandboxes hinweg und nahtloser Export und Import von Sandbox-Konfigurationen zwischen Sandboxes mit der Sandbox-Tool-Funktion. Verwenden Sie Sandbox-Tools, um die Wertschöpfungszeit für den Implementierungsprozess zu reduzieren und erfolgreiche Konfigurationen über Sandboxes hinweg zu verschieben.

Sie können die Sandbox-Tool-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Ein Paket kann aus einem oder mehreren Objekten bestehen. <!--or an entire sandbox.-->Alle Objekte, die in einem Paket enthalten sind, müssen aus derselben Sandbox stammen.

## Für Sandbox-Tools unterstützte Objekte {#supported-objects}

Die Sandbox-Tool-Funktion bietet Ihnen die Möglichkeit, [!DNL Adobe Real-Time Customer Data Platform] - und [!DNL Adobe Journey Optimizer] -Objekte in ein Paket zu exportieren.

### Real-time Customer Data Platform-Objekte {#real-time-cdp-objects}

In der folgenden Tabelle sind [!DNL Adobe Real-Time Customer Data Platform] -Objekte aufgeführt, die derzeit für Sandbox-Tools unterstützt werden:

| Plattform | Objekt | Details |
| --- | --- | --- |
| Kundendatenplattform | Quellen | Die Anmeldeinformationen des Quellkontos werden aus Sicherheitsgründen nicht in der Ziel-Sandbox repliziert und müssen daher manuell aktualisiert werden. Der Quelldataflow wird standardmäßig in den Entwurfsstatus kopiert. |
| Kundendatenplattform | Zielgruppen | Nur der **[!UICONTROL Kunden-Audience]**-Typ **[!UICONTROL Segmentierungsdienst]** wird unterstützt. Vorhandene Beschriftungen für die Zustimmung und Governance werden im selben Importauftrag kopiert. Das System wählt automatisch die standardmäßige Zusammenführungsrichtlinie in der Ziel-Sandbox mit derselben XDM-Klasse aus, wenn die Abhängigkeiten von Zusammenführungsrichtlinien überprüft werden. |
| Kundendatenplattform | Identitäten | Das System dedupliziert beim Erstellen in der Ziel-Sandbox automatisch Adobe-Standard-Identitäts-Namespaces. Zielgruppen können nur kopiert werden, wenn alle Attribute in Zielgruppenregeln im Vereinigungsschema aktiviert sind. Die erforderlichen Schemata müssen zunächst verschoben und für ein einheitliches Profil aktiviert werden. |
| Kundendatenplattform | Schemata | Vorhandene Beschriftungen für die Zustimmung und Governance werden im selben Importauftrag kopiert. Der Benutzer hat die Flexibilität, Schemas ohne aktivierte Option Unified Profile zu importieren. Die Edge-Groß-/Kleinschreibung für Schemabeziehungen ist nicht im Paket enthalten. |
| Kundendatenplattform | Datensätze | Datensätze werden kopiert, wobei die Einstellung für das einheitliche Profil standardmäßig deaktiviert ist. |
| Kundendatenplattform | Einverständnis und Governance-Richtlinien | Fügen Sie benutzerdefinierte Richtlinien, die von einem Benutzer erstellt wurden, zu einem Paket hinzu und verschieben Sie sie über Sandboxes. |

Die folgenden Objekte werden importiert, befinden sich jedoch im Status Entwurf oder deaktiviert :

| Funktion | Objekt | Status |
| --- | --- | --- |
| Importstatus | Source-Datenfluss | Entwurf |
| Importstatus | Journey | Entwurf |
| Einheitliches Profil | Datensatz | Einheitliches Profil deaktiviert |
| Richtlinien | Data Governance-Richtlinien | Deaktiviert |

### Adobe Journey Optimizer-Objekte {#abobe-journey-optimizer-objects}

In der folgenden Tabelle sind [!DNL Adobe Journey Optimizer] -Objekte aufgeführt, die derzeit für Sandbox-Tools und -Einschränkungen unterstützt werden:

| Plattform | Objekt | Details |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Zielgruppe | Eine Audience kann als abhängiges Objekt des Journey-Objekts kopiert werden. Sie können eine neue Zielgruppe erstellen oder eine vorhandene in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Schema | Die im Journey verwendeten Schemata können als abhängige Objekte kopiert werden. Sie können ein neues Schema erstellen oder ein vorhandenes Schema in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Zusammenführungsrichtlinie | Die im Journey verwendeten Zusammenführungsrichtlinien können als abhängige Objekte kopiert werden. In der Ziel-Sandbox können Sie **nicht** eine neue Zusammenführungsrichtlinie erstellen. Sie können nur eine bereits vorhandene nutzen. |
| [!DNL Adobe Journey Optimizer] | Journey – Details der Arbeitsfläche | Die Darstellung der Journey auf der Arbeitsfläche umfasst die Objekte in der Journey, wie z. B. Bedingungen, Aktionen, Ereignisse, Leseregistanzen usw., die kopiert werden. Die Sprungaktivität ist von der Kopie ausgeschlossen. |
| [!DNL Adobe Journey Optimizer] | Ereignis | Die auf der Journey verwendeten Ereignisse und Ereignisdetails werden kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt. |
| [!DNL Adobe Journey Optimizer] | Aktion | E-Mail- und Push-Nachrichten, die auf der Journey verwendet werden, können als abhängige Objekte kopiert werden. Die in den Journey-Feldern verwendeten Kanalaktionsaktivitäten, die zur Personalisierung in der Nachricht verwendet werden, werden nicht auf Vollständigkeit überprüft. Inhaltsbausteine werden nicht kopiert.<br><br>Die auf dem Journey verwendete Profilaktion &quot;Aktualisieren&quot;kann kopiert werden. Benutzerdefinierte Aktionen und Aktionsdetails, die auf der Journey verwendet werden, werden ebenfalls kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt. |
| [!DNL Adobe Journey Optimizer] | Journey | Durch Hinzufügen einer ganzen Journey zu einem Package werden die meisten Objekte, von denen die Journey abhängig ist, kopiert, einschließlich Zielgruppen, Schemata, Ereignisse und Aktionen. |
| [!DNL Adobe Journey Optimizer] | Inhaltsvorlage | Eine Inhaltsvorlage kann als abhängiges Objekt des Journey-Objekts kopiert werden. Eigenständige Vorlagen ermöglichen die einfache Wiederverwendung benutzerdefinierter Inhalte in allen Journey Optimizer-Kampagnen und -Journey. |
| [!DNL Adobe Journey Optimizer] | Fragment | Ein Fragment kann als abhängiges Objekt des Journey-Objekts kopiert werden. Fragmente sind wiederverwendbare Komponenten, die in einer oder mehreren E-Mails in Journey Optimizer-Kampagnen und -Journey referenziert werden können. |

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

Wählen Sie im linken Navigationsbereich **[!UICONTROL Schemas]** und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus, auf der die verfügbaren Schemas aufgelistet werden. Wählen Sie als Nächstes die Auslassungszeichen (`...`) neben dem ausgewählten Schema aus und ein Dropdown-Menü zeigt Steuerelemente an. Wählen Sie **[!UICONTROL Zu Paket hinzufügen]** aus der Dropdown-Liste aus.

![Liste der Schemas mit dem Dropdown-Menü, das das Steuerelement [!UICONTROL Zu Package hinzufügen] markiert.](../images/ui/sandbox-tooling/add-to-package.png)

Wählen Sie im Dialogfeld **[!UICONTROL Zu Paket hinzufügen]** die Option **[!UICONTROL Neues Paket erstellen]** aus. Geben Sie einen [!UICONTROL Namen] für Ihr Paket und eine optionale [!UICONTROL Beschreibung] ein und wählen Sie dann **[!UICONTROL Hinzufügen]** aus.

![Das Dialogfeld [!UICONTROL Zu Paket hinzufügen] mit ausgewähltem [!UICONTROL Neues Paket erstellen] und Markierung von [!UICONTROL Hinzufügen]](../images/ui/sandbox-tooling/create-new-package.png).

Sie werden zur Umgebung **[!UICONTROL Schemas]** zurückgegeben. Sie können dem von Ihnen erstellten Package jetzt zusätzliche Objekte hinzufügen, indem Sie die folgenden Schritte ausführen.

### Hinzufügen eines Objekts zu einem vorhandenen Paket und Veröffentlichen {#add-object-to-existing-package}

Um eine Liste der verfügbaren Schemas anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Schemas]** und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus. Wählen Sie dann die Auslassungszeichen (`...`) neben dem ausgewählten Schema aus, um die Kontrolloptionen in einem Dropdown-Menü anzuzeigen. Wählen Sie **[!UICONTROL Zu Paket hinzufügen]** aus der Dropdown-Liste aus.

![Liste der Schemas mit dem Dropdown-Menü, das das Steuerelement [!UICONTROL Zu Package hinzufügen] markiert.](../images/ui/sandbox-tooling/add-to-package.png)

Das Dialogfeld **[!UICONTROL Zu Paket hinzufügen]** wird angezeigt. Wählen Sie die Option **[!UICONTROL Vorhandenes Paket]** aus, wählen Sie dann das Dropdown-Menü **[!UICONTROL Paketname]** aus und wählen Sie das erforderliche Paket aus. Wählen Sie abschließend **[!UICONTROL Hinzufügen]** aus, um Ihre Auswahl zu bestätigen.

Dialogfeld ![[!UICONTROL Zum Paket hinzufügen] , in dem ein ausgewähltes Paket aus der Dropdown-Liste angezeigt wird.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Die Liste der dem Paket hinzugefügten Objekte wird aufgelistet. Um das Paket zu veröffentlichen und es für den Import in Sandboxes verfügbar zu machen, wählen Sie **[!UICONTROL Publish]** aus.

![Eine Liste der Objekte im Paket, die die Option [!UICONTROL Publish] hervorheben.](../images/ui/sandbox-tooling/publish-package.png)

Wählen Sie **[!UICONTROL Publish]** aus, um die Veröffentlichung des Pakets zu bestätigen.

![Publish-Paketbestätigungsdialogfeld, in dem die Option [!UICONTROL Publish] hervorgehoben wird.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nach der Veröffentlichung kann der Inhalt des Pakets nicht mehr geändert werden. Um Kompatibilitätsprobleme zu vermeiden, stellen Sie sicher, dass alle erforderlichen Assets ausgewählt wurden. Wenn Änderungen vorgenommen werden müssen, müssen Sie ein neues Paket erstellen.

Sie werden zur Registerkarte **[!UICONTROL Pakete]** in der Umgebung [!UICONTROL Sandboxes] zurückgeleitet, wo Sie das neue veröffentlichte Paket sehen können.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/published-packages.png)

## Importieren eines Pakets in eine Ziel-Sandbox {#import-package-to-target-sandbox}

>[!NOTE]
>
>Alle Importaktionen werden in den Prüfprotokollen aufgezeichnet.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zur Registerkarte Sandboxes **[!UICONTROL Durchsuchen]** und wählen Sie die Plusoption (+) neben dem Sandbox-Namen aus.

![Die Registerkarte &quot;Sandboxes **[!UICONTROL Durchsuchen]**&quot;, auf der die Auswahl des Importpakets hervorgehoben wird.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Wählen Sie im Dropdown-Menü den **[!UICONTROL Paketnamen]** aus, den Sie in die Ziel-Sandbox importieren möchten. Fügen Sie einen **[!UICONTROL Auftragsnamen]** hinzu, der für die zukünftige Überwachung verwendet wird. Standardmäßig wird das einheitliche Profil beim Importieren der Schemata des Pakets deaktiviert. Schalten Sie **Schemas für Profil aktivieren** um, um dies zu aktivieren, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Die Seite mit den Importdetails, auf der die Dropdown-Auswahl [!UICONTROL Paketname]](../images/ui/sandbox-tooling/import-package-to-sandbox.png) angezeigt wird

Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] enthält eine Liste aller in diesem Paket enthaltenen Assets. Das System erkennt automatisch abhängige Objekte, die für den erfolgreichen Import ausgewählter übergeordneter Objekte erforderlich sind. Alle fehlenden Attribute werden oben auf der Seite angezeigt. Wählen Sie **[!UICONTROL Details anzeigen]** aus, um eine detailliertere Aufschlüsselung anzuzeigen.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] enthält fehlende Attribute.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Abhängige Objekte können in der Ziel-Sandbox durch vorhandene ersetzt werden, sodass Sie vorhandene Objekte wiederverwenden können, anstatt eine neue Version zu erstellen. Wenn Sie beispielsweise ein Paket mit Schemas importieren, können Sie vorhandene benutzerdefinierte Feldergruppen und Identitäts-Namespaces in der Ziel-Sandbox wiederverwenden. Alternativ können Sie beim Importieren eines Pakets mit Journey bestehende Segmente in der Ziel-Sandbox wiederverwenden.

Um ein vorhandenes Objekt zu verwenden, wählen Sie das Stiftsymbol neben dem abhängigen Objekt aus.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] enthält eine Liste der im Paket enthaltenen Assets.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Die Optionen zum Erstellen neuer oder Verwenden vorhandener Elemente werden angezeigt. Wählen Sie **[!UICONTROL Vorhandenen]** verwenden aus.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] mit den abhängigen Objektoptionen [!UICONTROL Neu erstellen] und [!UICONTROL Vorhandene verwenden]](../images/ui/sandbox-tooling/use-existing-object.png).

Das Dialogfeld **[!UICONTROL Feldergruppe]** enthält eine Liste der für das Objekt verfügbaren Feldergruppen. Wählen Sie die erforderlichen Feldergruppen und dann **[!UICONTROL Speichern]** aus.

![Eine Liste von Feldern, die im Dialogfeld [!UICONTROL Feldergruppe] angezeigt werden und die Auswahl [!UICONTROL Speichern] markieren. ](../images/ui/sandbox-tooling/field-group-list.png)

Sie werden zur Seite [!UICONTROL Paketobjekt und Abhängigkeiten] zurückgegeben. Wählen Sie hier **[!UICONTROL Fertigstellen]** aus, um den Package-Import abzuschließen.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] enthält eine Liste der im Paket enthaltenen Assets, in der [!UICONTROL Beenden]](../images/ui/sandbox-tooling/finish-object-dependencies.png) hervorgehoben wird.

## Exportieren und Importieren einer gesamten Sandbox

>[!NOTE]
>
>Derzeit werden beim Exportieren oder Importieren einer gesamten Sandbox nur Real-time Customer Data Platform-Objekte unterstützt. Adobe Journey Optimizer-Objekte wie Journey werden derzeit nicht unterstützt.

Sie können alle unterstützten Objekttypen in ein vollständiges Sandbox-Paket exportieren und dann das Paket über verschiedene Sandboxes importieren, um Objektkonfigurationen zu replizieren. Diese Funktion ermöglicht beispielsweise Folgendes:

- Importieren Sie eine Sandbox erneut, um alle Objektkonfigurationen zu reproduzieren, wenn Sie die Sandbox zurücksetzen müssen.
- Importieren Sie das Paket in andere Sandboxes und nutzen Sie es als Blueprint-Sandbox, um den Entwicklungsprozess zu beschleunigen.

### Gesamte Sandbox exportieren {#export-entire-sandbox}

Um eine gesamte Sandbox zu exportieren, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** und wählen Sie **[!UICONTROL Paket erstellen]** aus.

![Die Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Pakete]**, auf der die Registerkarte [!UICONTROL Paket erstellen] hervorgehoben wird.](../images/ui/sandbox-tooling/create-sandbox-package.png)

Wählen Sie **[!UICONTROL Gesamte Sandbox]** für den [!UICONTROL Pakettyp] im Dialogfeld [!UICONTROL Paket erstellen] aus. Geben Sie einen [!UICONTROL Paketnamen] für das neue Paket ein und wählen Sie die **[!UICONTROL Sandbox]** aus der Dropdown-Liste aus. Wählen Sie abschließend **[!UICONTROL Erstellen]** aus, um Ihre Einträge zu bestätigen.

![Das Dialogfeld [!UICONTROL Paket erstellen] zeigt abgeschlossene Felder an und markiert [!UICONTROL Erstellen]](../images/ui/sandbox-tooling/create-package-dialog.png).

Das Paket wurde erfolgreich erstellt. Wählen Sie **[!UICONTROL Publish]** aus, um das Paket zu veröffentlichen.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Sie werden zur Registerkarte **[!UICONTROL Pakete]** in der Umgebung [!UICONTROL Sandboxes] zurückgeleitet, wo Sie das neue veröffentlichte Paket sehen können.

### Importieren des gesamten Sandbox-Pakets {#import-entire-sandbox-package}

>[!NOTE]
>
>Alle Objekte werden als neue Objekte in die Ziel-Sandbox importiert. Es empfiehlt sich, ein vollständiges Sandbox-Paket in eine leere Sandbox zu importieren.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Durchsuchen]** und wählen Sie die Plusoption (+) neben dem Sandbox-Namen aus.

![Die Registerkarte &quot;Sandboxes **[!UICONTROL Durchsuchen]**&quot;, auf der die Auswahl des Importpakets hervorgehoben wird.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Wählen Sie über das Dropdown-Menü die vollständige Sandbox mithilfe des Dropdown-Menüs **[!UICONTROL Paketname]** aus. Fügen Sie einen **[!UICONTROL Auftragsnamen]**, der für die zukünftige Überwachung verwendet wird, und eine optionale **[!UICONTROL Auftragsbeschreibung]** hinzu und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Die Seite mit den Importdetails, auf der die Dropdown-Auswahl [!UICONTROL Paketname]](../images/ui/sandbox-tooling/import-full-sandbox-package.png) angezeigt wird

>[!NOTE]
>
>Sie müssen über vollständige Berechtigungen für alle im Paket enthaltenen Objekte verfügen. Wenn Sie keine Berechtigungen haben, schlägt der Importvorgang fehl und es werden Fehlermeldungen angezeigt.

Sie gelangen zur Seite [!UICONTROL Package-Objekt und -Abhängigkeiten] , auf der Sie die Anzahl der Objekte und Abhängigkeiten sehen können, die importiert und ausgeschlossen werden. Wählen Sie hier **[!UICONTROL Import]** aus, um den Package-Import abzuschließen.

![ Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] zeigt die Inline-Meldung der nicht unterstützten Objekttypen an und markiert [!UICONTROL Import]](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png).

Warten Sie etwas, bis der Import abgeschlossen ist. Die Zeit zum Abschließen kann je nach der Anzahl der Objekte im Paket variieren. Sie können den Importauftrag über die Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Aufträge]** überwachen.

## Importdetails überwachen {#view-import-details}

Um die importierten Details anzuzeigen, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Aufträge]** und wählen Sie das Paket aus der Liste aus. Alternativ können Sie die Suchleiste verwenden, um nach dem Paket zu suchen.

![Auf der Registerkarte &quot;Sandboxes [!UICONTROL Aufträge]&quot;wird die Auswahl des Importpakets hervorgehoben.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Wählen Sie **[!UICONTROL Importzusammenfassung anzeigen]** aus dem rechten Detailbereich auf der Registerkarte **[!UICONTROL Aufträge]** in der Sandbox-Umgebung aus.

Die Registerkarte ![Sandboxes [!UICONTROL Importe] hebt die Auswahl [!UICONTROL Importdetails anzeigen] im rechten Bereich hervor.](../images/ui/sandbox-tooling/view-import-details.png)

Im Dialogfeld **[!UICONTROL Importzusammenfassung]** wird eine Aufschlüsselung der Importe mit Fortschritt in Prozent angezeigt.

>[!NOTE]
>
>Sie können eine Liste von Objekten anzeigen, indem Sie zu bestimmten Inventarseiten navigieren.

![Das Dialogfeld [!UICONTROL Importdetails] mit einer detaillierten Aufschlüsselung der Importe.](../images/ui/sandbox-tooling/import-details.png)

Nach Abschluss des Imports wird eine Benachrichtigung in der Platform-Benutzeroberfläche empfangen. Sie können auf diese Benachrichtigungen über das Warnungssymbol zugreifen. Sie können von hier aus zur Fehlerbehebung navigieren, wenn ein Auftrag nicht erfolgreich war.

## Video-Tutorial

Das folgende Video soll Ihnen dabei helfen, die Sandbox-Tools zu verstehen, und beschreibt, wie Sie ein neues Paket erstellen, ein Paket veröffentlichen und ein Paket importieren.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Nächste Schritte

In diesem Dokument erfahren Sie, wie Sie die Sandbox-Tool-Funktion in der Experience Platform-Benutzeroberfläche verwenden. Informationen zu Sandboxes finden Sie im [Sandbox-Benutzerhandbuch](../ui/user-guide.md).

Anweisungen zum Ausführen verschiedener Vorgänge mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md). Eine allgemeine Übersicht über Sandboxes im Experience Platform finden Sie in der [Übersichtsdokumentation](../home.md).
