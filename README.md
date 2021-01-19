# GNBM0


For the naive gaussian Bayesian classifier, the data, D, is a vector of samples. We assume that
the samples are independent and that they follow a Gaussian distribution.
The parameters of the gaussian for each class will be computed during the training of the
Python classifier. For each gaussian, the mean and standard deviation is computed.
Also, if some information about the class is available, and some classes are more or less likely,
then this knowledge is encoded in the prior probability P(C).
The Python code also returns a value epsilon, which is needed for numerical accuracy


According to the function of arm_gaussian_naive_bayes_predict_f32, it puts each probability to the buffer and returns the index of the highest probability value.
But in the example code of arm_bayes_example_f32.c, it calculates the max value in the result buffer even though arm_gaussian_naive_bayes_predict_f32 returns it.
  arm_gaussian_naive_bayes_predict_f32(&S, in, result);

  arm_max_f32(result, NB_OF_CLASSES, &maxProba, &index);
I think this is a bit redundant. So this is clearer.
  index = arm_gaussian_naive_bayes_predict_f32(&S, in, result);

  maxProba = result[index];

In the example I wanted to extract the probability in addition to the index.
But it does not make sense to re-compute the max for this. Hence the above is used.
We can also suspend background operations.
