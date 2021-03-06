There was a need to use the php function http://php.net/manual/de/function.htmlentities.php in a template. This is sample how to add. Other php manipulations are similar.

open your file ``Twig/TwigExtension.php``. It looks like:
````
namespace RK\EventPhotosModule\Twig;

use RK\EventPhotosModule\Twig\Base\AbstractTwigExtension;

/**
 * Twig extension implementation class.
 */
class TwigExtension extends AbstractTwigExtension
{
    // feel free to add your own Twig extension methods here
}
````

Here we can add our filter.

````
     public function getFilters()
     {
         $filters = parent::getFilters();

         $filters[] = new
\Twig_SimpleFilter('rkeventphotosmodule_myFilter', [$this, 'myFilter'], ['is_safe' => ['html']]);

         return $filters;
     }
````
plus
````
     public function myFilter($string)
     {
         // manipulate $string

         return $string;
     }
````

This is an example

````
namespace RK\EventPhotosModule\Twig;

use RK\EventPhotosModule\Twig\Base\AbstractTwigExtension;

/**
 * Twig extension implementation class.
 */
class TwigExtension extends AbstractTwigExtension
{
    // feel free to add your own Twig extension methods here
public function getFilters()
    {
        $filters = parent::getFilters();

        $filters[] = new \Twig_SimpleFilter('rkeventphotosmodule_htmlentitiesFilter', [$this, 'htmlentitiesFilter'], ['is_safe' => ['html']]);

        return $filters;
    }

public function htmlentitiesFilter($string)
    {
        // manipulate $string
		    $string = htmlentities($string);

        return $string;
    }

	 
}
````
With the first function you extend the function in ``Twig/base/AbstractTwigExtension.php``.

In the second function you are doing your filtering.

The usage in a temaplate is like this:
````
{{myString|rkeventphotosmodule_htmlentitiesFilter }}
````


