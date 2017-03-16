I learned today how to add a new table column and a new modvar. Both is quite easy.

You have to add to your installer the following function:

````
public function upgrade($oldVersion)
{
switch ($oldVersion) {

	 case '0.3.0':
				// add theYoutubeCode into rk_showroom_showroomalbum
				$sql = '
					ALTER TABLE `rk_showroom_showroomalbum` ADD `theYoutubeCode` VARCHAR( 11 ) NOT NULL AFTER `image` 
				';
				$this->entityManager->getConnection()->exec($sql);
				// add theYoutubeCode into rk_showroom_storyalbum
				$sql = '
					ALTER TABLE `rk_showroom_storyalbum` ADD `theYoutubeCode` VARCHAR( 11 ) NOT NULL AFTER `image` 
				';
				$this->entityManager->getConnection()->exec($sql);
				// add modVar 
				$this->setVar('doNotUseTitleImage', false);
	case '0.4.1':
				$this->setVar('enabledFinderTypes', [ 'showRoomItem' ,  'showRoomAlbum' ,  'story' ,  'storyAlbum' ]);
}

// update successful

 return true;

 }	
	
}
````

# adding a column
you need an sql statement. e.g. ``ALTER TABLE `rk_showroom_showroomalbum` ADD `theYoutubeCode` VARCHAR( 11 ) NOT NULL AFTER `image` ``.
The easiest way to get the right code is by using phpAdmin. If you add your new column by hand you will also get the sql statement. Great thing!

This mus be handled like shown in the example.

# adding a Molule Variable
That is even more simple. Look inside the abstact installer for the generated statement and copy the line (starting with ``$this->setVar...``

# the case statement
for the current old version you have to say what should happen . so add a new ``case '0.0.0': ``. This will be followed by the job to be done in the database.


