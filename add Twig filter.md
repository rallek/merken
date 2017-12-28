There was a need to use the php function http://php.net/manual/de/function.htmlentities.php in a template. This is simple to add:

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


