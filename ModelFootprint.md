## Model Footprint

As part of our sustainability efforts, we documented the energy consumption involved in the creation and deployment of the model to better understand its environmental footprint. Using [CodeCarbon](https://mlco2.github.io/codecarbon/), an open-source tool that estimates the energy consumption of machine learning workloads, we tracked energy usage during preprocessing and feature extraction on 5,922 samples. This stage consumed a total of **0.0675 kWh**—primarily from **CPU usage (0.0462 kWh)**, followed by **RAM (0.0109 kWh)** and **GPU (0.0105 kWh)**.

After training a **90-million-parameter** model over **4.22 minutes**, the total recorded energy consumption rose to **0.0875 kWh**. The training phase alone used approximately **0.0200 kWh**, broken down into **0.0109 kWh** from CPU, **0.0065 kWh** from GPU, and **0.0026 kWh** from RAM.

We also measured the energy usage during model testing on **1,185 samples**. This phase consumed only **0.00014 kWh** of electricity, with **0.000061 kWh** attributed to CPU, **0.000065 kWh** to GPU, and **0.000014 kWh** to RAM.

---

### Per-Case Energy Cost

To estimate the energy cost per user interaction with the deployed model:

- **Preprocessing per case**: 0.0000114 kWh  
- **Predicting per case**: 0.00000012 kWh  
- **Total per case**: **0.00001152 kWh**

| Number of Users | Total Energy Cost (kWh) |
|------------------|-------------------------|
| 1                | 0.00001152              |
| 1,000            | 0.01152                 |
| 100,000          | 1.152                   |

If **100,000 users** interact with MeowDecoder, the energy cost (1.152 kWh) is roughly the same as:

- Using a **laptop (50W)** for about **23 hours**, or  
- Running a **100W appliance** for **half a day**

With the global average carbon intensity of the electricity grid at **0.475 kg CO₂ per kWh**, the associated emissions would be **0.55 kg CO₂**, which is approximately equivalent to the CO₂ absorbed by a **tree in one week**.

---

### Energy Efficiency through Model Design

By adopting a **simple CNN structure** as the base of our model, we significantly reduced energy consumption compared to larger, more complex architectures like Transformers or deep residual networks. A smaller CNN requires:

- Less RAM  
- Lower GPU and CPU runtime  
- Faster inference with minimal power

This is especially beneficial when deployed at scale. The efficient pipeline—from lightweight preprocessing to a compact CNN model—supports a **more sustainable AI lifecycle**, aligning performance with environmental responsibility.

