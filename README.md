# Assignment 2

Total marks: 

For all the questions given below, create `assignment_q<question-number>_subjective_answers.md` and write your observations.

## Questions
## Assignment Question

1. Generate the following two functions:

    Dataset 1:
    ```python
    num_samples = 40
    np.random.seed(45) 
        
    # Generate data
    x1 = np.random.uniform(-20, 20, num_samples)
    f_x = 100*x1 + 1
    eps = np.random.randn(num_samples)
    y = f_x + eps
    ```
    
    Dataset 2: 
    ```python
    np.random.seed(45)
    num_samples = 40
        
    # Generate data
    x1 = np.random.uniform(-1, 1, num_samples)
    f_x = 3*x1 + 4
    eps = np.random.randn(num_samples)
    y = f_x + eps
    ```

    - Implement full-batch and stochastic gradient descent. Find the average number of steps it takes to converge to an $\epsilon$-neighborhood of the minimizer for both datasets. Visualize the convergence process for 15 epochs. Choose $\epsilon = 0.001$ for convergence criteria. Which dataset and optimizer takes a larger number of epochs to converge, and why? Show the contour plots for different epochs (or show an animation/GIF) for visualisation of optimisation process. Also, make a plot for Loss v/s epochs. **[3 marks]**
   - Explore the article [here](https://machinelearningmastery.com/gradient-descent-with-momentum-from-scratch/#:~:text=Momentum%20is%20an%20extension%20to,spots%20of%20the%20search%20space.) on gradient descent with momentum. Implement gradient descent with momentum for the above two datasets. Visualize the convergence process for 15 steps. Compare the average number of steps taken with gradient descent (both variants -- full batch and stochastic) with momentum to that of vanilla gradient descent to converge to an $\epsilon$-neighborhood of the minimizer for both datasets. Choose $\epsilon = 0.001$. Write down your observations. Show the contour plots for different epochs for momentum implementation. Specifically, show all the vectors: gradient, current value of theta, momentum, etc. **[3 marks]**
     
2. Refer to the [instructor's notebook](https://nipunbatra.github.io/ml-teaching/notebooks/dummy-variables-multi-colinearity.html) on multi-colinearity. Use `np.linalg.solve` instead of `np.linalg.inv` for the same problem. Compare and contrast their usage, which one is better and why? Hint: matrix conditioning. Can you find out an example where one works and the other fails? **[2 Marks]**

3. Referring to the same [notebook](https://nipunbatra.github.io/ml-teaching/notebooks/dummy-variables-multi-colinearity.html), explain why Sklearn's linear regression implementation is robust against multicollinearity. Dive deep into Sklearn's code and explain in depth the methodology used in sklearn's implementation. **[1 Mark]**
   
4. Begin by exploring the [instructor's notebook](https://github.com/nipunbatra/ml-teaching/blob/master/notebooks/siren.ipynb) that introduces the application of Random Fourier Features (RFF) for image reconstruction. Demonstrate the following applications using the cropped image from the notebook:
    - Superresolution: perform superresolution on the image shown in notebook to enhance its resolution by factor 2. Show a qualitative comparison of original and reconstructed image. **[2 Marks]**
    - The above only helps us with a qualitative comparison. Let us now do a quantitative comparison. First, skim read this article: https://github.com/sgrvinod/a-PyTorch-Tutorial-to-Super-Resolution **[2 Marks]**
        - Start with a 400x400 image (ground truth high resolution).
        - Resize it to a 200x200 image (input image)
        - Use RFF + Linear regression to increase the resolution to 400x400 (predicted high resolution image)
        - Compute the following metrics:
            - RMSE on predicted v/s ground truth high resolution image
            - Peak SNR
    - Completing Image with Random Missing Data: Apply RFF to complete the image with 10%, 20%, and so on up to 90% of its data missing randomly. Randomly remove portions of the data, train the model on the remaining data, and predict on the entire image. Display the reconstructed images for each missing data percentage and show the metrics calculated above. What do you conclude?. **[2 Marks]**

5. Use the [instructor's notebook](https://github.com/nipunbatra/ml-teaching/blob/master/notebooks/movie-recommendation-knn-mf.ipynb) on matrix factorisation, and solve the following questions. 
    - Use the above image from Q4 and complete the rectangular missing patch for three cases, i.e. a rectangular block of 30X30 is assumed missing from the image. Choose rank `r` yourself. Vary the patch location as follows. **[3 Marks]**
        1. an area with mainly a single color.
        2. an area with 2-3 different colors.
        3. an area with at least 5 different colors.
    
        Perform Gradient Descent till convergence, plot the selected patches, original and reconstructed images, compute the metrics mentioned in Q4 and write your observations. Obtain the reconstruction using RFF + Linear regression and compare the two.

    - Vary patch size (NxN) for ```N = [20, 40, 60, 80, 100]``` and peform Gradient Descent till convergence. Demonstrate the variation in reconstruction quality by making appropriate plots and metrics. **[3 Marks]**
    
        Reconstruct the same patches using RFF. Compare the results and write your observations.
            
    - Write a function using this [reference](https://pytorch.org/docs/stable/generated/torch.linalg.lstsq.html) and use alternating least squares instead of gradient descent to repeat Part 1, 2 of Q5, using your written function. **[3 Marks]**
    
    - Consider a patch of size (100x100) with at least 5 colors. Vary the low-rank value as ```r = [5, 10, 20, 50, 100]``` . Use Gradient Descent and plot the reconstructed images to demonstrate difference in reconstruction quality. Write your observations. **[3 Marks]**

6. Create a data set as follows:

```py
np.random.seed(45) 

# Generate data
x = np.array([i*np.pi/180 for i in range(60,300,2)])
y = 3*x + 8 + np.random.normal(0,3,len(x))

# Reshape x to be a column vector
x = x.reshape(-1, 1)

```
Now, using Sklearn's `preprocessing.PolynomialFeatures` generate polynomial features for the data provided above, plot norm of theta (Weights) v/s degree when you fit linear regression using the polynomial of degree `d`. Vary the degree from 1 to 12. What do you observe? What can you conclude? 

7. For the scenario described in the previous question, consider using polynomial features of varying degrees (1, 3, 5, 7, 9). Suppose we vary the size of the dataset, denoted by N, and plot the magnitude of the norm of the weights (theta) against the degree of the polynomial regression model for each value of N. Plot the observed trends and draw conclusions based on the plotted data.

8. Compare the Random Forest algorithm with Decision Tree for recognizing Human Activity using UCI-HAR dataset. We'll test them with tree depths ranging from 2 to 8 and plot their accuracies. Again we'll test using two types of data: one with flattened out linear acceleration data and another with features extracted (from flattened out Linear Acceleration) using the TSFEL library.

9. Use Linear Regression for the above problem. Consider each class label as an integer value. Use featurized data to compare the accuracy obtained from Linear Regression with that of Random Forest and Decision Tree (trees of infinite depth). How did the linear regression perform? Explain why.

10. Obtain the weights(take absolute values as weights can also be negative) of the linear regression model. Also, obtain the feature importance from the Random Forest model. Plot the weights obtained as a Bar plot. This will help you visualize what features are being prioritized by the models. Note that sum of feature importances for a Random Forest model is 1. you will have to bring the linear regression weights to the same scale. To do so you can divide the weights by the sum of all the weights. Plot the importance of the features in the same plot. Figure out the top 10 important features obtained from both the models and display their names.

11. Consider the [Daily Temperatures dataset](https://raw.githubusercontent.com/jbrownlee/Datasets/master/daily-min-temperatures.csv) from Australia. This is a dataset for a forecasting task. That is, given temperatures up to date (or period) T, design a forecasting (autoregressive) model to predict the temperature on date T+1. You can refer to [link 1](https://www.turing.com/kb/guide-to-autoregressive-models), [link 2](https://otexts.com/fpp2/AR.html) for more information on autoregressive models. Use linear regression as your autoregressive model. Plot the fit of your predictions vs the true values and report the RMSE obtained. A demonstration of the plot is given below. ![imgsrc](./Autoregressive_Demo.png)

