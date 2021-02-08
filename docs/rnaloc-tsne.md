[![powered by ImJoy](https://imjoy.io/static/badge/powered-by-imjoy-badge.svg)](https://imjoy.io/)

# Data visualization and inspection in ImJoy

## Motivation 

ImJoy permits to build plugins using state-of-art visualization tools.

Here, we provide an example for an interactive data explorer. For illustration purposes,
we use some data from one of our recent publications, where we study the link between 
RNA localization and local translation. For more details see the publication in [**Developmental Cell**](https://www.sciencedirect.com/science/article/abs/pii/S1534580720305840), or for a shorter version the nice [**preview**](https://www.sciencedirect.com/science/article/pii/S1534580720307085) from Chin & Lecuyer.

![paper_cell-dev.jpg](assets/paper_cell-dev.jpg ':size=600')

## The actual plugin

?> We analyze more than 9000 individual cells from different genes, and grouped them based on similarity
in their localization pattern. While the created t-SNE plot is already very informative, adding interactivity
further increases the understanding we can obtain from this analysis.

To illustrate how ImJoy can be used to create interactive data inspection tools, we build an interactive t-SNE plot.
This plugin will retrieve the data, and show the t-SNE. **This plot is interactive**, so play around!

- Each dot is a cell, when clicking on it the corresponding image will open and also a bar plot with the localization classes. 
- You can **zoom into** the plot to better resolve dense regions.
- In the menu you can find a dropdown menu where you can **highlight different localization** classes in t-SNE plot
  - Manual annotation: we manually annotated a subset of cells which will be color-coded based on this annotation.
  - Name of different localization classes: this will show the probability for a given cell to belong to the selected localization class. 
    We estimated this probability with an automated classification approach (for more details consult the paper).
    **different localization classes**, once selected the plot will be color coded according to the assigned probability for this classes.
- In the search box (upper right corner), you can **search for any string contained in the file-name**, e.g. `Rab13`, to specifically show these cells.
- The toggle switch allows you to visualize **2D or 3D t-sne**. Both, are fully interactive.

You can **run this plugin** either

- in a separate browser tab by clicking [**here**](https://imjoy.io/lite?plugin=https://github.com/fish-quant/fq-interactive-docs/blob/main/imjoy-plugins/RNAloc-TSNE.imjoy.html).
- directly in this documentation by press the `Run` button below.

<!-- ImJoyPlugin: { "type": "web-worker", "hide_code_block": true} -->
```js
class ImJoyPlugin {
    async setup() {}
    async run(ctx) {
        await api.createWindow({src: 'https://github.com/fish-quant/fq-interactive-docs/blob/main/imjoy-plugins/RNAloc-TSNE.imjoy.html'})
    }
}
api.export(new ImJoyPlugin())
```
