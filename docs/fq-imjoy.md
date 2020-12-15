[![powered by ImJoy](https://imjoy.io/static/badge/powered-by-imjoy-badge.svg)](https://imjoy.io/)

# FISH-quant in ImJoy

We provide several plugins to provide a convenient user-interface permitting the most common
analysis tasks.

to get a first feeling for how the data processing with FISH-quant looks like when using
our ImJoy plugins, you can use the embedded version below. For this, simply press on the `Run` button. 

## IMPORTANT - please read

1. These analysis require a **Python plugin engine** to perform the analysis. You can run this engine on mybinder.org, which means that no local installation is required. For large-scale analysis, we recommend installation a local version of the eninge, as described in the user manual. FISH-quant **runs on a remote server provided by mybinder.org**. Starting this server and installing the necessary libraries can take a few minutes. So be patient. 
2. We provide some **sample data** that you can try to analyze.
3. To **analyze your own data**, see the dedicated section below. 

## Analyze smFISH images in the browser

Pressing the `Run` button below, will launch the ImJoy plugin with the interface. This can take a bit of time, since
a remote server is spinning up for you. 

Below we only the **basic steps of the analysis**, for many steps you can find a little question mark. Pressing
on this button will open the documentation at the relevant page.

<!-- ImJoyPlugin: { "type": "web-worker", "hide_code_block": true} -->
```js
class ImJoyPlugin{
    async setup(){
    }
    async run(ctx){
        // create an imjoy app window
        const imjoy = await api.createWindow({src: "https://imjoy.io/#/app?workspace=sandbox&flags=quite"});
        imjoy.getPlugin("https://github.com/fish-quant/fq-imjoy/blob/master/imjoy-plugins/FISH-quant.imjoy.html").then((plugin)=>{plugin.run({config: {}, data: {}})})
    }
}
api.export(new ImJoyPlugin())
```


1. **Get data** (tab `Data specifications`)
    1. **Download (test) data** by pressing on button `Download zipped data`. This will open a prompt with the a prefilled url to download the data. You can also use this link to download the data on your local machine (see below for details). 
    2. After confirmation data will be downloaded and is available for processing. We also set a few custom parameters. 
    3. **Add the channel to be processed**, the prefilled parameter are correct for the test data. 
    4. **Scan** the folder for all images that can be processed. THis will only be one for the test data. 
    5. **Load image** by pressing on button.
2. **Spot detection** (panel `Spot detection`)
    1. Filter image
    2. Test pre-detection paramters.
    3. Choose a value (somewhere in the plateau)
    4. Process all images.

## Analyzing your own data


## Local installation

