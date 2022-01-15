# Dense Neural Network using M4 Globular Cluster Data

1. Introduction

The goal of this Jupyter notebook was to create a dense neural network (DNN) that can distinguish between members and non members of a star cluster, and to test which parameters demonstrate the border between them best. Two sets of data are used for this notebook. The first is a dataset containing only members of the star cluster, and the second includes stars located around the cluster. The code is written such that it can be easily adjusted for only one dataset.

Before beginning, the following packages must be imported: Numpy, Pandas, Matplotlib.pyplot, Tensorflow, Sklearn, and mpl_toolkits (the last is optional, only used for one 3D plot that is not integral to the rest of the notebook). 

2. Methods

The first step is to load the data using the pd.read function. Once ensuring the data is loaded properly, the next step is to visualize the parameters that will be used. This step is technically optional, but highly recommended, as it helps prevent future confusion/mistakes. For this project it was important to visualize (1) the relationship between the two datasets, and the expected location of the cluster with (2) right ascension and declination, and (3) proper motion in right ascension and proper motion in declination.

2.1 Dense Neural Network Setup

Once these preliminary steps are complete, work on the DNN can begin. The first step is to create input variables, which will be in the form of a 2D numpy array. This is done by pulling the necessary values for each data point from the dataset and removing any points that have missing values, fitting, transforming, and standardizing them [Steps 1(a, b, c)]. After creating this input variable, a separation between testing and training sets can be made. To do so, establish the desired input variable length and the percentage of points to be allocated to the testing set. Then, using np.random.choice, randomly separate the points into testing and training groups. The testing set is fed to the DNN, and the training set is used in the validation process. It is also important to create output vectors at this stage. This is done in a similar way as the input variable, both found in [Steps 2(a, b, c].

Now that both inputs and outputs are ready, the model can be built. Start by establishing the keras.Sequential model from tensorflow as a variable, as seen in [Steps 3(a, b, c)]. Then, calling that variable, add the desired number of layers. This notebook uses the following layers to start: layers.Flatten, two dense layers with rectified linear activation, a final dense layer with softmax activation, and then a compiling layer. This model can then be fed desired fit parameters and executed as seen in [Steps 4(a, b, c)]. In this step, the input training set is fed to the model, being fit to the form of the output training set, and ran against the validation data. In this notebook, ‘verbose’ is set to 1 to display the progress bars and numeric information, though it can be set to 0 for a cleaner output. Depending on the number of epochs chosen, computational time may be lengthy [10 epochs take ~2 minutes]. After the epochs have finished running, the training and testing losses are plotted to demonstrate how they are performing.

2.2 Dense Neural Network Analysis

The next step is to create a variable with predicted output values, as seen in [Steps 5(a, b, c)]. It is then optional to plot a histogram of the model's confidence in each point's predicted membership status, to verify the final plot. After this histogram, a final scatter plot can be made. As shown in [Step 6(a, b, c)], the predicted values can be plotted similar to the preliminary scatter plots, but setting the plot color to the predicted output. This shows the confidence scale and which stars are predicted to be cluster members. This visual is used to analyze whether the model and selected parameters successfully identified the cluster. For sets of three parameters, there is an optional [Step 7b] to create a 3D prediction plot.

After the aforementioned steps are complete, the resulting classification is analyzed. Effectiveness of boundaries, amount of certainty, and confidence at the center of the cluster (where it should be highest) are assessed . Repeat the outlined steps with as many more sets of parameters as is needed. This notebook conducted the outlined steps a total of three times, but less/more may be required for other sets of data. 

3. Conclusion

This notebook achieved the goal of creating a DNN to classify members and non members of a star cluster. After producing three different prediction plots, the model proved to be effective in varying degrees, which depend on the efficacy of variables, not the DNN itself. This notebook can be applied to other sets of data.

