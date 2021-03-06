#mogenerator + Xmo'd

Visit the [project's pretty homepage](http://rentzsch.github.com/mogenerator).

Read the [project's backgrounder](http://rentzsch.com/code/mogenerator). Or, for the impatient:

> `mogenerator` is a command-line tool that, given an `.xcdatamodel` file, will generate *two classes per entity*. The first class, `_MyEntity`, is intended solely for machine consumption and will be continuously overwritten to stay in sync with your data model. The second class, `MyEntity`, subclasses `_MyEntity`, won't ever be overwritten and is a great place to put your custom logic.

## Using Xmo'd

Xmo'd (pronounced *ex-mowed*) is an Xcode plugin that integrates mogenerator into Xcode. It saves you the hassle of having to write a *Run Script Build Phase* and/or manually adding+removing source files from your project as you add+remove entities.

Xmo'd works by noticing when your `*.xcdatamodel` is saved. If the model file's Xcode project item comment contains `xmod`, an AppleScript is fired that creates a folder based on your model's file name and populates it with derived source code files from your model. It then adds the new folder to your project as a Group Reference and adds all the source files to your project.

## Version History

* **1.15** Mon 2 Nov 2009 [download](http://cloud.github.com/downloads/rentzsch/mogenerator/mogenerator-1.15.dmg)

	* [CHANGE] Xmo'd: now adds `.h` human+machine header files to project (in addition 
to current `.m` + `.mm` files). ([rentzsch](http://github.com/rentzsch/mogenerator/commit/5c88445e366b15d4a4700b7f9a10a6915ff6b20b))

	* [NEW] Now supports key paths in fetch request predicates so long as they're relationships. ([Jon Olson](http://github.com/rentzsch/mogenerator/commit/6bd8051a70d32fe73c1965cb449d2f40d403260a))

	* [FIX] Log fetch-request-wrapper errors to `NSLog()` on iPhone since it lacks `-[NSApp presentError:]`. ([rentzsch](http://github.com/rentzsch/mogenerator/commit/4a834281da07af799206db5099a077fa28721742))

	* [NEW] `+insertInManagedObjectContext:` `NSParameterAssert()`'s its `moc` arg. ([rentzsch](http://github.com/rentzsch/mogenerator/commit/5ff20395ccdcde12955483046ee30ed215d3b920))

* **1.14** Fri 9 Oct 2009 [download](http://cloud.github.com/downloads/rentzsch/mogenerator/mogenerator-1.14.dmg)

	* **IMPORTANT:** 1.14 generates code that may be incompatible with clients of 1.13-or-earlier generated code. `+newInManagedObjectContext:` has been replaced with `+insertInManagedObjectContext:` and method implementations have been replaced with `@dynamic`, which don't work so well with overriding (most of these uses can be replaced with Cocoa Bindings). Upgrade only if you have spare cycles to fix-up existing projects.

	* [CHANGE] changed `+newInManagedObjectContext:` to `+insertInManagedObjectContext:` to satisfy the LLVM/clang static analyser. ([Ruotger Skupin](http://github.com/rentzsch/mogenerator/commit/25ad62d15a21e4ef855f5eb80bee32182a3ad6f4))

	* [CHANGE] Default machine templates now use @dynamic. The old templates still available in ` contributed templates/rentzsch non-dynamic`. ([Pierre Bernard](http://github.com/rentzsch/mogenerator/commit/68e73da2be59f0ae3e60e32a45986aa7b9651a3c))

	* [CHANGE] Xmo'd included again in default mogenerator installation -- the first time since 1.6. ([rentzsch](http://github.com/rentzsch/mogenerator/commit/c092a17734157a9976505bc94744bf0a90432dd7))

	* [CHANGE] Migrated project to github from self-hosted svn+trac installation.

	* [NEW] Xmo'd version checking whitelists Xcode versions 3.1(.x) and 3.2(.x).

	* [NEW] Dropped ppc support for Xmo'd. May reconsider if folks yelp. ([rentzsch](http://github.com/rentzsch/mogenerator/commit/c6d0ef3fa308c7b1095daaa5364e1c944a772d2e))