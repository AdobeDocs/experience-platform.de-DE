---
title: Sandbox-Tools
description: Nahtloser Export und Import von Sandbox-Konfigurationen zwischen Sandboxes.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 208c9c47b4bde211506867cf59b8743556db7fc8
workflow-type: tm+mt
source-wordcount: '2678'
ht-degree: 7%

---

# Sandbox-Werkzeuge

>[!NOTE]
>
>Sandbox-Tools sind eine grundlegende Funktion, die sowohl [!DNL Real-Time Customer Data Platform] als auch [!DNL Journey Optimizer] unterstützt, um die Effizienz des Entwicklungszyklus und die Konfigurationsgenauigkeit zu verbessern.<br><br>Für die Verwendung der Sandbox-Tooling-Funktion sind die folgenden beiden rollenbasierten Zugriffssteuerungsberechtigungen erforderlich:<br>- `manage-sandbox` oder `view-sandbox`<br>- `manage-package`

Verbessern Sie die Konfigurationsgenauigkeit über Sandboxes hinweg und exportieren und importieren Sie Sandbox-Konfigurationen zwischen Sandboxes mit der Sandbox-Tooling-Funktion nahtlos. Verwenden Sie die Sandbox-Tools, um die Wertschöpfungszeit für den Implementierungsprozess zu reduzieren und erfolgreiche Konfigurationen über Sandboxes hinweg zu verschieben.

Sie können die Sandbox-Tooling-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Ein Paket kann aus einem oder mehreren Objekten bestehen. <!--or an entire sandbox.-->Alle Objekte, die in einem Paket enthalten sind, müssen aus derselben Sandbox stammen.

## Für Sandbox-Tools unterstützte Objekte {#supported-objects}

Die Sandbox-Tooling-Funktion bietet Ihnen die Möglichkeit, [!DNL Adobe Real-Time Customer Data Platform] und [!DNL Adobe Journey Optimizer] Objekte in ein Paket zu exportieren.

### Real-time Customer Data Platform-Objekte {#real-time-cdp-objects}

In der folgenden Tabelle sind [!DNL Adobe Real-Time Customer Data Platform] Objekte aufgeführt, die derzeit für Sandbox-Tools unterstützt werden:

| Plattform | Objekt | Details |
| --- | --- | --- |
| Customer Data Platform | Quellen | Die Anmeldeinformationen für das Quellkonto werden aus Sicherheitsgründen nicht in der Ziel-Sandbox repliziert und müssen manuell aktualisiert werden. Der Quelldatenfluss wird standardmäßig in den Entwurfsstatus kopiert. |
| Customer Data Platform | Zielgruppen | Es wird nur **[!UICONTROL Typ]** Kundenzielgruppe **[!UICONTROL (]**) unterstützt. Vorhandene Kennzeichnungen für Einverständnis und Governance werden im selben Importvorgang kopiert. Das System wählt beim Überprüfen der Abhängigkeiten von Zusammenführungsrichtlinien automatisch die standardmäßige Zusammenführungsrichtlinie in der Ziel-Sandbox mit derselben XDM-Klasse aus. |
| Customer Data Platform | Identitäten | Das System dedupliziert beim Erstellen von Identitäts-Namespaces für Adobe Standard automatisch in der Ziel-Sandbox. Zielgruppen können nur kopiert werden, wenn alle Attribute in Zielgruppenregeln im Vereinigungsschema aktiviert sind. Die erforderlichen Schemata müssen zunächst verschoben und für das einheitliche Profil aktiviert werden. |
| Customer Data Platform | Schemata | Vorhandene Kennzeichnungen für Einverständnis und Governance werden im selben Importvorgang kopiert. Der Benutzer hat die Flexibilität, Schemas zu importieren, ohne die Option Einheitliches Profil aktiviert zu haben. Die Edge-Fall-Schemabeziehungen sind nicht im Paket enthalten. |
| Customer Data Platform | Datensätze | Datensätze werden kopiert, wobei die Einstellung „Einheitliches Profil“ standardmäßig deaktiviert ist. |
| Customer Data Platform | Einverständnis- und Governance-Richtlinien | Hinzufügen benutzerdefinierter Richtlinien, die von einem Benutzer erstellt wurden, zu einem Paket und Verschieben der Richtlinien über Sandboxes hinweg. |

Die folgenden Objekte werden importiert, haben jedoch den Status „Entwurf“ oder „Deaktiviert“:

| Funktion | Objekt | Status |
| --- | --- | --- |
| Importstatus | Source-Datenfluss | Entwurf |
| Importstatus | Journey | Entwurf |
| Einheitliches Profil | Datensatz | Einheitliches Profil deaktiviert |
| Richtlinien | Data Governance-Richtlinien | Deaktiviert |

### Adobe Journey Optimizer-Objekte {#abobe-journey-optimizer-objects}

In der folgenden Tabelle sind [!DNL Adobe Journey Optimizer] Objekte aufgeführt, die derzeit für Sandbox-Tools und Einschränkungen unterstützt werden:

| Plattform | Objekt | Unterstützte abhängige Objekte | Details |
| --- | --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Zielgruppe | | Eine Zielgruppe kann als abhängiges Objekt des Journey-Objekts kopiert werden. Sie können eine neue Zielgruppe erstellen oder eine vorhandene in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Schema | | Die auf der Journey verwendeten Schemata können als abhängige Objekte kopiert werden. Sie können ein neues Schema erstellen oder ein vorhandenes in der Ziel-Sandbox wiederverwenden. |
| [!DNL Adobe Journey Optimizer] | Zusammenführungsrichtlinie | | Die auf der Journey verwendeten Zusammenführungsrichtlinien können als abhängige Objekte kopiert werden. In der Ziel-Sandbox **Sie (**) keine neue Zusammenführungsrichtlinie erstellen, sondern nur eine vorhandene verwenden. |
| [!DNL Adobe Journey Optimizer] | Journey | Die folgenden Objekte, die auf der Journey verwendet werden, werden als abhängige Objekte kopiert. Während des Import-Workflows können Sie für jeden **[!UICONTROL Neu erstellen]** oder **[!UICONTROL Vorhandenes verwenden]** auswählen: <ul><li>Zielgruppen</li><li>Schemata</li><li>Benutzerdefinierte Aktionen</li><li>Ereignisse</li><li>Fragmente</li><li>Inhaltsvorlagen</li><li>Canvas-Details</li></ul> | <ul><li>**[!UICONTROL Benutzerdefinierte Aktionen]**: Wenn Sie **[!UICONTROL Vorhandene verwenden]** während des Importvorgangs auswählen, wenn Sie eine Journey in eine andere Sandbox kopieren, müssen die von Ihnen ausgewählten benutzerdefinierten Aktionen **&#x200B;**&#x200B;mit der benutzerdefinierten Quellaktion übereinstimmen. Wenn sie nicht identisch sind, weist die neue Journey unlösbare Fehler auf.</li><li>Die auf der Journey verwendeten Ereignisse und Ereignisdetails werden kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt.</li></ul> |
| [!DNL Adobe Journey Optimizer] | Aktion | | Auf der Journey verwendete E-Mail- und Push-Nachrichten können als abhängige Objekte kopiert werden. Die in den Journey-Feldern verwendeten Kanalaktionsaktivitäten, die in der Nachricht zur Personalisierung verwendet werden, werden nicht auf Vollständigkeit überprüft. Inhaltsbausteine werden nicht kopiert.<br><br>Die auf der Journey verwendete Aktion Profil aktualisieren kann kopiert werden. Benutzerdefinierte Aktionen können einem Paket unabhängig hinzugefügt werden. Auf der Journey verwendete Aktionsdetails werden ebenfalls kopiert. Es wird immer eine neue Version in der Ziel-Sandbox erstellt. |
| [!DNL Adobe Journey Optimizer] | Benutzerdefinierte Aktionen |  | Benutzerdefinierte Aktionen können einem Paket unabhängig hinzugefügt werden. Nachdem eine benutzerdefinierte Aktion einer Journey zugewiesen wurde, kann sie nicht mehr bearbeitet werden. Um Aktualisierungen an benutzerdefinierten Aktionen vorzunehmen, sollten Sie: <ul><li>Verschieben benutzerdefinierter Aktionen vor dem Migrieren einer Journey</li><li>Aktualisieren Sie Konfigurationen (z. B. Anfragekopfzeilen, Abfrageparameter und Authentifizierung) für benutzerdefinierte Aktionen nach der Migration</li><li>Migrieren von Journey-Objekten mit den benutzerdefinierten Aktionen, die Sie im ersten Schritt hinzugefügt haben</li></ul> |
| [!DNL Adobe Journey Optimizer] | Inhaltsvorlage | | Eine Inhaltsvorlage kann als abhängiges Objekt des Journey-Objekts kopiert werden. Eigenständige Vorlagen ermöglichen die einfache Wiederverwendung benutzerdefinierter Inhalte in Journey Optimizer-Kampagnen und -Journey. |
| [!DNL Adobe Journey Optimizer] | Fragment | Alle verschachtelten Fragmente. | Ein Fragment kann als abhängiges Objekt des Journey-Objekts kopiert werden. Fragmente sind wiederverwendbare Komponenten, die in einer oder mehreren Journey Optimizer-Kampagnen und -Journey-Umgebungen referenziert werden können. |
| [!DNL Adobe Journey Optimizer] | Kampagnen | Die folgenden in der Kampagne verwendeten Objekte werden als abhängige Objekte kopiert: <ul><li>Kampagnen</li><li>Zielgruppen</li><li>Schemata</li><li>Inhaltsvorlagen</li><li>Fragmente</li><li>Nachricht/Inhalt</li><li>Kanalkonfiguration</li><li>Einheitliche Entscheidungsobjekte</li><li>Experimenteinstellungen/-varianten</li></ul> | <ul><li>Kampagnen können zusammen mit allen Elementen kopiert werden, die sich auf das Profil, die Zielgruppe, das Schema, Inline-Nachrichten und abhängige Objekte beziehen. Einige Elemente werden nicht kopiert, z. B. Datennutzungsbeschriftungen und Spracheinstellungen. Eine vollständige Liste der Objekte, die nicht kopiert werden können, finden Sie im Handbuch [Exportieren von Objekten in eine andere Sandbox](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/configuration/copy-objects-to-sandbox) .</li><li>Das System erkennt automatisch ein vorhandenes Kanalkonfigurationsobjekt in der Ziel-Sandbox und verwendet es erneut, wenn eine identische Konfiguration vorhanden ist. Wenn keine übereinstimmende Konfiguration gefunden wird, wird die Kanalkonfiguration beim Import übersprungen und Benutzende müssen die Kanaleinstellungen in der Ziel-Sandbox für diese Journey manuell aktualisieren.</li><li>Benutzer können vorhandene Experimente und Zielgruppen in der Ziel-Sandbox als abhängige Objekte ausgewählter Kampagnen wiederverwenden.</li></ul> |

Oberflächen (z. B. Voreinstellungen) werden nicht kopiert. Das System wählt basierend auf dem Nachrichtentyp und dem Namen der Oberfläche automatisch die bestmögliche Übereinstimmung für die Ziel-Sandbox aus. Wenn keine Oberflächen in der Ziel-Sandbox gefunden werden, schlägt die Kopie der Oberfläche fehl, wodurch die Nachrichtenkopie fehlschlägt, da für eine Nachricht eine Oberfläche zur Einrichtung verfügbar sein muss. In diesem Fall muss mindestens eine Oberfläche für den richtigen Kanal der Nachricht erstellt werden, damit die Kopie funktioniert.

Benutzerdefinierte Identitätstypen werden beim Exportieren einer Journey nicht als abhängige Objekte unterstützt.

## Exportieren von Objekten in ein Paket {#export-objects}

>[!NOTE]
>
>Alle Exportaktionen werden in den Auditprotokollen aufgezeichnet.

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
>Sie können ein Paket nur importieren, wenn Sie über die Berechtigung zum Zugriff auf die Objekte verfügen.

In diesem Beispiel wird der Prozess des Exports eines Schemas und dessen Hinzufügen zu einem Paket dokumentiert. Sie können denselben Prozess verwenden, um andere Objekte zu exportieren, z. B. Datensätze, Journey und viele mehr.

### Objekt zu einem neuen Paket hinzufügen {#add-object-to-new-package}

Wählen Sie **[!UICONTROL linken Navigationsbereich die Option]** Schemata“ und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus, auf der die verfügbaren Schemata aufgeführt sind. Klicken Sie als Nächstes auf das Auslassungszeichen (`...`) neben dem ausgewählten Schema, und in einem Dropdown-Menü werden dann Steuerelemente angezeigt. Wählen **[!UICONTROL Zum Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata mit dem Dropdown-Menü, in dem das Steuerelement [!UICONTROL Zum Paket hinzufügen] hervorgehoben ist.](../images/ui/sandbox-tooling/add-to-package.png)

Wählen Sie **[!UICONTROL Dialogfeld „Zum Paket hinzufügen]** die Option **[!UICONTROL Neues Paket erstellen]** aus. Geben Sie einen [!UICONTROL Namen] für Ihr Paket und eine optionale [!UICONTROL Beschreibung] an und klicken Sie dann auf **[!UICONTROL Hinzufügen]**.

![Das Dialogfeld [!UICONTROL Zum Paket hinzufügen] mit [!UICONTROL Neues Paket erstellen] ausgewählt und [!UICONTROL Hinzufügen] hervorgehoben](../images/ui/sandbox-tooling/create-new-package.png)

Sie kehren zur Umgebung **[!UICONTROL Schemata]** zurück. Sie können jetzt dem von Ihnen erstellten Paket zusätzliche Objekte hinzufügen, indem Sie die nächsten Schritte ausführen, die unten aufgeführt sind.

### Objekt zu einem vorhandenen Paket hinzufügen und veröffentlichen {#add-object-to-existing-package}

Um eine Liste der verfügbaren Schemata anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Schemata]** und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus. Klicken Sie als Nächstes auf das Auslassungszeichen (`...`) neben dem ausgewählten Schema, um die Steuerungsoptionen in einem Dropdown-Menü anzuzeigen. Wählen **[!UICONTROL Zum Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata mit dem Dropdown-Menü, in dem das Steuerelement [!UICONTROL Zum Paket hinzufügen] hervorgehoben ist.](../images/ui/sandbox-tooling/add-to-package.png)

Das **[!UICONTROL Zu Paket hinzufügen]** wird angezeigt. Wählen Sie die Option **[!UICONTROL Vorhandenes Paket]** aus, klicken Sie dann in **[!UICONTROL Dropdown-Liste Paketname]** und wählen Sie das erforderliche Paket aus. Wählen Sie abschließend **[!UICONTROL Hinzufügen]** aus, um Ihre Auswahl zu bestätigen.

![[!UICONTROL Zum Paket hinzufügen] zeigt ein ausgewähltes Paket aus dem Dropdown-Menü an.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Die Liste der dem Paket hinzugefügten Objekte wird aufgelistet. Um das Paket zu veröffentlichen und es für den Import in Sandboxes verfügbar zu machen, wählen Sie &quot;**[!UICONTROL &quot;]**.

![Liste der Objekte im Paket, Hervorhebung der Option [!UICONTROL Veröffentlichen].](../images/ui/sandbox-tooling/publish-package.png)

Wählen **[!UICONTROL Veröffentlichen]** aus, um die Veröffentlichung des Pakets zu bestätigen.

![Bestätigungsdialogfeld „Paket veröffentlichen“ mit hervorgehobener Option [!UICONTROL Veröffentlichen].](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nach der Veröffentlichung kann der Inhalt des Pakets nicht mehr geändert werden. Um Kompatibilitätsprobleme zu vermeiden, stellen Sie sicher, dass alle erforderlichen Assets ausgewählt wurden. Wenn Änderungen vorgenommen werden müssen, müssen Sie ein neues Paket erstellen.

Sie kehren zur Registerkarte **[!UICONTROL Pakete]** in der Umgebung [!UICONTROL Sandboxes] zurück, auf der Sie das neue veröffentlichte Paket sehen können.

![Liste der Sandbox-Pakete mit Hervorhebung des neuen veröffentlichten Pakets.](../images/ui/sandbox-tooling/published-packages.png)

## Paket in eine Ziel-Sandbox importieren {#import-package-to-target-sandbox}

>[!NOTE]
>
>Alle Importaktionen werden in den Auditprotokollen aufgezeichnet.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zur Registerkarte **[!UICONTROL Durchsuchen]** und wählen Sie die Option Plus (+) neben dem Sandbox-Namen aus.

![Die Registerkarte **[!UICONTROL Durchsuchen]** mit hervorgehobener Auswahl für das Importpaket.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Wählen Sie über das Dropdown-Menü den **[!UICONTROL Paketnamen]** den Sie in die Ziel-Sandbox importieren möchten. Fügen Sie einen **[!UICONTROL Auftragsnamen]** hinzu, der für die zukünftige Überwachung verwendet wird. Standardmäßig wird Unified Profile deaktiviert, wenn die Schemata des Pakets importiert werden. Schalten Sie **Schemata für Profil aktivieren** um dies zu aktivieren, und klicken Sie dann auf **[!UICONTROL Weiter]**.

![Die Seite mit den Importdetails, auf der die Dropdown[!UICONTROL Auswahl „Paketname] angezeigt wird](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

Die Seite [!UICONTROL Paketobjekt und &#x200B;]&quot; enthält eine Liste aller in diesem Paket enthaltenen Assets. Das System erkennt automatisch abhängige Objekte, die für den erfolgreichen Import ausgewählter übergeordneter Objekte erforderlich sind. Alle fehlenden Attribute werden oben auf der Seite angezeigt. Wählen Sie **[!UICONTROL Details anzeigen]**, um eine detailliertere Aufschlüsselung zu erhalten.

![Auf [!UICONTROL &#x200B; Seite „Paketobjekt und &#x200B;]&quot; fehlen Attribute.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Abhängige Objekte können durch vorhandene in der Ziel-Sandbox ersetzt werden, sodass Sie vorhandene Objekte wiederverwenden können, anstatt eine neue Version zu erstellen. Wenn Sie beispielsweise ein Paket importieren, das Schemata enthält, können Sie vorhandene benutzerdefinierte Feldergruppen und Identitäts-Namespaces in der Ziel-Sandbox wiederverwenden. Alternativ können Sie beim Importieren eines Pakets, das Journey enthält, vorhandene Segmente in der Ziel-Sandbox wiederverwenden.
>
>Sandbox-Tools unterstützen derzeit nicht das Aktualisieren oder Überschreiben vorhandener Objekte. Sie können ein neues Objekt erstellen oder das vorhandene Objekt ohne Änderungen weiter verwenden.

Um ein vorhandenes Objekt zu verwenden, wählen Sie das Stiftsymbol neben dem abhängigen Objekt aus.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] zeigt eine Liste der im Paket enthaltenen Assets an.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Die Optionen zum Erstellen neuer oder zum Verwenden vorhandener werden angezeigt. Wählen Sie **[!UICONTROL Use existing]** aus.

![Die Seite [!UICONTROL Paketobjekt und Abhängigkeiten] mit den abhängigen Objektoptionen [!UICONTROL Neu erstellen] und [!UICONTROL Vorhandenes verwenden].](../images/ui/sandbox-tooling/use-existing-object.png)

Das **[!UICONTROL Feldgruppe]** zeigt eine Liste der für das Objekt verfügbaren Feldgruppen an. Wählen Sie die erforderlichen Feldergruppen aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

![Eine Liste der Felder, die im Dialogfeld [!UICONTROL Feldergruppe] angezeigt wird, wobei die Auswahl [!UICONTROL Speichern] hervorgehoben wird. ](../images/ui/sandbox-tooling/field-group-list.png)

Sie kehren zur Seite &quot;[!UICONTROL &#x200B; und Abhängigkeiten“ &#x200B;]. Wählen Sie von hier aus **[!UICONTROL Beenden]**, um den Package-Import abzuschließen.

![Die Seite [!UICONTROL Paketobjekt und &#x200B;]&quot; zeigt eine Liste der im Paket enthaltenen Assets an und markiert [!UICONTROL Beenden].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Gesamte Sandbox exportieren und importieren

>[!NOTE]
>
>Derzeit werden beim Exportieren oder Importieren einer gesamten Sandbox nur Real-time Customer Data Platform-Objekte unterstützt. Adobe Journey Optimizer-Objekte wie Journey werden derzeit nicht unterstützt.

Sie können alle unterstützten Objekttypen in ein vollständiges Sandbox-Paket exportieren und dann das Paket über verschiedene Sandboxes hinweg importieren, um Objektkonfigurationen zu replizieren. Mit dieser Funktion können Sie beispielsweise:

- Importieren Sie eine Sandbox erneut, um alle Konfigurationen des -Objekts zu reproduzieren, wenn Sie die Sandbox zurücksetzen müssen
- Importieren Sie das Paket in andere Sandboxes und verwenden Sie es als Blueprint-Sandbox, um den Entwicklungsprozess zu beschleunigen.

### Gesamte Sandbox exportieren {#export-entire-sandbox}

Um eine gesamte Sandbox zu exportieren, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** und wählen Sie **[!UICONTROL Paket erstellen]** aus.

![Die Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** mit hervorgehobener Option [!UICONTROL Paket erstellen].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Wählen Sie **[!UICONTROL Gesamte Sandbox]** für [!UICONTROL Pakettyp] im Dialogfeld [!UICONTROL Paket erstellen] aus. Geben Sie einen [!UICONTROL Paketnamen] für Ihr neues Paket an und wählen Sie die **[!UICONTROL Sandbox]** aus der Dropdown-Liste aus. Wählen Sie abschließend **[!UICONTROL Erstellen]** aus, um Ihre Eingaben zu bestätigen.

![Das Dialogfeld [!UICONTROL Paket erstellen] mit ausgefüllten Feldern und Hervorhebung [!UICONTROL Erstellen].](../images/ui/sandbox-tooling/create-package-dialog.png)

Das Paket wurde erfolgreich erstellt. Wählen Sie **[!UICONTROL Veröffentlichen]** aus, um das Paket zu veröffentlichen.

![Liste der Sandbox-Pakete mit Hervorhebung des neuen veröffentlichten Pakets.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Sie kehren zur Registerkarte **[!UICONTROL Pakete]** in der Umgebung [!UICONTROL Sandboxes] zurück, auf der Sie das neue veröffentlichte Paket sehen können.

### Importieren des gesamten Sandbox-Pakets {#import-entire-sandbox-package}

>[!NOTE]
>
>Alle Objekte werden als neue Objekte in die Ziel-Sandbox importiert. Es empfiehlt sich, ein vollständiges Sandbox-Paket in eine leere Sandbox zu importieren.

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Durchsuchen]** und wählen Sie die Option Plus (+) neben dem Sandbox-Namen aus.

![Die Registerkarte **[!UICONTROL Durchsuchen]** mit hervorgehobener Auswahl für das Importpaket.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Wählen Sie im Dropdown-Menü mithilfe der Dropdown-Liste **[!UICONTROL Paketname]** die vollständige Sandbox aus. Fügen Sie einen **[!UICONTROL Auftragsnamen]**, der für die zukünftige Überwachung verwendet wird, und eine optionale **[!UICONTROL Auftragsbeschreibung]** hinzu und klicken Sie dann auf **[!UICONTROL Weiter]**.

![Die Seite mit den Importdetails, auf der die Dropdown[!UICONTROL Auswahl „Paketname] angezeigt wird](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Sie müssen über vollständige Berechtigungen für alle Objekte verfügen, die im Paket enthalten sind. Wenn Sie nicht über die erforderlichen Berechtigungen verfügen, schlägt der Importvorgang fehl und es werden Fehlermeldungen angezeigt.

Sie gelangen auf die Seite [!UICONTROL Paketobjekt und Abhängigkeiten], auf der Sie die Anzahl der Objekte und Abhängigkeiten sehen können, die importierte und ausgeschlossene Objekte sind. Wählen Sie von hier **[!UICONTROL Importieren]**, um den Package-Import abzuschließen.

![Die Seite [!UICONTROL Paketobjekt und &#x200B;]&quot; zeigt die Inline-Meldung von nicht unterstützten Objekttypen und markiert [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Warten Sie etwas, bis der Import abgeschlossen ist. Die Dauer des Vorgangs kann von der Anzahl der Objekte im Paket abhängen. Sie können den Importauftrag über die Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Aufträge]** überwachen.

## Importdetails überwachen {#view-import-details}

Um die importierten Details anzuzeigen, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Vorgänge]** und wählen Sie das Paket aus der Liste aus. Alternativ können Sie über die Suchleiste nach dem Paket suchen.

![Auf der Registerkarte [!UICONTROL Vorgänge] wird die Auswahl des Importpakets hervorgehoben.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Wählen **[!UICONTROL Importzusammenfassung anzeigen]** im rechten Detailbereich auf der Registerkarte **[!UICONTROL Vorgänge]** in der Sandbox-Umgebung aus.

![Die Registerkarte [!UICONTROL Importe] der Sandboxes hebt die Auswahl [!UICONTROL Importdetails anzeigen] im rechten Bereich hervor.](../images/ui/sandbox-tooling/view-import-details.png)

Das **[!UICONTROL Importzusammenfassung]** zeigt eine Aufschlüsselung der Importe mit Fortschritt in Prozent an.

>[!NOTE]
>
>Sie können eine Liste von Objekten anzeigen, indem Sie zu bestimmten Inventarseiten navigieren.

![Das Dialogfeld [!UICONTROL Importdetails] mit einer detaillierten Aufschlüsselung der Importe.](../images/ui/sandbox-tooling/import-details.png)

Nach Abschluss des Imports erhalten Sie eine Benachrichtigung über den Import in der Experience Platform-Benutzeroberfläche. Sie können auf diese Benachrichtigungen über das Warnhinweissymbol zugreifen. Wenn ein Vorgang nicht erfolgreich war, können Sie von hier aus zur Fehlerbehebung navigieren.

## Video-Tutorial

Das folgende Video soll Ihnen dabei helfen, die Sandbox-Tools besser zu verstehen, und beschreibt, wie Sie ein neues Paket erstellen, ein Paket veröffentlichen und ein Paket importieren.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Nächste Schritte

In diesem Dokument wurde gezeigt, wie die Sandbox-Tooling-Funktion in der Experience Platform-Benutzeroberfläche verwendet wird. Informationen zu Sandboxes finden Sie im [Sandbox-Benutzerhandbuch](../ui/user-guide.md).

Anweisungen zum Ausführen verschiedener Vorgänge mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md). Eine allgemeine Übersicht zu Sandboxes in Experience Platform finden Sie in der [Übersichtsdokumentation](../home.md).
