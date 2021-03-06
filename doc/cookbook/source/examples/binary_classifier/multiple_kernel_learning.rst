========================
Multiple Kernel Learning
========================

Multiple kernel learning (MKL) is based on convex combinations of arbitrary kernels over potentially different domains.

.. math::

    {\bf k}(x_i,x_j)=\sum_{i=1}^{K} \beta_k {\bf k}_i(x_i, x_j)

where :math:`\beta_k > 0`, :math:`\sum_{k=1}^{K} \beta_k = 1`, :math:`K` is the number of sub-kernels, :math:`\bf{k}` is a combined kernel, :math:`{\bf k}_i` is an individual kernel and :math:`{x_i}_i` are the training data.

Classification is done by using Support Vector Machines (SVM). See :doc:`linear_svm` for more details. Optimal :math:`\alpha` and :math:`b` for SVM and :math:`\beta` are determined via training.

See :cite:`sonnenburg2006large` for more details.

-------
Example
-------

Imagine we have files with training and test data. We create CDenseFeatures (here 64 bit floats aka RealFeatures) and :sgclass:`CBinaryLabels` as

.. sgexample:: mkl.sg:create_features

Then we create indvidual kernels like :sgclass:`CPolyKernel` and :sgclass:`CGaussianKernel` which will be later combined in one :sgclass:`CCombinedKernel`.

.. sgexample:: mkl.sg:create_kernel

We create an instance of :sgclass:`CCombinedKernel` and append the :sgclass:`CKernel` objects.

.. sgexample:: mkl.sg:create_combined_train

We create an object of :sgclass:`CMKLClassification`, provide the combined kernel and labels before training it.

.. sgexample:: mkl.sg:train_mkl

After training, we can extract :math:`\beta`, SVM coefficients :math:`\alpha` and :math:`b`.

.. sgexample:: mkl.sg:extract_weights

We update the :sgclass:`CCombinedKernel` object for testing data.

.. sgexample:: mkl.sg:create_combined_test

We set the updated kernel and predict :sgclass:`CBinaryLabels` for test data.

.. sgexample:: mkl.sg:mkl_apply

Finally, we can evaluate test performance via e.g. :sgclass:`CAccuracyMeasure`.

.. sgexample:: mkl.sg:evaluate_accuracy

----------
References
----------
:wiki:`Multiple_kernel_learning`

.. bibliography:: ../../references.bib
    :filter: docname in docnames
