# GitBook PlantUml Plugin

* inspired by [romanlytkin/gitbook-plantuml](https://github.com/romanlytkin/gitbook-plantuml)

The plugin now supports two APIs for generating PlantUML diagrams:
* [bitjourney/plantuml-service](https://github.com/bitjourney/plantuml-service)
* [PlantUML Server](http://www.plantuml.com/plantuml/)


## Installation

* Add the plugin to your book.json

```js
{
  "plugins": ["plantuml-cloud"]
}
```

* Install the plugin to you gitbook

```$ gitbook install```

* No additional steps required

## Configuration

* If you do not add a plugin configuration to your book.json, then the following defaults will be used:

| Configuration option | Description | Default |
| -------------------- | ----------- | ------- |
| umlPath | Path to a directory where the generated images for the diagrams will be cached. | "assets/images/uml" |
| type | Determines the type of the server side API | "plantuml-service" |
| host | Host for the diagramming service | "plantuml-service.herokuapp.com" |
| port | Port number for the diagramming service | 80 |
| protocol | https or http | "https" |
| path | URL Fragment which will be appended to the host part | "/svg" |
| blockRegex | Regular expression to select the diagramming text blocks. | ^```uml((.*\n)+?)?```$ |

* If want to use the PlantUML Server API the following changes need to be made to the plugin configuration in your book.json:

```js
{
  "plugins": ["plantuml-cloud"],
  "pluginsConfig": {
    "plantuml-cloud": {
      "protocol": "http",
      "type": "plantuml-server",
      "host": "www.plantuml.com",
      "path": "/plantuml/svg/"
    }
  }
}
```

> The PlantUML Server API on plantuml.com expects the diagram text blocks in a special encoding. [Look here for more information.](http://plantuml.com/pte)
> To make this encoding work in this plugin it was necessary to include some code for the deflate operations. [Look here for more information.](https://github.com/johan/js-deflate)

* [x] Make the plugin work with nodejs zlib deflate implementation and remove the duplicated deflate code.
