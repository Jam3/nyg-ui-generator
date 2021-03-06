# nyg-ui-generator
Generator is based on [nyg](https://www.npmjs.com/package/nyg) and [nyg-module-generator](https://www.npmjs.com/package/nyg-module-generator).

## Prerequisites

Following modules need to be installed globally:
* [nyg](https://www.npmjs.com/package/nyg) 
* [nyg-module-generator](https://www.npmjs.com/package/nyg-module-generator)
* [ghrepo](https://github.com/Jam3/ghrepo)

install:
```
npm i ghrepo -g
npm i nyg -g
npm i nyg-module-generator -g
```

`nyg-module-generator` will prompt to set your `init.author.name`, `init.author.email` and `init.author.github` if it's not already set. You can check existing configs using `npm config get` and set missing props using `npm config set someProp "some-value"`

## Install
```
npm i nyg-ui-generator -g
```

## Basics
```
nyg nyg-ui-generator
```

There are 3 options:

- **Generate a boilerplate UI component**. The available types are *React, React-f1,* and *Bigwheel*
- **Create a UI Module**. Create a UI node module of a specified type that can be published to github and npm.
- **Post Publish**. Publish an existing generated component as a module. Creating a UI module will also perform this action.

You will then be prompted with a number of questions, which will define the type of UI component you want to generate, where to put it, and whether you want to publish it. A user flow diagram detailing these interactions is available [here](https://docs.google.com/presentation/d/1Fc0p_LC4s2bE6acedVbCg13IkN-QMR0R24pfzfWTCUE/edit?ts=57b2198f#slide=id.g12acd49da1_0_14). Details are also available in the usage section [below](#usage)
 
## Arguments

You can pass in command line arguments to the ui generator that specify the type, folder name, folder location and component type. running `nyg nyg-ui-generator -h` will bring up the available options and their descriptions.

```shell
Usage: nyg [options] [command]
  
  Commands:
  
    help  Display help
  
  Options:
  
    -a, --action    The desired action (module, boilerplate, postpublish)
    -f, --folder    The name of the ui folder
    -h, --help      Output usage information
    -l, --location  The location of the ui folder
    -n, --name      The name of the ui component
    -t, --type      The type of component to be made (react, react-f1, bigwheel)
    -v, --version   Output the version number

``` 
These arguments are currently for the `boilerplate` action only.

## Usage

There are 3 actions possible when using the UI generator.

**1. Generate UI component files** - simply create boilerplate files (js, styles, templates). 
Recommended to run generator from project's root for this option.
Generator will prompt the following questions:
 * path - where to put the new component (default: cwd)
 * component folder name - folder to be created under specified path (default: MyComponent)
 * component name - component's class name inside JS file (default: MyComponent)
 * UI type (React, React-F1, or Bigwheel)
 * whether the user want to rename your index.js (e.g MyComponent.js). Default is 'No'
 
Generator will copy files into new component folder and show it in your file browser

**2. Create UI module** - generate UI module with boilerplate files and set up test and example. Suggested that you have a specific global folder for all your generated modules. 
Generator will prompt the following questions:
 * path - where to put the new component (default: your modules folder e.g `/Users/name/modules/`)
 * module name - respective folder will be created under specified path
 * module specific questions such as description, kew words etc
 * component name - component's class name inside JS file (default: MyComponent)
 * UI type (React, React-F1, or Bigwheel)
 
Generator will copy appropriate files into new component folder, install dependencies, open component folder in the file viewer and run example in the web browser.

Afterwards, the user will be asked about publishing the UI module to GitHub and npm.

**3. Post publish** - publish existing component as module. **IMPORTANT: to run this, you have to be in the component folder**. Generator will try to read existing config file and get the information about UI type, index file name, etc.
 
When reading `nyg-cfg.json`:
  * if there's a file named`index.js` or there's only one JS file exists in the component root, or config file contains rename informaion, the respective file will be assigned as index. Otherwise, the user will be asked to choose it from the list
  * if there's no UI type information contained in the config file, the user will be prompted to choose it from the list
 
Note: Should any problem arise during reading reading ```nyg-cfg.json``` with further unexpected generator exit, the user can try removing the config file, then they will be prompted for missing info.

Generator will proceed with similar to **Create UI module** steps. Suggested that files will be copied to and published from your default modules folder (e.g. `/Users/name/modules/`) which you will be asked about upon installation.

Generator will try to detect all dependencies (modules as well as local files) based on imports (requires) reading them recursively, then install all module dependencies and bring all local dependencies into ```lib``` folder inside your target directory, overwriting import paths. Note that this will use ```acorn-jsx``` module to parse your jsx and some syntax may not be supported such as ```static```, so you would have to resolve it manually.

## Test
To manually run the example in your browser
```
cd your-ui-component-directory
npm start
```

To manually run test
```
cd your-ui-component-directory
npm test
```

## License

MIT, see [LICENSE.md](http://github.com/Jam3/nyg-ui-generator/blob/master/LICENSE.md) for details.
