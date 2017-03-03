# view.html.twig

to hide some items inside the quick navigation you have to use this syntax:
````
    {{ include('@RKShowRoomModule/ShowRoomItem/viewQuickNav.html.twig', {itemLanguageFilter:false, hideMeFilter:false, switchUserFieldsOffFilter:false}) }}
````