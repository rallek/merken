My Guru helped me to add a service for my module made with modulestudio for zikula. This example is for https://github.com/rallek/showroom

The Twig Extension should me help to find out the name of the first level (showRoomItem) of its stories and substories. Stories do have a self relation and can have endless levels.

# declaration of the service
you do need a yml file to create the service. I got this code:
````
services:
    rk_showroom_module.custom_twig_extension:
        class: RK\ShowRoomModule\Twig\CustomTwigExtension
        public: true
        tags:
            - { name: twig.extension }
````
Be shure not to use tab. In yml files we have to use spaces.
This code should be placed inside ``Resources/config/customServices.yml``

# adding the service
to make this service known for the module you have to add this inside the file ``Resources/config/services.yml``. at the edn you have to add 
````
  - { resource: 'customServices.yml' }
````
To avoid overwriting by a new generated version of the module you should add this file to the markFiles inside the setting container of modulestudio.

# creating the extension
Now we do need the extension itself. For this we add a file ``Twig\CustomTwigExtension.php`` (see the ``class:`` in our service declaration)

This file do get the following code:
````
<?php
namespace RK\ShowRoomModule\Twig;

use Twig_Extension;
use RK\ShowRoomModule\Entity\ShowRoomItemEntity;
use RK\ShowRoomModule\Entity\StoryEntity;

/**
 * Custom Twig extension implementation class.
 */
class CustomTwigExtension extends Twig_Extension
{
    /**
     * Returns a list of custom Twig functions.
     *
     * @return array
     */
    public function getFunctions()
    {
        return [
            new \Twig_SimpleFunction('rkshowroommodule_getShowRoomItemForStory', [$this, 'getShowRoomItemForStory'])
        ];
    }

    /**
     * Returns the show room item for a given story.
     *
     * @param StoryEntity $story Story entity
     *
     * @return ShowRoomItemEntity|null
     */
    public function getShowRoomItemForStory(StoryEntity $story)
    {
        $showRoomItem = null;
        $parentStory = $story;
        while (null === $showRoomItem && null !== $parentStory) {
            $showRoomItem = $parentStory->getShowRoomItem();
            $parentStory = $parentStory->getStory();
        }

        return $showRoomItem;
    }
}
````
# Using in a template
To print the title of the root element you have to run this code:
````
{% set storyShowRoomItem = rkshowroommodule_getShowRoomItemForStory(story) %}
{% if storyShowRoomItem is not empty %}
    <p>{{ storyShowRoomItem.title }}</p>
{% endif %}
````

# more Twig Extensions?
you can add more Twig Extensions into CustomTwigExtension.php. This way to implement avoids to touch generated code.
