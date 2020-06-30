## Chapter 6. Progressing with GANs

"As our mountaineer gets closer to a valley, we can start increasing the complexity by zooming in on the terrain. Then we no longer see just the coarse/pixelated texture, but instead get to see the finer details. This approach has the advantage that as our mountaineer goes down the slope, they can easily make little optimizations to make the hiking easier. For example, they can take a path through a dried-up creek to make the descent into the valley even faster. That is progressive growing: increasing the resolution of the terrain as we go."

"we progressively smooth in and slowly introduce more complexity as the mountaineer gets closer to the objective"

![progressive_size](https://i.gyazo.com/393bbc384daee809adf819de44456ff3.png)

" rather than immediately jumping to this resolution, we smoothly fade in this new layer with higher resolution by a parameter alpha (α), which is between 0 and 1. Alpha affects how much we use either the old—but upscaled—layer or the natively larger one. On the side of the D, we simply shrink by 0.5x to allow for smoothly injecting the trained layer for discrimination."

