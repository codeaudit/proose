[Proose](http://github.com/mdorn/proose) is a RESTful web services wrapper around the [Goose](http://github.com/jiminoc/goose) HTML content extracting library.  It also has limited (5,000 character maximum) support for the unofficial [Google Translate Java API](http://code.google.com/p/google-api-translate-java/).  Proose is based on the [Prudence](http://threecrickets.com/prudence/), the RESTful web platform for the JVM.

To use it, you'll need a JavaScript/Rhino-enabled edition of Prudence.  You'll need to install the `proose` source in your instance's `applications` directory, and install the following dependencies in the `libraries` directory.

* Goose: http://github.com/jiminoc/goose (can be built with Maven)
* (Optional) Google Translate Java API: download jar here: http://code.google.com/p/google-api-translate-java/downloads/list

Once it's up and running, it will return a JSON representation of the main text of the URI you give it within an HTTP POST containing your request data in JSON format:

<code>
curl -i -H "Accept: application/json" -X POST -d '{"uri": "http://threecrickets.com/prudence/rest/"}' http://localhost:8080/proose/page/
</code>

<code>
{
    "title": "Prudence: Scalable REST/JVM Web Development Platform",
    "text": "There's a lot of buzz about REST, but also a lot confusion about what it is and what it's good for. This essay attempts to convey REST's simple essence. Let's start, then, not at REST, but at an attempt to create a new architecture for building scalable applications. Our goals are for it to be minimal, straightforward, and still have enough features to be productive. We want to learn some lessons from the failures of other, more elaborate and complete architectures. ..."
}
</code>

<code>
curl -i -H "Accept: application/json" -X POST -d '{"uri": "http://threecrickets.com/prudence/legal/", "source_language": "en", "target_language": "fr"}' http://localhost:8080/proose/page/
</code>

<code>
{
    "title": "Licence et les marques - Prudence: REST Scalable / Plate-forme de développement Web JVM - Trois grillons",
    "text": "Prudence vous est fourni sous la licence GNU Lesser General Public License version 3.0.\n\nEn outre, nous voulons mentionner expressément que les grillons Trois LLC, le titulaire du droit d'auteur que de tout le code source, n'a pas l'intention de libérer les futures versions du projet Prudence open source sous plusieurs licences restrictives, telles que la GPL. Si nous changeons la licence de nouveau dans l'avenir, il ne pouvait être pour une licence moins restrictive (comme Apache Public License).\n\nNotez que cet accord ne couvre pas les bibliothèques redistribués tiers. Les bibliothèques vous sont fournis à des fins de commodité, mais restent sous leurs licences respectives, qui sont reproduites dans les «licences / *" fichiers. Pour les demandes d'autorisation spéciales, s'il vous plaît contacter Trois grillons LLC."
}
</code>
