### Introduction

WebPack plugin to upload built script files to PlayCanvas. 

### Installation

```shell
npm install --save playcanvas-webpack-plugin
```

### Usage

1. Build your WebPack output one time.

2. Go to your account settings and scroll down to API Tokens and generate a new one.

2. Go to the project overview page and copy the project id from the URL.

3. Go to the PlayCanvas editor for your project on the web.

4. Go to version control and note the branch id of the current/wanted branch.

5. Drop the build file into the assets window.

6. Select the build file you dropped in the assets window of the PlayCanvas editor and note its
Asset Id in the properties panel.  Use this in your WebPack configuration along with 
the API token, branch id and the project id.

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
            
            bearer: 'YOUR_BEARER_TOKEN',          // From the step above
            project: YOUR_PROJECT_ID,             // From the step above
            branchid: YOUR_BRANCH_ID,             // From the step above
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

You can use an additional option of `skipUpload` if you want to have conditional build
logic to not upload your output files.
