# use a variable

````
	{% if getModVar('RKShowRoomModule', 'property01') == false %}
		...
	{% endif %}
````

# check for permissions
````
	{% if hasPermission('RKShowRoomModule:ShowRoomItem:', '::', 'ACCESS_EDIT') %}
		...
	{% endif %}
````