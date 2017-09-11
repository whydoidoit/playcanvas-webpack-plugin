### Introduction

WebPack plugin to upload built script files to PlayCanvas. 

### Installation

```language-shell
npm install --save playcanvas-webpack-plugin
```

### Usage

1. Build your WebPack output and drag and drop it into PlayCanvas editor.

2. Select the file and note it's Asset Id.  Use this in your WebPack 
configuration.

3. Also note your Project ID from PlayCanvas. It's in the URL of the project overview page and elsewhere.

4. In your webpack config add the plugin and configure its options:


```language-javascript

var PlayCanvasWebpackPlugin = require('playcanvas-webpack-plugin')

module.exports = {
    
    //...
    
    entry: {
        "your_build": './path/to/entry/point.js'
        //...
    },
        
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: '[name].output.js',             //Example only, use what you like
        publicPath: '/'
    },
        
    //...
    
    plugins: [
       
        //...
        
        new PlayCanvasWebpackPlugin({
            
            bearer: 'YOUR_BEARER_TOKEN',          // From your organisation API tokens (or network tab in dev tools)
            project: YOUR_PROJECT_ID,             // From the url of the launch page of your project
            files: {
                "your_build.output.js": {         //Name of your build output
                    path: "your_build.output.js", //Name in PlayCanvas, normally the same
                    assetId: ASSET_ID             //Asset ID from the step above
                }
            }
        })
        
    ]
    
    //...
}

```
