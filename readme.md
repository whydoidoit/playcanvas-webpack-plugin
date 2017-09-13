### Introduction

WebPack plugin to upload built script files to PlayCanvas. 

### Installation

```shell
npm install --save playcanvas-webpack-plugin
```

### Usage

1. Build your WebPack output one time.

2. Go to the PlayCanvas editor for your project on the web and open your developer tools.

3. Drop the build file into the assets window.

4. In the javascript console type config.accessToken - use this as your bearer token later

5. In the javascript console type config.project.id - use this as your project id later

6. Select the build file you dropped in the assets window of the PlayCanvas editor and note its
Asset Id in the properties panel.  Use this in your WebPack configuration along with 
the bearer token and the project id.

7. In your webpack config add the plugin and configure its options:


```javascript

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
