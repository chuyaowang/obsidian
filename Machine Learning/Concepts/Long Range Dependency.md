# Long Range Dependency

## Definition

Long-range dependency (LRD) is a phenomenon that may arise in the analysis of spatial or time series data. It relates to the rate of decay of statistical dependence of two points with increasing time interval or spatial distance between the points.

A time series with LRD is one in which the values at different times are not independent of each other. Instead, they are related to each other in a way that decays slowly over time. This means that the values at distant times can still be correlated, even if they are separated by a large number of time steps.

## Examples

An example of a time series with LRD is the price of a stock. The price of a stock today is not independent of the price of the stock yesterday. In fact, there is a strong correlation between the two prices. This correlation decays slowly over time, so the price of the stock today is still correlated to the price of the stock a year ago, even though they are separated by a large number of time steps.

Another example of a time series with LRD is the number of earthquakes in a region. The number of earthquakes in a region today is not independent of the number of earthquakes in the region yesterday. In fact, there is a strong correlation between the two numbers. This correlation decays slowly over time, so the number of earthquakes today is still correlated to the number of earthquakes a year ago, even though they are separated by a large number of time steps.

## Significance

LRD can be a challenge for time series analysis. Traditional time series models, such as autoregressive models, assume that the values at different times are independent of each other. This assumption is violated in the presence of LRD, so traditional time series models may not be able to accurately model time series with LRD.

There are a number of methods that can be used to model time series with LRD. One approach is to use fractionally integrated models. Fractionally integrated models allow for the possibility of long-range dependency in the data. Another approach is to use wavelet analysis. Wavelet analysis can be used to decompose the time series into different frequency bands. The long-range dependency can then be modeled in the low-frequency bands.

LRD is a complex phenomenon that can have a significant impact on the analysis of time series data. It is important to be aware of LRD when analyzing time series data, and to use appropriate methods to model time series with LRD.

## Transformer Model

The [transformer](Transformer) model allows learning of long range dependencies in data because it does not rely on sequential processing. In contrast to recurrent neural networks (RNNs), which process data one step at a time, transformers can attend to any part of the input sequence, regardless of its position. This allows transformers to learn relationships between distant elements in the input sequence.

Transformers achieve this by using self-attention, a mechanism that allows each element in the input sequence to attend to any other element in the sequence. Self-attention is implemented using a neural network that computes a score for each pair of elements in the sequence. The scores are then used to weight the contributions of each element to the representation of the other elements.