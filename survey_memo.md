## Feasability Survey
1. Understanding what the model has learned by **visualization** approaches

    [Github codes](https://github.com/utkuozbulak/pytorch-cnn-visualizations) with several common CNN visualization techniques implemented. Below are the ones that I think may work in semantic segmentation tasks.
    1. Visualizing conv layer filters by **gradient ascending**
        1. [Paper: Understanding Neural Networks Through Deep Visualization](http://yosinski.com/media/papers/Yosinski__2015__ICML_DL__Understanding_Neural_Networks_Through_Deep_Visualization__.pdf) and [blog](http://yosinski.com/deepvis) by author of the paper. (not the original inventor of this method)
        2. [Another blog](https://towardsdatascience.com/how-to-visualize-convolutional-features-in-40-lines-of-code-70b7d87b0030) with some simple PyTorch codes to implement it fast.
    2. Visualizing activations of hidden layers
        
        Examples are show in Figure.4 from this [paper: Learning Deconvolution Network for Semantic Segmentation](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Noh_Learning_Deconvolution_Network_ICCV_2015_paper.pdf).
        
    I found those visualizations are often analyzed **case by case** (model by model), since the results are strongly affected by the data the model trained on. I did not find a general process on explinaing these visualized results.
       
2. Verifying the **robustness** of a model (evaluating whether the model is well-trained)
    1. Measuring filter importance 
        1. [Filter importance by L1 norm](https://openreview.net/pdf?id=rJqFGTslg) => naive but efficient
        2. [Filter importance by Tyler expansion](https://arxiv.org/pdf/1611.06440.pdf) => costly but beats navie ones
        3. [Classification accuracy reduciton (CAR)](https://arxiv.org/pdf/1705.07356.pdf) => computationally heavy
    2. [Model resistence to corruptions and perturbations](https://arxiv.org/pdf/1903.12261.pdf) => common corruptions and perturbation like Gaussian noise and Gaussian blur
    3. Adversarial attacks and defenses
    
        This is an interesting one since we usually won't expect (perhaps?) such attakcs from our client.
        
        [A quick view on adversarial attacks](http://karpathy.github.io/2015/03/30/breaking-convnets/).
        
        [ClerverHans: An adversarial benchmark](https://github.com/tensorflow/cleverhans)

    4. Something I came up with...
    
        Maybe we could try to plot the distirbution of the filter activations on a whole dataset, and try to find out redundant filters. (The distribution could be the sum of standardized mean of the outputs of that layer)
