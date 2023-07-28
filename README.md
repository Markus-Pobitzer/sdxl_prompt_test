# Stable Diffusion XL (SDXL) Prompt Test
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Markus-Pobitzer/sdxl_prompt_test/blob/main/prompt_test.ipynb)


![SDXL](https://github.com/Stability-AI/generative-models) uses two text encoders (OpenCLIP-ViT/G and CLIP-ViT/L) for their base model. This means we can use two prompts at the same time, one for each encoder.

Here we try to get a better understanding of how the text encoders can be used together and how the results will change when using both at the same time. We are using code from the ![diffusers](https://github.com/huggingface/diffusers) library. Introduction on how to use SDXL with diffusers ![link](https://huggingface.co/docs/diffusers/api/pipelines/stable_diffusion/stable_diffusion_xl).

# Two text encoders - two prompts
Here we test what it means using two text encoders at the same time. Prompt is the text input for the first text encoder, Prompt_2 is the input for the second text encoder (as specified in diffusers). Each column in the following images uses a different prompt combination, the rows are the image results of a fixed seed. In the first two columns we use the same prompt for both text encoders, just differently ordered. In the third column, we use prompt A for the first encoder and prompt B for the second one, for the fourth column it is vice versa.

![Apple and Banana](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/apple_banana.png)

<hr>

![HMS Victory and Oil Painting](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/victory_painting.png)

<hr>

![Apple and Claude Monet](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/apple_monet.png)


# Two positive - Two negative
We can also specify a negative prompt for each text encoder. To better understand the combination of the positive prompt and the negative prompt we show the following experiment. Text encoder one uses "Red" as the positive prompt and "Green" as the negative, text encoder two uses "Green" as the positive prompt and "Red" as the negative. The result can be seen in the following image. In each row, we have a different combination of prompts. P means that we used the same prompt for both encoders, P1 is the positive prompt for the first encoder, and N1 for the negative prompt of the first encoder. Each column shows the result of a different fixed seed.

![Negative prompt Red and Green](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/negative_red_green.png)

# Complete prompt list
Here we tried several combinations of prompts.

![Apple and Banana](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/apple_banana_complete.png)

<hr>

![HMS Victory and Oil Painting](https://raw.githubusercontent.com/Markus-Pobitzer/sdxl_prompt_test/main/images/victory_painting_complete.png)

# Personal impression
From these results, I am under the impression that the second text encoder in the diffusers library is more influential that the first one. Compare The first image (apple and bananas), in the second and third columns we see that Prompt_2 is more dominant since the mentioned fruit is more persistent. This is especially noticeable in the first image with "HMS Vicory", where the first row, second column shows a woman (inherited from oil painting) and no ship.

Also, the negative prompt experiment seems to follow this. The third and fourth rows seem to follow more P2 (prompt_2) that gets fed into the second text encoder.

Most likely this relationship is sensitive to the way of combining the text latent and these experiments may be irrelevant if the underlying code in the diffusers library changes.
