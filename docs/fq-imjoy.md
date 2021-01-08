[![powered by ImJoy](https://imjoy.io/static/badge/powered-by-imjoy-badge.svg)](https://imjoy.io/)

# FISH-quant in ImJoy

We provide several plugins to provide a convenient user-interface permitting the most common
analysis tasks.

to get a first feeling for how the data processing with FISH-quant looks like when using
our ImJoy plugins, you can use the embedded version below. For this, simply press on the `Run` button.

## IMPORTANT - please read FIRST

1. These analysis require a **Python plugin engine** to perform the analysis. You can run this engine on mybinder.org, which means that no local installation is required. For large-scale analysis, we recommend installation of a local eninge, as described in the [**documentation**](https://fq-imjoy.readthedocs.io/en/latest/). 
2. For this documentation, FISH-quant **runs on a remote server provided by mybinder.org**. Starting this server and installing the necessary libraries can take a few minutes. So be patient.
3. We provide some **sample data** that you can try to analyze.

## Analyze smFISH images in the browser

Pressing the `Run` button below, to launch the ImJoy plugin. This can take a bit of time, since
a remote server is spinning up for you.

?> Below we provide the **basic steps of the analysis**. More details you can find the detailed [**documentation**](https://fq-imjoy.readthedocs.io/en/latest/), or for many steps you can find a little question mark. Pressing
on this button will open the documentation at the relevant page directly in ImJoy.

<!-- ImJoyPlugin: { "type": "web-worker", "hide_code_block": true} -->
```js
class ImJoyPlugin{
    async setup(){
    }
    async run(ctx){
        // create an imjoy app window
        // use imjoy.createWindow instead of api.createWindow will make the window appear inside the embedded ImJoy App
        const imjoy = api; //await api.createWindow({src: "https://imjoy.io/#/app?workspace=sandbox&flags=quiet"});
        
       // Connect to mybinder 
       try{
            const engineManager = await imjoy.getPlugin("Jupyter-Engine-Manager")
            await engineManager.createEngine({
                                    name: "MyBinder Engine",
                                    url: "https://mybinder.org",
                                    spec: "oeway/imjoy-binder-image/master"
                                })
        }
        catch(e){
            await imjoy.alert("Failed to connect to Jupyter notebook engine on MyBinder.org, error: " + e.toString())
        }

        // Start FISH-quant
        const plugin = await imjoy.getPlugin("https://github.com/fish-quant/fq-imjoy/blob/master/imjoy-plugins/FISH-quant.imjoy.html")
        await plugin.run({config: {}, data: {}})
    }
}
api.export(new ImJoyPlugin())
```

### Analyze test data

1. **Get data** (tab `Data specifications`)
    1. **Download (test) data** by pressing on button `Download zipped data`. This will open a prompt with the a prefilled url to download the data. You can also use this link to download the data on your local machine (see below for details).After confirmation data will be downloaded and is available for processing. We also set a few custom parameters to get starter quickly.
    1. **Define regular expression** to tell the plugin how to infer information about channel, position, and the experiment from the file-name. The provided regular expression works for the test data. While this might look complicated, it provides lots of flexibility to import files with different naming conventions.
    1. **Add the channel to be processed**. Here you can define the channel(s) that you want to analyze. The prefilled parameter are defined for the test data. Press on button `Add` to tellplugin to process this channel
    1. **Scan** the folder for all images that can be processed. All images that fit the regular expression and contain the specified channel(s) will be listed
    1. **Load one image** by pressing on the upload button next to it. You can double-click on the image to open it in our viewer.

2. **Spot detection** (panel `Spot detection`)
    1. **Filter** image to reduce background and increase the signal of the spots. You can again double-click on the image to load it. The raw image will be shown as well, and you can toggle between the two.

    ?> You can change the size of the kernels to see how the filtered image is affected.
    1. **Test different intensity values for detection**: you can specify a range of intensity values that will be used to detect spots in the filtered image by pressing on the button `Test threhold`. The number of detections as a function of the intensity threshold will be shown in the plot. 
    2. Choose a **intensity threshold** either by selecting a point on the curve, or specifying it directly, and press the the button `Apply detection treshold`. Once the detection is finished, our viewer will be shown with the detection results and the images.

    ?> You can play around with the detection threshold to see how this value affects the detection
    1. **Process** all image(s) by pressing on the button in the lowest part of the interface.

### Additional options

Above we only describe a basic workflow. Other interesting options include

1. Limit the analysis to define you paramter to a smaller subregion. This accelerates the processing.
2. Decompose dense areas of RNA aggregation.

## Local installation

If you want to analyze your own data wiht a local installation, please consult our detailed user manual, that you can find [**here**](https://fq-imjoy.readthedocs.io/en/latest/).