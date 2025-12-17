# vault-trends-freesurfer-cobre
Vault TReNDS FreeSurfer COBRE

Pre-processing details below

Input data
T1w sMRI scans

Data is pre-processed using Freesurfer v 5.3

Pre-processing pipeline​
Freesurfer recon-all pipeline​
Performs the cortical reconstruction process. ​
Volumetric measurements read from aseg*stats aparc*stats​



Motion Correction and Conform​
NU (Non-Uniform intensity normalization)​
Talairach transform computation​
Intensity Normalization 1​
Skull Strip​
EM Register (linear volumetric registration)​
CA Intensity Normalization​
CA Non-linear Volumetric Registration​
Remove Neck​
LTA with Skull​
CA Label (Volumetric Labeling, ie Aseg) and Statistics​
Intensity Normalization 2 (start here for control points)​
White matter segmentation​
Edit WM With ASeg​
Fill (start here for wm edits)​
Tessellation (begins per-hemisphere operations)​
Smooth1​
Inflate1​
QSphere​
Automatic Topology Fixer​
Final Surfs (start here for brain edits for pial surf)​
Smooth2​
Inflate2​
Spherical Mapping​
Spherical Registration​
Spherical Registration, Contralateral hemisphere​
Map average curvature to subject​
Cortical Parcellation - Desikan_Killiany and Christophe (Labeling)​
Cortical Parcellation Statistics​
Cortical Ribbon Mask​
Cortical Parcellation mapping to Aseg​
​
​
Output files
Volumetric measurements read from aseg*stats aparc*stats​


Algorithm
Ridge Regression (Singleshot) - FreeSurfer Volumes

Input data
Volumetric measurements read from aseg*stats aparc*stats​


Dependent variable-volumes, thickness measurements of various brain regions from freesurfer preprocessed data. 

Independent variables -various demographic/cognitive variables.

On Client’s machine:  Fits OLS() to data and sends beta values to the remote




On COINSTAC server:  Averages all local beta’s and sends to Client’s machine

Options in COINSTAC
Lambda
Regularization Effect: The λI\lambda IλI term penalizes large coefficients, shrinking them toward zero, but not exactly zero (unlike Lasso Regression).
Trade-off:
A large λ\lambdaλ increases the penalty, resulting in smaller coefficients (more shrinkage).
A small λ\lambdaλ approaches the OLS solution.
Bias-Variance Trade-off: Ridge Regression reduces variance at the cost of introducing bias, improving predictive performance in many cases.


Github link: https://github.com/trendscenter/coinstac-ssr-fsl


Output data
Coefficients
Beta values

R Squared
1 - SSE / SST

sum of squared errors (SSE)= ||(y - y_estimate)^2||^2 where ||.|| --> l2-norm
total sum of squares (SST) = ||y - y_mean||^2 where ||.|| --> l2-norm

Degrees of Freedom

T stats
t-statistic is the coefficient divided by its standard error.
beta/std.err(beta)

P values
two-tailed p-value (The p-value is the probability of seeing a result as extreme as the one you are getting (a t value as large as yours) in a collection of random data in which the variable had no effect.)
Given by len(y) - len(beta_vector)
ts_beta (float) : t-statistic of shape [n_features +  1]
        var_covar_beta_global = MSE[i] * sp.linalg.inv(varX_matrix_global[i])
        se_beta_global = np.sqrt(var_covar_beta_global.diagonal())
        ts_ beta = (avg_beta_vector[i] / se_beta_global).tolist()

[2 * stats.t.sf(np.abs(t), dof) for t in ts_beta]

