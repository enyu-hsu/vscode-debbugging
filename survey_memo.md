## Feasability Survey
1. Understanding what the model has learned by **visualization** approaches

    [Github codes](https://github.com/utkuozbulak/pytorch-cnn-visualizations) with several common CNN visualization techniques implemented. Below are the ones that I think may work in semantic segmentation tasks.
    1. Visualizing conv layer filters by **gradient ascending**
        1. [Paper: Understanding Neural Networks Through Deep Visualization](http://yosinski.com/media/papers/Yosinski__2015__ICML_DL__Understanding_Neural_Networks_Through_Deep_Visualization__.pdf) and [blog](http://yosinski.com/deepvis) by author of the paper. (not the original inventor of this method)
        2. [Another blog](https://towardsdatascience.com/how-to-visualize-convolutional-features-in-40-lines-of-code-70b7d87b0030) with some simple PyTorch codes to implement it fast.
    2. Visualizing activations of hidden layers
        
        Examples are show in Figure.4 from this [paper: Learning Deconvolution Network for Semantic Segmentation](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Noh_Learning_Deconvolution_Network_ICCV_2015_paper.pdf).
        
    I found those visualizations are often analyzed **case by case** (model by model), since the results are strongly affected by the data the model trained on. I did not find a general process on explinaing these visualized results.
       
2. Verifying the **robustness** of a model
    1. Adversarial attack and defense
    
        This is an interesting one since we usually won't expect (perhaps?) such attakcs from our client.
        
        [A quick view on adversarial attacks](http://karpathy.github.io/2015/03/30/breaking-convnets/).
        
        [ClerverHans: An adversarial benchmark](https://github.com/tensorflow/cleverhans)
