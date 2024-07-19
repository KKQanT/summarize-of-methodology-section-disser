# summarize-of-methodology-section-disser

## Methodology & Experiment

### Selected Approach

#### cost-sensitive
You should know this

#### Fuzzy SVM for class imbalance learning
You should know this

#### Adaptive Feature-Space Conformal Transformation for Imbalanced-Data Learning
- **Kernel Function:**
  - Given any kernel function K(x_i, x_j) = φ(x_i) ⋅ φ(x_j), where φ(x) is an unknown non-linear mapping function for a kernel SVM.
  - The conformal transformation of Kernel K is defined as:
    Tilde_K(x_i, x_j) = D(x_i)D(x_j) K(x_i, x_j)
    where D(x) is a positive function.

- **Selection of D(x):**
  - By selecting appropriate D(x), we can increase the area around the boundary in the higher dimension surface for the K kernel SVM.
  - Suggested by [CT] that D(x) can be chosen as:
    D(x) = Σ_{x_k ∈ SV} exp(-1/τ_k^2 ||x - x_k||^2)
    where:
    τ_k^2 = 1/N_k Σ_{x_s ∈ SV_k} ||x_s - x_k||^2
    SV_k denotes a set of N_k nearest support vectors to the support vector x_k.

- **Alternative τ_k Definition:**
  - Suggested by [ACT] that τ_k should be defined as:
    τ_k^2 = 1/|P| Σ_{x_s ∈ P} ||φ(x_s) - φ(x_k)||^2
    where:
    P = { ||φ(x_s) - φ(x_k)||^2 < M, y_s ≠ y_k }
    M denotes the average distance in the higher non-linear space of the closest and the farthest support vectors of the support vector x_k.

- **Key Difference:**
  - One of the huge differences between the equations is that the formulation of τ_k in [ACT] considers the distance in the implicit feature space instead of Euclidean distance in the original space, which can be more meaningful in the context of kernel SVM.

- **Addressing Imbalanced Data:**
  - Suggested in the original paper that τ_k^2 should be scaled with different scaling factors η for each class as follows:
    Tilde_τ_k^2 = 
    { η^+ τ_k^2 if y_i = 1
    and
      η^- τ_k^2 if y_i = -1 }
  - By setting η^+ larger than η^-, it will relatively increase the region boundary near minority class support vectors to the majority ones.
  - Suggested that η^+ and η^- should be proportional to the imbalance of support vectors.

- **Implementation in Our Work:**
  - η^+ is set to 1 while η^- is set to |SV^+| / |SV^-| ≤ 1, meaning that we shrink the τ_k^2 corresponding to the majority class while maintaining the τ_k^2 for the minority class to be the same.

- **Method Exploration:**
  - This method aims to enhance the kernel function to have a larger region around the important area, which is the region boundary while considering the imbalance of data.
  - Potential to improve predictive performance in our data compared to vanilla SVM.
  - The method only modifies the kernel part, allowing it to be applied along with other methods including cost-sensitive SVM and FSVM CIL, which will be discussed in the following sections.
[ACT] = Wu, Gang & Chang, Edward. (2003). Adaptive Feature-Space Confor-
mal Transformation for Imbalanced-Data Learning. Proceedings, Twen-
tieth International Conference on Machine Learning. 2. 816-823.

[CT] = Wu, Si and Shun-ichi Amari. “Conformal Transformation of Kernel
Functions: A Data-Dependent Way to Improve Support Vector Machine
Classifiers.” Neural Processing Letters 15 (2002): 59-67.

### Improvement of previous works

#### Redefine the distance from the own class center of FSVM-CIL
in progress

#### Kernel modification of FSVM-CIL
in progress

### Experiment setup
You should know this part as it related to data, cross validate and etc
