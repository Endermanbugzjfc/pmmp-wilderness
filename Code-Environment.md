## Code API (a.k.a. library, SDK)
Unless otherwise specified, the API for plugin development questions is assumed to be the latest commit on the PocketMine repo, on the master branch or any branch that is considerably dominant in development (such as the `core-rewrite` or `mcpe-0.12` branches in the past), at the time of posting, as well as that on any other repos of dependency plugins specified.

## Code context
If no context is given, any code put in \[PHP\] tags is assumed to be in the context of (a non-static class method in) a plugin's main class, run in the main thread. A context **only** refers to _where_ the code is put at, not _when_ the code is run (i.e. the stack is not relevant, e.g. in a task, in an event handler, in a command handler, doesn't matter). In simple words, this context should only affect the values of `$this`, `self::` and `static::`. (`parent::` is assumed to be equivalent to `PluginBase::`).

## Variable names
Here are some variables that are common sense under some contexts:
* `$this`: see [above](#code-context)
* `$cmd`: abbreviation of `$command`
* `$ev`, `$evt`: abbreviation of `$event`
* `$main` or `$plugin` refers to the singleton instance of the main class of the plugin (the one that you can get from `PluginManager::getPlugin()`, in case there is discussion about multiple instances of the main class)
* `$task` can refer to a Task or an AsyncTask. Forum members are encouraged to emphasize that AsyncTask is not a subclass of Task, and to emphasize if you are using an AsyncTask rather than a Task.
* Variables that are lowercase of (the last word of) simple class names (e.g. `$player` for `Player`, `$scheduler` for `ServerScheduler`): _the_ singleton instance, or should-be-given values appropriate in that context, of the named class. For example, `$player` refers to an appropriate instance of `Player` (if the question is asking about how to do things *on a player*), and `$event` refers to the current event in event handlers (the event in the nearest stack level if an event is fired within another).
* In addition to the above rule, the plural form of these words, such as `$players`, refers to an array or a [`Traversable`](//php.net/traversable) or instances of that type.

If a variable contains values provided in the question or other places, the type of the variable should be specified (the class of an object variable, the type of a resource variable, or the scalar type of a scalar variable).

## Method names
As mentioned [above](#code-context), the context of a method is assumed to be in the main class if not specified, and therefore methods like `onEnable`, `onCommand` are assumed to override/implement their parent implementations.

Exceptionally, the method `onRun($t)` (the parameter name doesn't matter) refers to an implementation of a `PluginTask`.

A public method that accepts only one parameter that is an event is assumed to be a registered event handler function.

## Class names
A class may be referred to with its simple name (namespace removed). However, some names exist with the same name in different namespaces in PocketMine, so here lists some assumptions of what they refer to. Here also lists some commonly-used aliases.
* `Item`: We usually assume it to be `pocketmine\item\Item`, especially if `Item::get()` is used
* `DroppedItem` or `ItemEntity` is the alias for `pocketmine\entity\Item` if `pocketmine\item\Item` is also used in the same code snippet
* `ItemItem` or `Item` is the alias for `pocketmine\item\Item` if `pocketmine\entity\Item` is also used in the same code snippet
* `ProtocolInfo` for `pocketmine\network\protocol\Info
* `TallGrass` is assumed to be `pocketmine\block\TallGrass`
* `TallGrassPopulator` for `pocketmine\level\generator\populator\TallGrass`
* `TallGrassObject` for `pocketmine\level\generator\object\TallGrass`
* `ObjectOre` for `pocketmine\level\generator\object\Ore`
* `ObjectTree` for `pocketmine\level\generator\object\Tree`
* `Chest` is assumed to be `pocketmine\tile\Chest`
* `TileChest` for `pocketmine\tile\Chest`
* `ChestBlock` for `pocketmine\block\Chest`
