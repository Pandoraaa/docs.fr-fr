# [Avancé](index.md)
## [Architecture de WPF](wpf-architecture.md)
## [Intégration du format XAML au format WPF](xaml-in-wpf.md)
### [Vue d’ensemble du langage XAML (WPF)](xaml-overview-wpf.md)
### [Syntaxe XAML en détail](xaml-syntax-in-detail.md)
### [Code-behind et XAML dans WPF](code-behind-and-xaml-in-wpf.md)
### [XAML et classes personnalisées pour WPF](xaml-and-custom-classes-for-wpf.md)
### [Extensions de balisage et XAML WPF](markup-extensions-and-wpf-xaml.md)
### [Espaces de noms XAML et mappage d'espace de noms pour XAML WPF](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)
### [Portées de nom XAML WPF](wpf-xaml-namescopes.md)
### [Modèles et styles intralignes](inline-styles-and-templates.md)
### [TypeConverters et XAML](typeconverters-and-xaml.md)
### [Extensions XAML WPF](wpf-xaml-extensions.md)
#### [Binding, extension de balisage](binding-markup-extension.md)
#### [ColorConvertedBitmap, extension de balisage](colorconvertedbitmap-markup-extension.md)
#### [ComponentResourceKey, extension de balisage](componentresourcekey-markup-extension.md)
#### [DateTime, syntaxe XAML](datetime-xaml-syntax.md)
#### [Extension de balisage DynamicResource](dynamicresource-markup-extension.md)
#### [RelativeSource, extension de balisage](relativesource-markupextension.md)
#### [StaticResource, extension de balisage](staticresource-markup-extension.md)
#### [TemplateBinding, extension de balisage](templatebinding-markup-extension.md)
#### [ThemeDictionary, extension de balisage](themedictionary-markup-extension.md)
#### [Syntaxe XAML PropertyPath](propertypath-xaml-syntax.md)
#### [PresentationOptions:Freeze, attribut](presentationoptions-freeze-attribute.md)
### [Fonctionnalités de langage pour la compatibilité du balisage (mc:)](markup-compatibility-mc-language-features.md)
#### [mc:Ignorable, attribut](mc-ignorable-attribute.md)
#### [mc:ProcessContent (attribut)](mc-processcontent-attribute.md)
## [Éléments de base](base-elements.md)
### [Vue d’ensemble des éléments de base](base-elements-overview.md)
### [Vue d’ensemble des objets Freezable](freezable-objects-overview.md)
### [Vue d'ensemble de l'alignement, des marges et du remplissage](alignment-margins-and-padding-overview.md)
### [Rubriques de guide pratique](base-elements-how-to-topics.md)
#### [Rendre un UIElement transparent ou semi-transparent](how-to-make-a-uielement-transparent-or-semi-transparent.md)
#### [Animer la taille d'un FrameworkElement](how-to-animate-the-size-of-a-frameworkelement.md)
#### [Déterminer si un Freezable est gelé](how-to-determine-whether-a-freezable-is-frozen.md)
#### [Gérer un événement chargé](how-to-handle-a-loaded-event.md)
#### [Définir les marges d'éléments et de contrôles](how-to-set-margins-of-elements-and-controls.md)
#### [Mettre un Freezable en lecture seule](how-to-make-a-freezable-read-only.md)
#### [Obtenir une copie en écriture d'un Freezable en lecture seule](how-to-obtain-a-writable-copy-of-a-read-only-freezable.md)
#### [Retourner un UIElement horizontalement ou verticalement](how-to-flip-a-uielement-horizontally-or-vertically.md)
#### [Utiliser un objet ThicknessConverter](how-to-use-a-thicknessconverter-object.md)
#### [Gérer l’événement ContextMenuOpening](how-to-handle-the-contextmenuopening-event.md)
## [Sérialisation et arborescence d'éléments](element-tree-and-serialization.md)
### [Arborescences dans WPF](trees-in-wpf.md)
### [Limitations de sérialisation de XamlWriter.Save](serialization-limitations-of-xamlwriter-save.md)
### [Initialisation d’éléments objet ne figurant pas dans une arborescence d’objets](initialization-for-object-elements-not-in-an-object-tree.md)
### [Rubriques de guide pratique](element-tree-and-serialization-how-to-topics.md)
#### [Rechercher un élément par son nom](how-to-find-an-element-by-its-name.md)
#### [Remplacer l’arborescence logique](how-to-override-the-logical-tree.md)
## [Propriétés](properties-wpf.md)
### [Vue d’ensemble des propriétés de dépendance](dependency-properties-overview.md)
### [Vue d'ensemble des propriétés jointes](attached-properties-overview.md)
### [Validation et rappels de propriétés de dépendance](dependency-property-callbacks-and-validation.md)
### [Propriétés de dépendance personnalisées](custom-dependency-properties.md)
### [Métadonnées de propriété de dépendance](dependency-property-metadata.md)
### [Métadonnées de propriété de framework](framework-property-metadata.md)
### [Priorité de la valeur de propriété de dépendance](dependency-property-value-precedence.md)
### [Propriétés de dépendance en lecture seule](read-only-dependency-properties.md)
### [Héritage de la valeur de propriété](property-value-inheritance.md)
### [Sécurité de propriété de dépendance](dependency-property-security.md)
### [Modèles de constructeur sécurisé pour DependencyObjects](safe-constructor-patterns-for-dependencyobjects.md)
### [Propriétés de dépendance de type collection](collection-type-dependency-properties.md)
### [Propriétés de dépendance et chargement XAML](xaml-loading-and-dependency-properties.md)
### [Rubriques de guide pratique](properties-how-to-topics.md)
#### [Implémenter une propriété de dépendance](how-to-implement-a-dependency-property.md)
#### [Ajouter un type propriétaire d'une propriété de dépendance](how-to-add-an-owner-type-for-a-dependency-property.md)
#### [Enregistrer une propriété jointe](how-to-register-an-attached-property.md)
#### [Substituer les métadonnées d'une propriété de dépendance](how-to-override-metadata-for-a-dependency-property.md)
## [Événements](events-wpf.md)
### [Vue d’ensemble des événements routés](routed-events-overview.md)
### [Vue d’ensemble des événements attachés](attached-events-overview.md)
### [Événements de la durée de vie d’un objet](object-lifetime-events.md)
### [Marquage des événements routés comme gérés et gestion de classe](marking-routed-events-as-handled-and-class-handling.md)
### [Événements Preview](preview-events.md)
### [Événements de changement de propriété](property-change-events.md)
### [Gestion des événements Visual Basic et WPF](visual-basic-and-wpf-event-handling.md)
### [Modèles d’événement faible](weak-event-patterns.md)
### [Rubriques de guide pratique](events-how-to-topics.md)
#### [Ajouter un gestionnaire d'événements à l'aide de code](how-to-add-an-event-handler-using-code.md)
#### [Gérer un événement routé](how-to-handle-a-routed-event.md)
#### [Créer un événement routé personnalisé](how-to-create-a-custom-routed-event.md)
#### [Rechercher l'élément source dans un gestionnaire d'événements](how-to-find-the-source-element-in-an-event-handler.md)
#### [Ajouter la gestion de classe d'un événement routé](how-to-add-class-handling-for-a-routed-event.md)
## [Entrée](input-wpf.md)
### [Vue d’ensemble des entrées](input-overview.md)
### [Vue d’ensemble des commandes](commanding-overview.md)
### [Vue d’ensemble du focus](focus-overview.md)
### [FocusVisualStyle et application d'un style au focus dans les contrôles](styling-for-focus-in-controls-and-focusvisualstyle.md)
### [Procédure pas à pas : création de votre première application Touch](walkthrough-creating-your-first-touch-application.md)
### [Rubriques de guide pratique](input-and-commands-how-to-topics.md)
#### [Activer une commande](how-to-enable-a-command.md)
#### [Modifier le type de curseur](how-to-change-the-cursor-type.md)
#### [Modifier la couleur d'un élément à l'aide d'événements Focus](how-to-change-the-color-of-an-element-using-focus-events.md)
#### [Appliquer un FocusVisualStyle à un contrôle](how-to-apply-a-focusvisualstyle-to-a-control.md)
#### [Effectuer une détection en cas d'appui sur la touche Entrée](how-to-detect-when-the-enter-key-pressed.md)
#### [Créer un effet de substitution à l'aide d'événements](how-to-create-a-rollover-effect-using-events.md)
#### [Faire en sorte qu'un objet suive le pointeur de la souris](how-to-make-an-object-follow-the-mouse-pointer.md)
#### [Créer un RoutedCommand](how-to-create-a-routedcommand.md)
#### [Implémenter ICommandSource](how-to-implement-icommandsource.md)
#### [Raccorder une commande à un contrôle sans prise en charge de commande](how-to-hook-up-a-command-to-a-control-with-no-command-support.md)
#### [Raccorder une commande à un contrôle avec prise en charge de commande](how-to-hook-up-a-command-to-a-control-with-command-support.md)
### [Encre numérique](digital-ink.md)
#### [Vues d’ensemble](digital-ink-overviews.md)
##### [Débuter avec l'encre](getting-started-with-ink.md)
##### [Collecte d'encre](collecting-ink.md)
##### [Reconnaissance d'écriture manuscrite](handwriting-recognition.md)
##### [Stockage de l’encre](storing-ink.md)
##### [Modèle objet encre : Windows Forms et COM ou WPF](the-ink-object-model-windows-forms-and-com-versus-wpf.md)
##### [Gestion avancée de l’encre](advanced-ink-handling.md)
###### [Encre de rendu personnalisé](custom-rendering-ink.md)
###### [Interception d'entrée à partir du stylet](intercepting-input-from-the-stylus.md)
###### [Création d'un contrôle d'entrée d'encre](creating-an-ink-input-control.md)
###### [Modèle de thread de l'encre](the-ink-threading-model.md)
#### [Rubriques de guide pratique](digital-ink-how-to-topics.md)
##### [Sélectionner une entrée manuscrite à partir d’un contrôle personnalisé](how-to-select-ink-from-a-custom-control.md)
##### [Ajouter des données personnalisées aux données de l’entrée manuscrite](how-to-add-custom-data-to-ink-data.md)
##### [Effacer l’entrée manuscrite sur un contrôle personnalisé](how-to-erase-ink-on-a-custom-control.md)
##### [Reconnaître les mouvements d’application](how-to-recognize-application-gestures.md)
##### [Glisser et déplacer une entrée manuscrite](how-to-drag-and-drop-ink.md)
##### [Lier des données à un InkCanvas](how-to-data-bind-to-an-inkcanvas.md)
##### [Analyser l’entrée manuscrite avec des indications d’analyse](how-to-analyze-ink-with-analysis-hints.md)
##### [Faire pivoter l’entrée manuscrite](how-to-rotate-ink.md)
##### [Désactiver RealTimeStylus pour les applications WPF](disable-the-realtimestylus-for-wpf-applications.md)
## [Glisser-déposer](drag-and-drop.md)
### [Vue d'ensemble du glisser-déplacer](drag-and-drop-overview.md)
### [Données et objets de données](data-and-data-objects.md)
### [Procédure pas à pas : activation de la fonction glisser-déplacer sur un contrôle utilisateur](walkthrough-enabling-drag-and-drop-on-a-user-control.md)
### [Rubriques de guide pratique](drag-and-drop-how-to-topics.md)
#### [Ouvrir un fichier qui est déplacé dans un contrôle RichTextBox](how-to-open-a-file-that-is-dropped-on-a-richtextbox-control.md)
#### [Créer un objet de données](how-to-create-a-data-object.md)
#### [Déterminer si un format de données est présent dans un objet de données](how-to-determine-if-a-data-format-is-present-in-a-data-object.md)
#### [Répertorier les formats de données dans un objet de données](how-to-list-the-data-formats-in-a-data-object.md)
#### [Récupérer des données dans un format de données particulier](how-to-retrieve-data-in-a-particular-data-format.md)
#### [Stocker plusieurs formats de données dans un objet de données](how-to-store-multiple-data-formats-in-a-data-object.md)
## [Ressources](resources-wpf.md)
### [Ressources XAML](xaml-resources.md)
#### [Ressources et code](resources-and-code.md)
#### [Dictionnaires de ressources fusionnés](merged-resource-dictionaries.md)
#### [Rubriques de guide pratique](resources-how-to-topics.md)
##### [Définir et référencer une ressource](how-to-define-and-reference-a-resource.md)
##### [Utiliser des ressources d'application](how-to-use-application-resources.md)
##### [Utiliser des SystemFonts](how-to-use-systemfonts.md)
##### [Utiliser des clés de polices système](how-to-use-system-fonts-keys.md)
##### [Utiliser SystemParameters](how-to-use-systemparameters.md)
##### [Utiliser les clés des paramètres système](how-to-use-system-parameters-keys.md)
## [Documents](documents.md)
### [Documents dans WPF](documents-in-wpf.md)
### [Sérialisation et stockage de documents](document-serialization-and-storage.md)
### [Annotations](annotations.md)
#### [Vue d’ensemble des annotations](annotations-overview.md)
#### [Schéma d'annotations](annotations-schema.md)
### [Contenu de flux](flow-content.md)
#### [Vue d’ensemble des documents dynamiques](flow-document-overview.md)
#### [Vue d'ensemble du modèle de contenu de TextElement](textelement-content-model-overview.md)
#### [Vue d’ensemble de Table](table-overview.md)
#### [Rubriques de guide pratique](flow-content-elements-how-to-topics.md)
##### [Ajuster l'espacement entre les paragraphes](how-to-adjust-spacing-between-paragraphs.md)
##### [Générer une table par programmation](how-to-build-a-table-programmatically.md)
##### [Modifier la propriété FlowDirection d'un contenu par programmation](how-to-change-the-flowdirection-of-content-programmatically.md)
##### [Modifier la propriété TextWrapping par programmation](how-to-change-the-textwrapping-property-programmatically.md)
##### [Définir une table avec XAML](how-to-define-a-table-with-xaml.md)
##### [Modifier la typographie d’un texte](how-to-alter-the-typography-of-text.md)
##### [Activer la suppression de texte](how-to-enable-text-trimming.md)
##### [Insérer un élément dans du texte par programmation](how-to-insert-an-element-into-text-programmatically.md)
##### [Manipuler des éléments de contenu dynamique avec la propriété Blocks](how-to-manipulate-flow-content-elements-through-the-blocks-property.md)
##### [Manipuler des éléments de contenu de flux avec la propriété Inlines](how-to-manipulate-flow-content-elements-through-the-inlines-property.md)
##### [Manipuler un FlowDocument avec la propriété Blocks](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
##### [Manipuler les colonnes d’un tableau avec la propriété Columns](how-to-manipulate-table-columns-through-the-columns-property.md)
##### [Manipuler les groupes de lignes d’un tableau avec la propriété RowGroups](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
##### [Utiliser les éléments de contenu de flux](how-to-use-flow-content-elements.md)
##### [Utiliser les attributs de séparation de colonnes de FlowDocument](how-to-use-flowdocument-column-separating-attributes.md)
### [Typographie](typography.md)
#### [Typographie dans WPF](typography-in-wpf.md)
#### [Vue d’ensemble ClearType](cleartype-overview.md)
#### [Paramètres du Registre ClearType](cleartype-registry-settings.md)
#### [Dessin du texte mis en forme](drawing-formatted-text.md)
#### [Mise en forme de texte avancée](advanced-text-formatting.md)
#### [Polices](fonts-wpf.md)
##### [Fonctionnalités des polices OpenType](opentype-font-features.md)
##### [Empaquetage de polices avec des applications](packaging-fonts-with-applications.md)
##### [Exemple de pack de polices OpenType](sample-opentype-font-pack.md)
##### [Rubriques de guide pratique](fonts-how-to-topics.md)
###### [Énumérer les polices système](how-to-enumerate-system-fonts.md)
###### [Utiliser la classe FontSizeConverter](how-to-use-the-fontsizeconverter-class.md)
#### [Glyphes](glyphs.md)
##### [Introduction à l'objet GlyphRun et à l'élément Glyphs](introduction-to-the-glyphrun-object-and-glyphs-element.md)
##### [Guide pratique pour dessiner du texte à l'aide de glyphes](draw-text-using-glyphs.md)
#### [Rubriques de guide pratique](typography-how-to-topics.md)
##### [Créer une décoration de texte](how-to-create-a-text-decoration.md)
##### [Spécifier si un lien hypertexte est souligné ou non](how-to-specify-whether-a-hyperlink-is-underlined.md)
##### [Appliquer des transformations à du texte](how-to-apply-transforms-to-text.md)
##### [Guide pratique pour appliquer des animations à du texte](how-to-apply-animations-to-text.md)
##### [Créer du texte avec une ombre](how-to-create-text-with-a-shadow.md)
##### [Créer du texte avec contour](how-to-create-outlined-text.md)
##### [Dessiner du texte sur l’arrière-plan d’un contrôle](how-to-draw-text-to-a-control-background.md)
##### [Ajouter du texte à un Visual](how-to-draw-text-to-a-visual.md)
##### [Utiliser des caractères spéciaux en XAML](how-to-use-special-characters-in-xaml.md)
### [Impression et gestion du système d’impression](printing-and-print-system-management.md)
#### [Vue d’ensemble de l’impression](printing-overview.md)
#### [Rubriques de guide pratique](printing-how-to-topics.md)
##### [Appeler une boîte de dialogue Imprimer](how-to-invoke-a-print-dialog.md)
##### [Cloner une imprimante](how-to-clone-a-printer.md)
##### [Diagnostiquer un travail d'impression problématique](how-to-diagnose-problematic-print-job.md)
##### [Déterminer si un travail d'impression peut être imprimé à cette heure de la journée](how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md)
##### [Énumérer un sous-ensemble de files d'attente à l'impression](how-to-enumerate-a-subset-of-print-queues.md)
##### [Obtenir les propriétés de l'objet de système d'impression sans réflexion](how-to-get-print-system-object-properties-without-reflection.md)
##### [Imprimer des fichiers XPS par programmation](how-to-programmatically-print-xps-files.md)
##### [Observer à distance l'état d'imprimantes](how-to-remotely-survey-the-status-of-printers.md)
##### [Valider et fusionner des PrintTicket](how-to-validate-and-merge-printtickets.md)
## [Globalisation et localisation](globalization-and-localization.md)
### [Vue d’ensemble de la globalisation et de la localisation WPF](wpf-globalization-and-localization-overview.md)
### [Globalisation pour WPF](globalization-for-wpf.md)
### [Vue d’ensemble de l’utilisation de la disposition automatique](use-automatic-layout-overview.md)
### [Attributs et commentaires de localisation](localization-attributes-and-comments.md)
### [Vue d'ensemble des fonctionnalités bidirectionnelles dans WPF](bidirectional-features-in-wpf-overview.md)
### [Rubriques de guide pratique](globalization-and-localization-how-to-topics.md)
#### [Localiser une application](how-to-localize-an-application.md)
#### [Utiliser la disposition automatique pour créer un bouton](how-to-use-automatic-layout-to-create-a-button.md)
#### [Utiliser une grille pour la disposition automatique](how-to-use-a-grid-for-automatic-layout.md)
#### [Utiliser un ResourceDictionary pour gérer des ressources de type chaîne localisables](how-to-use-a-resourcedictionary-to-manage-localizable-string-resources.md)
#### [Utiliser des ressources dans des applications localisables](how-to-use-resources-in-localizable-applications.md)
## [Disposition](layout.md)
## [Migration et interopérabilité](migration-and-interoperability.md)
### [Interopérabilité WPF et Windows Forms](wpf-and-windows-forms-interoperation.md)
#### [Architecture d’entrée pour l’interopérabilité entre Windows Forms et WPF](windows-forms-and-wpf-interoperability-input-architecture.md)
#### [Considérations sur la disposition de l’élément WindowsFormsHost](layout-considerations-for-the-windowsformshost-element.md)
#### [Contrôles Windows Forms et contrôles WPF équivalents](windows-forms-controls-and-equivalent-wpf-controls.md)
#### [Mappage de propriétés Windows Forms et WPF](windows-forms-and-wpf-property-mapping.md)
#### [Dépannage des applications hybrides](troubleshooting-hybrid-applications.md)
#### [Procédure pas à pas : hébergement d’un contrôle Windows Forms dans WPF](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
#### [Procédure pas à pas : hébergement d’un contrôle Windows Forms dans WPF avec XAML](walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml.md)
#### [Procédure pas à pas : hébergement d'un contrôle composite Windows Forms dans WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
#### [Procédure pas à pas : hébergement d'un contrôle ActiveX dans WPF](walkthrough-hosting-an-activex-control-in-wpf.md)
#### [Guide pratique pour activer des styles visuels dans une application hybride](how-to-enable-visual-styles-in-a-hybrid-application.md)
#### [Procédure pas à pas : organisation des contrôles Windows Forms dans WPF](walkthrough-arranging-windows-forms-controls-in-wpf.md)
#### [Procédure pas à pas : liaison de données dans des applications hybrides](walkthrough-binding-to-data-in-hybrid-applications.md)
#### [Procédure pas à pas : hébergement d’un contrôle composite 3-D WPF dans les Windows Forms](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)
#### [Procédure pas à pas : Hébergement d'un contrôle composite WPF dans Windows Forms](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
#### [Procédure pas à pas : mappage de propriété à l'aide du contrôle ElementHost](walkthrough-mapping-properties-using-the-elementhost-control.md)
#### [Procédure pas à pas : mappage de propriétés à l'aide de l'élément WindowsFormsHost](walkthrough-mapping-properties-using-the-windowsformshost-element.md)
#### [Procédure pas à pas : localisation d'une application hybride](walkthrough-localizing-a-hybrid-application.md)
### [Interopérabilité WPF et Win32](wpf-and-win32-interoperation.md)
#### [Vue d'ensemble des régions de technologie](technology-regions-overview.md)
#### [Partage de boucles de messages entre Win32 et WPF](sharing-message-loops-between-win32-and-wpf.md)
#### [Hébergement de contenu Win32 dans WPF](hosting-win32-content-in-wpf.md)
#### [Procédure pas à pas : hébergement d'un contrôle Win32 dans WPF](walkthrough-hosting-a-win32-control-in-wpf.md)
#### [Procédure pas à pas : hébergement de contenu WPF dans Win32](walkthrough-hosting-wpf-content-in-win32.md)
#### [Procédure pas à pas : hébergement d'un WPF Clock dans Win32](walkthrough-hosting-a-wpf-clock-in-win32.md)
### [Interopérabilité WPF et Direct3D9](wpf-and-direct3d9-interoperation.md)
#### [Considérations sur les performances de l'interopérabilité entre Direct3D9 et WPF](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
#### [Procédure pas à pas : création de contenu Direct3D9 à héberger dans WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
#### [Procédure pas à pas : hébergement de contenu Direct3D9 dans WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)
## [Performances](performance.md)
### [Couches de rendu graphiques](graphics-rendering-tiers.md)
### [Optimisation des performances des applications WPF](optimizing-wpf-application-performance.md)
#### [Planification des performances des applications](planning-for-application-performance.md)
#### [Tirer parti du matériel](optimizing-performance-taking-advantage-of-hardware.md)
#### [Disposition et conception](optimizing-performance-layout-and-design.md)
#### [Graphiques 2D et acquisition d'images](optimizing-performance-2d-graphics-and-imaging.md)
#### [Comportement de l’objet](optimizing-performance-object-behavior.md)
#### [Ressources d'application](optimizing-performance-application-resources.md)
#### [Texte](optimizing-performance-text.md)
#### [Liaison de données](optimizing-performance-data-binding.md)
#### [Contrôles](optimizing-performance-controls.md)
#### [Autres recommandations relatives aux performances](optimizing-performance-other-recommendations.md)
#### [Temps de démarrage d’une application](application-startup-time.md)
### [Procédure pas à pas : mise en cache de données d’application dans une application WPF](walkthrough-caching-application-data-in-a-wpf-application.md)
## [Modèle de thread](threading-model.md)
## [Référence des API non managées WPF](wpf-unmanaged-api-reference.md)
### [Activer une fonction](activate-function-wpf-unmanaged-api-reference.md)
### [Fonction CreateIDispatchSTAForwarder](createidispatchstaforwarder-function-wpf-unmanaged-api-reference.md)
### [Désactiver une fonction](deactivate-function-wpf-unmanaged-api-reference.md)
### [Fonction ForwardTranslateAccelerator](forwardtranslateaccelerator-function-wpf-unmanaged-api-reference.md)
### [Fonction LoadFromHistory](loadfromhistory-function-wpf-unmanaged-api-reference.md)
### [Fonction ProcessUnhandledException](processunhandledexception-function-wpf-unmanaged-api-reference.md)
### [Fonction SaveToHistory](savetohistory-function-wpf-unmanaged-api-reference.md)
### [Fonction SetFakeActiveWindow](setfakeactivewindow-function-wpf-unmanaged-api-reference.md)
