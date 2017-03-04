# use a variable

````
	{% if getModVar('RKShowRoomModule', 'property01') == false %}
		...
	{% endif %}
````
better instead ``getModVar('RKShowRoomModule', 'property01')`` you use a default value ``getModVar('RKShowRoomModule', 'property01' default value)``. With the default value you are on the safe side if the variable do not exist or is empty.

# check for permissions
````
	{% if hasPermission('RKShowRoomModule:ShowRoomItem:', '::', 'ACCESS_EDIT') %}
		...
	{% endif %}
````

# truncate with a variable
````
	{% set truncateLength = getModVar('RKShowRoomModule', 'teaserTruncateStoryListlength', 123) %}
	{{ showRoomItem.descriptionTeaser|striptags|truncate(truncateLength) }}
````
use ``|striptags`` instead of ``|safehtml`` to ensure you are not cutting html in a tag

# string combination
````
{% set templateTitle = showRoomItem.title ~ ' ' ~ showRoomItem.property01 ~ ' ' ~ showRoomItem.property02 %}
````
in this example I create a new template title. The strings are combined via `` ~ ``