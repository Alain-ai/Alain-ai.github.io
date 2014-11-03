---
layout: post
title: BaseEstimator in Scikit-Learn
categories: Machine_Learning
tags: Machine_Learning Python

---

<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


## How it looks like
Very simaple, just looks like as follows:
<pre>
class BaseEstimator(object):

    @classmethod
    def _get_param_names(cls):

    def get_params(self, deep=True):

    def set_params(self, **params):

    def __repr__(self):
</pre>
The existing four methods are mainly responsible for recognizing the names of paremeters and printing. However, just making use of these four methods, we are able to simplify our work a lot.

## How can we use it
In order to use the class, the first thing comes to our minds is inheritance. After we make our individual estimators which inherits from the BaseEstimator, we are allowed to pass our own estimators to whatever methods provided by scikit-learn only if they take BaseEstimator as a parameter.

A quick example is sklearn.grid_search.GridSearchCV. Its signature is as
<pre>
sklearn.grid_search.GridSearchCV(estimator, param_grid, scoring=None, loss_func=None, score_func=None, fit_params=None, n_jobs=1, iid=True, refit=True, cv=None, verbose=0, pre_dispatch='2*n_jobs')
</pre>
As we see, we can pass our the estimators to the 1st parameter. Then we could take advantage of GridSearchCV to performe cross-validation with plenty of options rather than write program to do it. An additional requirement is that our estimators will need to implement fit(X, y) and predict(y).


## An Example
Here is a concrete examples. Say we are going to implement a series of classifiers and run experiments on these.

First we boil down the common features of these classifiers, and make up a common parent called Estimator. Then we also have to let Estimator inherit from BaseEstimator so as to obtain the aforementioned sugar.

Then for each classifier we want to make, take Estimator as base class and implement its own "fit" and "predict" methods.

Say we'd like to make up a Logistic Regression classifier in this way. The mini-batch gradient descent has been used to optimize the model with a selective stepsize in every iteration epoch. The code looks like this.

<pre>
class Estimator(sb.BaseEstimator):
    def common_method(**args):

class LogisticRegression(Estimator):
    def __init__(self, lamb=1., T=5000):
        self.lamb = lamb
        self.w = None
        self.T = T

    def predict(self, X_test):
        s = X_test.dot(self.w).ravel()
        s[np.where(s >= 0)[0]] = 1
        s[np.where(s < 0)[0]] = 0
        return s

    def fit(self, X_train, y_train):
        w = np.zeros(X_train.shape[1], dtype=np.float64)
        rand_idx = numpy.random.permutation(X_train.shape[0])
        avg_T, it = 250, 0

        ########################
        # plt.axis([0, self.T/avg_T + 1, 1000, 5000])
        # plt.ion()
        # plt.show()
        # p_i = 0
        ########################

        w = np.zeros(X_train.shape[1], dtype=np.float64)
        mean_pre, mean_cur = 0, 0
        obj = self.obj_func_lg(w, (X_train, y_train))
        objs = [obj]
        # objs = []
        rand_i = 0
        while it < self.T:
            eta = 1./(math.sqrt(it) + 1.)
            # eta = 1./(it + 1)
            # print 'iter ' + str(it)
            rand_i = rand_i % rand_idx.size
            mini_batch = rand_idx[rand_i:min(rand_i+10, len(rand_idx))]
            rand_i += 10
            x_rand = X_train[mini_batch, :].reshape((mini_batch.size, X_train.shape[1]))
            y_rand = y_train[mini_batch].reshape(mini_batch.size)
            g = self.gradient_lg(w, (x_rand, y_rand))
            w = w - eta * g.ravel()
            # obj = self.obj_func_lg(w, (X_train, y_train))
            # objs.append(obj)
            # if len(objs) == avg_T:
            #     mean_pre = mean_cur
            #     mean_cur = np.mean(objs)
            #
            #     ################################
            #     # plt.scatter(p_i, mean_cur)
            #     # p_i += 1
            #     # plt.draw()
            #     ################################
            #     objs = []
            #     if abs(mean_cur - mean_pre) < 1e-5:
            #         break
            it += 1
        self.w = w

    def obj_func_lg(self, w, *args):
        X, y = args[0], args[1]
        s = self.sigmoid(X, w)
        obj = self.lamb * .5 * (np.linalg.norm(w)**2)
        obj -= y.T.dot(np.log(s)) + (1. - y).T.dot(np.log(1. - s))
        return obj

    def gradient_lg(self, w, *args):
        X, y = args[0], args[1]
        s = self.sigmoid(X, w)
        g = X.T.dot((s - y)) + self.lamb * w
        return g.ravel()

    def sigmoid(X, w):
        s = 1. / (1. + np.exp(-1. * (X.dot(w))))
        return s.ravel()
</pre>

Then we can performe cross-validation very easily like:

<pre>
def lg_run(X, y, X_test, y_test):
    tuned_parameters = [{'lamb': [5.**i for i in xrange(-5, 5)]}]
    clf = sklearn.grid_search.GridSearchCV(LogisticRegression(fit_sel=2), tuned_parameters, cv=5, scoring='accuracy')
    clf.fit(X, y.ravel())
    print("Best parameters set found on development set:")
    print(clf.best_estimator_)
    clf_best = clf.best_estimator_
    y_pred = clf_best.predict(X_test)
    clf_best.stats_pred(y_pred, y_test)
</pre>
