# use a variable

````
	{% if getModVar('RKShowRoomModule', 'property01') == false %}
		...
	{% endif %}
````
better instead ``getModVar('RKShowRoomModule', 'property01')`` you use a default value ``getModVar('RKShowRoomModule', 'property01' default value)``. With the default value you are on the safe side if the variable do not exist or is empty.

## Variables for field length
inside the corresponding edit.html.twig you may want to add the maxlength. e.g.
````
{{ form_row(form.descriptionTeaser, { 'attr': { 'maxlength': getModVar('RKShowRoomModule', 'storyTeaserDescriptionLength') }}) }}
````

## override help text
If we want to override the help text with the allowed number of characters we can do as follow:
````
{% set allowedLength = getModVar('RKShowRoomModule', 'descriptionLength', 200) %}
{{ form_row(form.description, { 'attr': { 'maxlength':  allowedLength }, 'help' : __f('Allowed length is %amount% characters.', { '%amount%': allowedLength }) }) }}
````
the original help text is than not available anymore

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
use ``|striptags`` instead of ``|safeHtml`` to ensure you are not cutting html in a tag

# string combination
````
{% set templateTitle = showRoomItem.title ~ ' ' ~ showRoomItem.property01 ~ ' ' ~ showRoomItem.property02 %}
````
in this example I create a new template title. The strings are combined via `` ~ ``