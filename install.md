# module installer changes

I want to have some presets during installation. You have to change the installer in the module root as following:

````
class ShowRoomModuleInstaller extends AbstractShowRoomModuleInstaller
{
    // feel free to extend the installer here
	public function install()
	{
		$result = parent::install();
		if (true === $result) {
			// eigene Werte setzen
			$this->setVar('enableShrinkingForShowRoomItemTitleImage', true);
		}
		return $result;
	}
}
````