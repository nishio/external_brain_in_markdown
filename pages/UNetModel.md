---
title: "UNetModel"
---

`class UNetModel(nn.Module)`
- The full UNet model with attention and timestep embedding.
- :param in_channels: channels in the input Tensor.
- :param model_channels: base channel count for the model.
- :param out_channels: channels in the output Tensor.

- :param num_res_blocks: number of residual blocks per downsample.


            - :param attention_resolutions: a collection of downsample rates at which
                            - attention will take place. May be a set, list, or tuple.
                            - For example, if this contains 4, then at 4x downsampling, attention
                            - will be used.
            - :param dropout: the dropout probability.
            - :param channel_mult: channel multiplier for each level of the UNet.
            - :param conv_resample: if True, use learned convolutions for upsampling and
                            - downsampling.
            - :param dims: determines if the signal is 1D, 2D, or 3D.
            - :param num_classes: if specified (as an int), then this model will be
                            - class-conditional with `num_classes` classes.
            - :param use_checkpoint: use gradient checkpointing to reduce memory usage.
            - :param num_heads: the number of attention heads in each attention layer.
            - :param num_heads_channels: if specified, ignore num_heads and instead use
                                                                                                                        - a fixed channel width per attention head.
            - :param num_heads_upsample: works with num_heads to set a different number
                                                                                                                        - of heads for upsampling. Deprecated.
            - :param use_scale_shift_norm: use a FiLM-like conditioning mechanism.
            - :param resblock_updown: use residual blocks for up/downsampling.
            - :param use_new_attention_order: use a different attention pattern for potentially
                                                                                                                                            - increased efficiency.


Residual neural network(2016)
- [Residual neural network - Wikipedia](https://en.wikipedia.org/wiki/Residual_neural_network)

