#Contrôleurs

Dans une application MVC, les Contrôleurs se placent entre les Modules et les Vues. Ils passent l'information aux modèles lorsque les données nécessitent des traitements et ils demandent l'information nécessaire aux modules. Les Contrôleurs transmettent les informations du Modèle aux Vues qui contiennent le code à afficher aux utilisateurs.

Les contrôleurs sont appelés par rapport à l'URL appelée, pour plus d'informations consulter la documentation sur [les URLs et les Liens](about.urls).

## Nommage des contrôleurs et fonctionnement

Le nom d'un contrôleur doit correspondre exactement au nom de fichier.

**Conventions d'écriture**

* les nom de fichiers des contrôleurs doivent �tre en minuscule, e.g. `articles.php`
* ils doivent �tre situés dans le (sous-)dossier **classes/controller**, e.g. `classes/controller/articles.php`
* la classe du contrôleur doit correspondre au fichier, commencer par une majuscule et �tre préfixée par **Controller_**, e.g. `Controller_Articles`
* elle doit héritée de la classe Controller
* les méthodes du contrôleur doivent �tre précédées de **action_** (e.g. `action_do_something()` ) pour pouvoir �tre appelées par rapport à l'URL



### Un contrôleur simple

Ci-dessous un exemple de contrôleur qui affiche Hello World à l'écran.

**application/classes/controller/article.php**
~~~
<?php defined('SYSPATH') OR die('No direct access allowed.');
 
class Controller_Article extends Controller
{
    public function action_index()
    {
        echo 'Hello World!';
    }
}
~~~
Si vous entrez alors l'URL yoursite.com/article dans votre navigateur (ou yoursite.com/index.php/article sans URL rewritting) vous devriez voir appara�tre:
~~~
Hello World
~~~
C'est tout pour votre premier contrôleur. Toutes les conventions ont été appliquées.



### Un contrôleur plus avancé

Dans l'exemple ci-dessus la méthode `index()` est appelée par l'URL yoursite.com/article. Si le second segment de l'URL est vide, la méthode index est appelée par défaut. Elle pourrait aussi �tre appelée en entrant l'URL yoursite.com/article/index.

_Si le second segment de l'URL n'est pas vide, il détermine la méthode du contrôleur à appeler._

**application/classes/controller/article.php**
~~~
class Controller_Article extends Controller
{
    public function action_index()
    {
        echo 'Hello World!';
    }
 
    public function action_overview()
    {
        echo 'Article list goes here!';
    }
}
~~~
Maintenant, si vous entrez l'URL yoursite.com/article/overview vous devriez voir appara�tre:
~~~
Article list goes here!
~~~


### Un contrôleur avec des arguments

Imaginons que l'on souhaite afficher un article particulier, identifi� par l'id `1` et le titre `your-article-title`.

L'URL ressemblerait alors � yoursite.com/article/view/**your-article-title/1**. Les 2 derniers segments sont pass�es � la m�thode view() du contrôleur.

**application/classes/controller/article.php**
~~~
class Controller_Article extends Controller
{
    public function action_index()
    {
        echo 'Hello World!';
    }
 
    public function action_overview()
    {
        echo 'Article list goes here!';
    }
 
    public function action_view($title, $id)
    {
        echo $id . ' - ' . $title;
        // you'd retrieve the article from the database here normally
    }
}
~~~
Si vous appelez yoursite.com/article/view/**your-article-title/1** vous devriez voir appara�tre:
~~~
1 - your-article-title
~~~
