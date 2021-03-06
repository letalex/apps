---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-07"

---

{: new_window: target="_blank"}
{:shortdesc: .shortdesc}
{: codeblock: .codeblock}

# Ajout d'un service à votre application
{: #add_service}

Lorsque vous créez une application avec {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}, vous pouvez ajouter des ressources à partir de la page de présentation de l'application. Toutefois, vous pouvez également les mettre à disposition directement à partir du catalogue {{site.data.keyword.Bluemix_notm}} en dehors du contexte de votre application.
{: shortdesc}

Vous pouvez demander une instance de la ressource et l'utiliser indépendamment de votre application, ou vous pouvez ajouter l'instance de ressource à votre application à partir de la page de présentation de l'application. Vous pouvez mettre à disposition un type spécifique de ressource (un service) directement à partir du catalogue {{site.data.keyword.Bluemix_notm}}.

## Reconnaissance de services
{: #discover_services}

Vous pouvez afficher tous les services qui sont disponibles dans {{site.data.keyword.Bluemix_notm}} comme suit :

* Depuis la console {{site.data.keyword.Bluemix_notm}}. Affichez le catalogue {{site.data.keyword.Bluemix_notm}}.
* Depuis l'interface de ligne de commande ibmcloud. Utilisez la commande `ibmcloud service offerings`.
* Depuis votre propre application. Utilisez l'[API GET /v2/services Services ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}.

Vous pouvez sélectionner le service dont vous avez besoin pendant le développement des applications. Une fois le service sélectionné, {{site.data.keyword.Bluemix_notm}} met le service à disposition. Le processus de mise à disposition peut varier en fonction des types de service. Par exemple, un service de base de données crée une base de données, un service de notification push pour des applications mobiles génère des informations de configuration.

{{site.data.keyword.Bluemix_notm}} fournit les ressources d'un service à votre application par le biais d'une
instance de service. Une instance de service peut être partagée entre plusieurs applications Web.

Vous pouvez aussi utiliser des services qui sont hébergés dans d'autres régions, si ces services sont disponibles dans ces régions. Ils doivent être accessibles depuis Internet et posséder des noeuds finaux d'API. Vous devez coder manuellement votre application pour l'utilisation
de ces services de la même façon que vous codez les applications externes ou les outils tiers pour l'utilisation des services
{{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [Utilisation des services {{site.data.keyword.Bluemix_notm}} avec des
applications externes et des outils tiers](#accser_external).

## Demande de nouvelle instance de service
{: #req_instance}

Pour demander une nouvelle instance de service, vous devez utiliser l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

**Remarque :** lorsque vous spécifiez le nom du service, évitez d'utiliser des caractères autres qu'alphabétiques ou numériques, pour ne pas risquer de générer des résultats imprévisibles.

Si vous utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}} pour demander une instance de service, procédez comme suit :

1. Dans le catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette du service que vous souhaitez ajouter. La page des détails du service s'ouvre.

2. Entrez un nom dans la zone **Nom du service**. Un nom par défaut est fourni. Vous pouvez le changer dans la zone ou le
conserver.

3. Renseignez les autres zones ou effectuez les sélections requises, puis cliquez sur **Créer**.

Si vous utilisez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour demander une instance de service, téléchargez votre application localement, ouvrez la ligne de commande puis accédez au répertoire de l'application.

1. Exécutez la commande suivante pour ajouter un service à votre application. Vous pouvez sélectionner un service déjà activé sur votre compte ou ajouter un nouveau service.

  ```bash
  ibmcloud dev edit
  ```
  {: pre}

2. Suivez les invites pour sélectionner un groupe de ressources et pour créer et connecter à votre application (Cloudant, par exemple) un service lié aux données. Il peut être nécessaire de sélectionner une région et un plan pour le service.
3. Lorsque le service est créé, plusieurs fichiers (notamment les données d'identification) sont ajoutés au répertoire d'application afin que vous puissiez plus facilement intégrer le service à votre application. Vous pouvez fusionner manuellement des fichiers ou ignorer cette étape pour l'instant.

Vous ne pouvez lier une instance de service qu'aux instances d'application se trouvant dans le même espace ou la même organisation. Toutefois, vous pouvez utiliser des instances de service provenant d'autres espaces ou d'autres organisations, à l'instar d'une application externe. Au lieu de
créer une liaison, utilisez les données d'identification afin de configurer directement votre instance d'application. Pour plus d'informations sur la façon dont les applications externes utilisent les services {{site.data.keyword.Bluemix_notm}}, voir [Utilisation des services {{site.data.keyword.Bluemix_notm}} avec des applications externes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](#accser_external){: new_window}.

## Configuration de votre application
{: #config}

Une fois que vous avez lié une instance de service à votre application, vous devez configurer votre application pour
qu'elle interagisse avec le service.

Chaque service peut nécessiter un mécanisme différent pour communiquer avec les applications. Ces mécanismes sont documentés dans la définition de service, dont vous disposez lorsque vous développez des applications. Pour assurer une cohérence, les mécanismes sont requis pour que votre application interagisse avec le service.

* Pour interagir avec des services de base de données, utilisez les
informations fournies par {{site.data.keyword.Bluemix_notm}}, comme l'ID utilisateur, le mot de passe et l'URI
d'accès pour l'application.
* Pour interagir avec des services de back end mobile, utilisez les informations fournies par
{{site.data.keyword.Bluemix_notm}}, comme l'identité de l'application, les informations de sécurité propres au
client et l'URI d'accès pour l'application. En général, les services mobiles fonctionnent en contexte les uns avec les autres de sorte que les informations de contexte, comme le nom du développeur de l'application et l'utilisateur qui utilise l'application, puissent être partagées entre les services.
* Pour interagir avec des applications Web ou le code de cloud côté client pour les applications mobiles, utilisez les informations fournies par
{{site.data.keyword.Bluemix_notm}}, comme les données d'identification d'exécution dans la variable
d'environnement *VCAP_SERVICES* de l'application. La valeur de la variable d'environnement *VCAP_SERVICES* est la sérialisation
d'un objet JSON. La variable contient les données d'exécution requises pour interagir avec les services auxquels l'application est liée. Le format des données varie selon les services. Reportez-vous à la documentation du service pour plus de détails sur la manière d'interpréter chaque élément d'information.

Si un service que vous liez à une application tombe en panne, il se peut que l'application s'arrête ou présente des erreurs. {{site.data.keyword.Bluemix_notm}} ne redémarre pas automatiquement l'application pour assurer la reprise à la suite de ces problèmes. Envisagez de coder votre application afin d'identifier les pannes et
d'assurer la reprise après une indisponibilité, une exception ou une panne de connexion. Pour plus d'informations, voir [Les applications ne sont pas redémarrées automatiquement](/docs/troubleshoot/ts_apps.html#ts_apps_not_auto_restarted).

## Accès à des services via des environnements de déploiement {{site.data.keyword.Bluemix_notm}}
{: #migrate_instance}

{{site.data.keyword.Bluemix_notm}} propose un grand nombre d'options de déploiement et vous pouvez accéder à un service qui s'exécute dans un environnement à partir d'un autre environnement. Par exemple, si vous avez un service qui s'exécute dans Cloud Foundry, vous pouvez accéder à ce service à partir d'une application qui s'exécute dans un cluster Kubernetes.

### Exemple : Accès à un service Cloud Foundry à partir d'un pod Kubernetes

Pour accéder à un service Cloud Foundry à partir d'un pod dans un cluster Kubernetes, vous devez lier le service à votre cluster pour stocker les données d'identification pour le service dans une valeur confidentielle de Kubernetes. Vous pouvez ensuite mettre ces informations à disposition de votre application. 
{: shortdesc}

Les données d'identification pour le service qui sont stockées dans une valeur confidentielle de Kubernetes sont codées en base64 et chiffrées en etcd par défaut. 

**Important** : Ne référencez ou n'exposez pas vos données d'identification pour le service directement dans votre fichier YAML de déploiement. Les fichiers YAML de déploiement ne sont pas conçus pour contenir des données sensibles et ne chiffrent pas vos données d'identification pour le service par défaut. Pour stocker ces informations et y accéder correctement, vous devez utiliser une valeur confidentielle de Kubernetes. 

1. [Liez le service à votre cluster](/docs/containers/cs_integrations.html#adding_cluster). 
2. Pour accéder aux données d'identification de votre service à partir du pod de votre application, choisissez l'une des options suivantes : 
   - [Monter la valeur confidentielle en tant que volume sur votre pod](#mount_secret)
   - [Référencer la valeur confidentielle dans les variables d'environnement](#reference_secret)

## Activation d'applications externes
{: #accser_external}

Vous pouvez disposer d'applications créées et exécutées en dehors de {{site.data.keyword.Bluemix_notm}}, mais également utiliser des outils tiers. Si des services {{site.data.keyword.Bluemix_notm}} fournissent des clés de service accessibles depuis Internet, vous pouvez utiliser ces services dans vos applications locales ou dans des outils tiers.

Les services suivants vous fournissent des clés de service pour un usage externe :

* {{site.data.keyword.alertnotificationshort}} <!--Alert Notification-->
* {{site.data.keyword.sparks}} <!--Analytics for Apache Spark-->
* {{site.data.keyword.blockchain}} <!--Blockchain-->
* {{site.data.keyword.cloudant}} <!--Cloudant&reg; NoSQL DB-->
* {{site.data.keyword.conversationshort}} <!--Conversation-->
* {{site.data.keyword.discoveryshort}} <!--Discovery-->
* {{site.data.keyword.geospatialshort_Geospatial}} <!--Geospatial Analytics-->
* {{site.data.keyword.GlobalizationPipeline_short}} <!--Globalization Pipeline-->
* {{site.data.keyword.appconserviceshort}} <!--IBM&reg; App Connect-->
* {{site.data.keyword.languagetranslatorshort}} <!--Language Translator-->
* {{site.data.keyword.dwl_short}} <!--Lift-->
* {{site.data.keyword.messagehub}} <!--Message Hub-->
* {{site.data.keyword.nlclassifiershort}} <!--Natural Language Classifier-->
* {{site.data.keyword.objectstorageshort}} <!--Object Storage-->
* {{site.data.keyword.personalityinsightsshort}} <!--Personality Insights-->
* {{site.data.keyword.mobilepush}} <!--Push-->
* {{site.data.keyword.speechtotextshort}} <!-- Speech to Text-->
* {{site.data.keyword.streaminganalyticsshort}} <!--Streaming Analytics-->
* {{site.data.keyword.texttospeechshort}} <!--Text to Speech-->
* {{site.data.keyword.toneanalyzershort}} <!--Tone Analyzer-->
* {{site.data.keyword.weather_short}} <!--Weather Company Data-->
* {{site.data.keyword.workloadscheduler}} <!--Workload Scheduler-->

Pour autoriser une application externe ou un outil tiers à utiliser un service {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Demandez une instance du service.
    1. Dans le tableau de bord de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, cliquez sur **Créer une ressource**. Le catalogue s'affiche.
    2. Dans le catalogue, sélectionnez le service de votre choix en cliquant sur la vignette correspondante. La page des détails du service s'ouvre.
    3. Dans la fenêtre du service, conservez la sélection par défaut de la liste **Connecter à :**: sur **Laisser non lié**. Cette sélection signifie que le service n'est pas connecté à une application {{site.data.keyword.Bluemix_notm}}.
    4. Faites toutes les sélections requises. Ensuite, cliquez sur **Créer**. Une instance de service est créée et le tableau de bord du service s'affiche.
2. Dans le tableau de bord du service, vous pouvez sélectionner **Données d'identification pour le service** pour afficher ou ajouter des données d'identification au format JSON. Sélectionnez un ensemble de données d'identification, puis cliquez sur **Afficher les données d'identification** dans la colonne Actions. Utilisez la clé d'API affichée comme données d'identification pour vous connecter à l'instance de service.

Votre application qui s'exécute en dehors de {{site.data.keyword.Bluemix_notm}} peut désormais accéder au
service {{site.data.keyword.Bluemix_notm}}.

**Remarque :** si vous souhaitez supprimer des instances de service ou consulter les informations de facturation, vous devez revenir à votre tableau de bord dans l'interface utilisateur afin de gérer les instances de service.

## Création d'une instance de service fournie par l'utilisateur
{: #user_provide_services}

Certains de vos services peuvent être gérés en dehors de {{site.data.keyword.Bluemix_notm}}. Si vous disposez des données d'identification permettant d'accéder à ces services externes depuis Internet, vous pouvez créer des instances de service {{site.data.keyword.Bluemix_notm}} fournies par l'utilisateur afin de représenter vos services externes et de communiquer avec eux.

Pour créer une instance de service fournie par l'utilisateur et la lier à une application, procédez comme suit :

1. Créez une instance de service fournie par l'utilisateur avec la commande `ibmcloud service user-provided-create` :
    * Pour créer une instance de service fournie par l'utilisateur générale, utilisez l'option **-p** et séparez les noms de paramètre par une virgule. L'interface de ligne de commande `ibmcloud` vous invite alors à entrer chacun des paramètres. Exemple :
        ```
        ibmcloud service user-provided-create testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Pour créer une instance de service qui envoie des informations à un logiciel de gestion de journal tiers, utilisez l'option `-l`. Indiquez la destination fournie par le logiciel de gestion des journaux tiers. Exemple :

        ```
        ibmcloud service user-provided-create testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    Pour mettre à jour un ou plusieurs paramètres de l'instance de service fournie par l'utilisateur, utilisez la commande `ibmcloud service user-provided-update`.

    * Pour mettre à jour une instance de service fournie par l'utilisateur générale, utilisez l'option **-p** et spécifiez les clés et les valeurs des paramètres dans un objet JSON. Exemple :

        ```
        ibmcloud service user-provided-update testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Pour créer une instance de service qui envoie des informations à un logiciel de gestion de journal tiers, utilisez l'option `-l`. Exemple :

        ```
        ibmcloud service user-provided-create testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Liez l'instance de service à votre application avec la commande `ibmcloud service bind`. Exemple :

	```
	ibmcloud service bind myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

A présent, vous pouvez configurer votre application afin d'utiliser les services externes. Pour savoir comment configurer votre application pour l'interaction avec un service, voir [Configuration de votre application pour l'interaction avec un service ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](#config){: new_window}.
