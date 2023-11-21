---
title: Deep Learning深度学习-学习笔记
date: 2023-11-18 02:18:00
tags:
  - DL
categories: 软件
cover: https://fp1.fghrsh.net/2023/11/21/49843f304bf140153456b64733542a06.jpg!q80.jpeg
katex: true
mathjax: true
---

This notes' content are all based on https://www.coursera.org/specializations/deep-learning<!-- more -->

>   Latex may have some issues when displaying.

## 1. Neural Networks and Deep Learning

### 1.1 Introduction to Deep Learning

#### 1.1.1 Supervised Learning with Deep Learning

-   Structured Data: Charts.
-   Unstructured Data: Audio, Image, Text.

#### 1.1.2 Scale drives deep learning progress

-   The larger the amount of data, the better the performance of the larger neural network compare to smaller one or supervised learning.
-   Sigmoid change to ReLU will make gradient descent much more faster. Since the gradient will not go to 0 really fast.

### 1.2 Basics of Neural Network Programming

#### 1.2.1 Binary Classification

-   Input: {% katex %}X \in R^{nx} {% endkatex %}
-   Output: 0, 1

#### 1.2.2 Logistic Regression

-   Given {% katex %}x{% endkatex %}, want {% katex %}\hat{y} = P(y=1|x){% endkatex %}
-   Input: {% katex %}x \in R^{n_x} {% endkatex %}
-   Parameters: {% katex %}w \in R^{n_x}, b \in R {% endkatex %}
-   Output {% katex %}\hat{y} = \sigma(w^Tx + b){% endkatex %}
    -   {% katex %}\sigma(z)=\dfrac{1}{1+e^{-z}}{% endkatex %}
    -   If {% katex %}z {% endkatex %} large, {% katex %}\sigma(z)\approx\dfrac{1}{1+0}\approx1{% endkatex %}
    -   If {% katex %}z {% endkatex %} large negative number, {% katex %}\sigma(z)\approx\dfrac{1}{1+Bignum}\approx0{% endkatex %}

-   Loss (error) function: 
    -   {% katex %}\hat{y} = \sigma(w^Tx + b){% endkatex %}, where {% katex %}\sigma(z)=\dfrac{1}{1+e^{-z}}{% endkatex %}
        -   {% katex %}z^{(i)}=w^Tx^{(i)}+b{% endkatex %}

    -   Want {% katex %}y^{(i)} \approx \hat{y}^{(i)} {% endkatex %}
    -   {% katex %}L(y, \hat{y}) = -[y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})]{% endkatex %}
        -   If {% katex %}y=1: L(\hat{y}, y)=-\log{\hat{y}} {% endkatex %} <- want {% katex %}\log{\hat{y}}{% endkatex %} as large as possible, want {% katex %}\hat{y}{% endkatex %} large
        -   If {% katex %}y=0: L(\hat{y}, y)=-\log{(1-\hat{y})} {% endkatex %} <- want {% katex %}\log{(1-\hat{y})}{% endkatex %} as large as possible, want {% katex %}\hat{y}{% endkatex %} small

-   Cost function
    -   {% katex %}J(w, b)=\dfrac{1}{m}\sum\limits_{i=1}^{m}L(\hat{y}^{(i)},y^{(i)})=-\dfrac{1}{m}\sum\limits_{i=1}^{m}L[y^{(i)} \log(\hat{y}^{(i)}) + (1 - y^{(i)}) \log(1 - \hat{y}^{(i)})]{% endkatex %}

#### 1.2.3 Gradient Descent

-   Repeat {% katex %}w:=w-\alpha\dfrac{dJ(w)}{dw}{% endkatex %}; {% katex %}b:=b-\alpha\dfrac{\partial J(w,b)}{\partial b}{% endkatex %}
    -   {% katex %}\alpha{% endkatex %}: Learning rate
    -   Right side of minimum, {% katex %}\dfrac{dJ(w)}{dw} > 0{% endkatex %}; Left side of minimum, {% katex %}\dfrac{dJ(w)}{dw} < 0{% endkatex %}
-   Logistic Regression Gradient Descent
    -   {% katex %}x_1,x_2,w_1,w_2,b{% endkatex %}
        -   {% katex %}z=w_1x_1+w_2x_2+b{% endkatex %} -->{% katex %}a=\sigma(z){% endkatex %} -->{% katex %}L=(a,y){% endkatex %}
        -   {% katex %}da=\dfrac{dL(a,y)}{da}=-\dfrac{y}{a}+\dfrac{1-y}{1-a}{% endkatex %}
            -   {% katex %}\dfrac{dL(y,a)}{da} = \dfrac{d}{da}(-y\log(a) - (1-y)\log(1-a)){% endkatex %}
            -   {% katex %}\dfrac{d}{da} (-y\log(a)) = -\dfrac{y}{a}{% endkatex %}
            -   {% katex %}\dfrac{d}{da} (-(1-y)\log(1-a)) = -\dfrac{1-y}{1-a} \times (-1) = \dfrac{1-y}{1-a} {% endkatex %}
            -   {% katex %}=-\dfrac{y}{a} + \dfrac{1-y}{1-a} = -\dfrac{y}{a} - \dfrac{y-1}{1-a}{% endkatex %}
        -   {% katex %}dz=\dfrac{dL}{dz}=\dfrac{dL(a,y)}{dz}=a-y{% endkatex %}
            -   {% katex %}=\dfrac{dL}{da}\cdot\dfrac{da}{dz}{% endkatex %}  ({% katex %}\dfrac{da}{dz}=a(1-a){% endkatex %})
        -   {% katex %}\dfrac{dL}{dw_1}="dw_1"=x_1\cdot dz{% endkatex %}
        -   {% katex %}\dfrac{dL}{dw_2}="dw_2"=x_2\cdot dz{% endkatex %}
        -   {% katex %}db=dz{% endkatex %}
-   Gradient Descent on {% katex %}m{% endkatex %} examples
    -   {% katex %}J(w, b)=\dfrac{1}{m}\sum\limits_{i=1}^{m}L(a^{(i)},y^{(i)}){% endkatex %}
    -   {% katex %}\dfrac{\partial}{\partial w_1}J(w,b)=\dfrac{1}{m}\sum\limits_{i=1}^{m}\dfrac{\partial}{\partial w_1}L(a^{(i)},y^{(i)}){% endkatex %}
    -   {% katex %}J=0;dw_1=0;dw_2=0;db=0{% endkatex %}
        -   for {% katex %}i=1{% endkatex %} to {% katex %}m{% endkatex %}
            -   {% katex %}z^{(i)}=w^Tx^{(i)}+b{% endkatex %}
            -   {% katex %}a^{(i)}=\sigma (z^{(i)}){% endkatex %}
            -   {% katex %}J+=-[y^{(i)}loga^{(i)}+(1-y^{(i)})log(1-a^{(i)})]{% endkatex %}
            -   {% katex %}dz^{(i)}=a^{(i)}-y^{(i)}{% endkatex %}
            -   {% katex %}dw_1+=x_1^{(i)}dz^{(i)}{% endkatex %} (for n = 2)
            -   {% katex %}dw_2+=x_2^{(i)}dz^{(i)}{% endkatex %} (for n = 2)
            -   {% katex %}db+=dz^{(i)}{% endkatex %}
        -   {% katex %}J/=m;dw_1/=m;dw_2/=m;db/=m{% endkatex %}
        -   {% katex %}dw_1=\dfrac{\partial J}{\partial w_1}; dw_2=\dfrac{\partial J}{\partial w_2}{% endkatex %}
            -   {% katex %}w_1:=w_1-\alpha dw_1{% endkatex %}
            -   {% katex %}w_2:=w_2-\alpha dw_2{% endkatex %}
            -   {% katex %}b:=b-\alpha db{% endkatex %}

#### 1.2.4 Computational Graph

-   {% katex %}J(a,b,c)=3(a+bc){% endkatex %}
    -   {% katex %}u=bc{% endkatex %}
    -   {% katex %}v=a+u{% endkatex %}
    -   {% katex %}J=3v{% endkatex %}
    -   Left to right computation

-   Derivatives with a Computation Graph
    -   {% katex %}\dfrac{dJ}{dv}=3{% endkatex %}
        -   {% katex %}\dfrac{dJ}{da}=3{% endkatex %}
        -   {% katex %}\dfrac{dv}{da}=1{% endkatex %}
        -   Chain Rule: {% katex %}\dfrac{dJ}{da}=\dfrac{dJ}{dv}\cdot\dfrac{dv}{da}{% endkatex %}
        -   {% katex %}\dfrac{dJ}{du}=3; \dfrac{du}{db}=2; \dfrac{dJ}{db}=6{% endkatex %}
        -   {% katex %}\dfrac{du}{dc}=3; \dfrac{dJ}{dc}=9{% endkatex %}

#### 1.2.5 Vectorization

-   avoid explicit for-loops.
-   {% katex %}J=0;dw=np.zeros((n_x,1));db=0{% endkatex %}
    -   for {% katex %}i=1{% endkatex %} to {% katex %}m{% endkatex %}
        -   {% katex %}z^{(i)}=w^Tx^{(i)}+b{% endkatex %}
        -   {% katex %}a^{(i)}=\sigma (z^{(i)}){% endkatex %}
        -   {% katex %}J+=-[y^{(i)}loga^{(i)}+(1-y^{(i)})log(1-a^{(i)})]{% endkatex %}
        -   {% katex %}dz^{(i)}=a^{(i)}-y^{(i)}{% endkatex %}
        -   {% katex %}dw+=x^{(i)}dz^{(i)}{% endkatex %}
        -   {% katex %}db+=dz^{(i)}{% endkatex %}
    -   {% katex %}J/=m;dw/=m;db/=m{% endkatex %}
-   {% katex %}Z=np.dot(w.T,x)+b{% endkatex %} ; b(1,1)-->Broodcasting
-   Vectorization Logistic Regression
    -   {% katex %}dz^{(1)}=a^{(1)}-y^{(1)}; dz^{(2)}=a^{(2)}-y^{(2)}...{% endkatex %}
    -   {% katex %}dz=[dz^{(1)}, dz^{(2)},...,dz^{(m)}]{% endkatex %}  {% katex %}1\times m{% endkatex %}
    -   {% katex %}A=[a^{(1)}, a^{(2)}, ..., a^{(m)}]{% endkatex %}    {% katex %}Y=[y^{(1)}, y^{(2)}, ..., y^{(m)}]{% endkatex %}
    -   {% katex %}dz=A-Y=[a^{(1)}-y^{(1)}, a^{(2)}-y^{(2)}, ...]{% endkatex %}
    -   Get rid of {% katex %}db{% endkatex %} and {% katex %}dw{% endkatex %} in for loop
        -   {% katex %}db=\dfrac{1}{m}\sum\limits_{i=1}^{m}dz^{(i)}=\dfrac{1}{m} np.sum(dz){% endkatex %}
        -   {% katex %}dw=\dfrac{1}{m}\cdot X\cdot dz^T=\dfrac{1}{m}[x^{(1)}...][dz^{(1)}...]=\dfrac{1}{m}\cdot[x^{(1)}dz^{(1)}+...+x^{(m)}dz^{(m)}]{% endkatex %}   {% katex %}n\times 1{% endkatex %}
    -   New Form of Logistic Regression
        -   {% katex %}Z=w^tX+b=np.dot(w.T, X)+b{% endkatex %}
        -   {% katex %}A=\sigma (Z){% endkatex %}
        -   {% katex %}dz=A-Y{% endkatex %}
        -   {% katex %}dw=\dfrac{1}{m}\cdot X \cdot dZ^T{% endkatex %}
        -   {% katex %}db=\dfrac{1}{m}np.sum(dz){% endkatex %}
        -   {% katex %}w:=w-\alpha dw{% endkatex %}
        -   {% katex %}b:=b-\alpha db{% endkatex %}

-   Broadcasting(same as bsxfun in Matlab/Octave)
    -   {% katex %}(m,n){% endkatex %}+-*/{% katex %}(1,n){% endkatex %}->{% katex %}(m,n){% endkatex %}  1->m will be all the same number.
    -   {% katex %}(m,n){% endkatex %}+-*/{% katex %}(m,1){% endkatex %}->{% katex %}(m,n){% endkatex %}  1->n will be all the same number
    -   Don't use    {% katex %}a = np.random.randn(5){% endkatex %}    {% katex %}a.shape = (5,){% endkatex %}  "rank 1 array"
    -   Use   {% katex %}a = np.random.randn(5,1){% endkatex %}    or    {% katex %}a = np.random.randn(1,5){% endkatex %}
    -   Check by   {% katex %}assert(a.shape == (5,1)){% endkatex %}
    -   Fix rank 1 array by    {% katex %}a = a.reshape((5,1)){% endkatex %}
-   Logistic Regression Cost Function
    -   Lost
        -   {% katex %}p(y|x)=\hat{y}^y(1-\hat{y})^{(1-y)}{% endkatex %}
        -   If {% katex %}y=1{% endkatex %}: {% katex %}p(y|x)=\hat{y}{% endkatex %}
        -   If {% katex %}y=0{% endkatex %}: {% katex %}p(y|x)=(1-\hat{y}){% endkatex %}
        -   {% katex %}\log p(y|x)=\log \hat{y}^y(1-\hat{y})^{(1-y)}=y\log \hat{y}+(1-y)\log(1-\hat{y})=-L(\hat{y},y){% endkatex %}
    -   Cost
        -   {% katex %}\log p(labels\space in\space training\space set)=\log \Pi_{i=1}^{m}p(y^{(i)},x^{(i)}){% endkatex %}
        -   {% katex %}\log p(labels\space in\space training\space set)=\sum\limits_{i=1}^m\log p(y^{(i)},x^{(i)})=-\sum\limits_{i=1}^mL(\hat{y}^{(i)},y^{(i)}){% endkatex %}
        -   Use maximum likelihood estimation(MLE)
        -   Cost(minmize): {% katex %}J(w,b)=\dfrac{1}{m}\sum\limits_{i=1}^mL(\hat{y}^{(i)},y^{(i)}){% endkatex %}

### 1.3 Shallow Neural Networks

#### 1.3.1 Neural Network Representation

-   ![deep-learning-notes_1-3-1](https://s2.loli.net/2023/11/20/EHtqxOI6c5NQuG8.jpg)

-   Input layer, hidden layer, output layer
    -   {% katex %}a^{[0]}=x{% endkatex %} -> {% katex %}a^{[1]}=[[a^{[1]}_1,a^{[1]}_2,a^{[1]}_3,a^{[1]}_4]]{% endkatex %} -> {% katex %}a^{[2]}{% endkatex %}
    -   Layers count by # of hidden layer+# of output layer.
-   {% katex %}x_1,x_2,x_3{% endkatex %} -> {% katex %}4\space hidden\space nodes{% endkatex %} -> {% katex %}Output\space layer{% endkatex %}
    -   First hidden node: {% katex %}z^{[1]}_1=w^{[1]T}_1+b^{[1]}_1, a^{[1]}_1=\sigma(z^{[1]}_1){% endkatex %}
    -   Seconde hidden node: {% katex %}z^{[1]}_2=w^{[1]T}_2+b^{[1]}_2, a^{[1]}_2=\sigma(z^{[1]}_2){% endkatex %}
    -   Third hidden node: {% katex %}z^{[1]}_3=w^{[1]T}_3+b^{[1]}_3, a^{[1]}_3=\sigma(z^{[1]}_3){% endkatex %}
    -   Forth hidden node: {% katex %}z^{[1]}_4=w^{[1]T}_4+b^{[1]}_4, a^{[1]}_4=\sigma(z^{[1]}_4){% endkatex %}
-   Vectorization
    -   {% katex %}w^{[1]}=\begin{gathered}\begin{bmatrix}-w^{[1]T}_1- \\ -w^{[1]T}_2- \\ -w^{[1]T}_3- \\ -w^{[1]T}_4- \end{bmatrix}\end{gathered} (4,3)matrix{% endkatex %}
    -   {% katex %}z^{[1]}=\begin{gathered}\begin{bmatrix}-w^{[1]T}_1- \\ -w^{[1]T}_2- \\ -w^{[1]T}_3- \\ -w^{[1]T}_4- \end{bmatrix}\end{gathered}\cdot \begin{gathered}\begin{bmatrix}x_1 \\ x_2 \\ x_3 \end{bmatrix}\end{gathered} + \begin{gathered}\begin{bmatrix}b^{[1]}_1 \\ b^{[1]}_2 \\b^{[1]}_3 \\ b^{[1]}_4 \end{bmatrix}\end{gathered} =\begin{gathered}\begin{bmatrix}w^{[1]T}_1\cdot x+b^{[1]}_1 \\ w^{[1]T}_2\cdot x+b^{[1]}_2 \\ w^{[1]T}_3\cdot x++b^{[1]}_3 \\ w^{[1]T}_4\cdot x+b^{[1]}_4 \end{bmatrix}\end{gathered}=\begin{gathered}\begin{bmatrix}z^{[1]}_1 \\ z^{[1]}_2 \\z^{[1]}_3 \\ z^{[1]}_4 \end{bmatrix}\end{gathered}{% endkatex %}
    -   {% katex %}a^{[1]}=\begin{gathered}\begin{bmatrix}a^{[1]}_1 \\ a^{[1]}_2 \\a^{[1]}_3 \\ a^{[1]}_4 \end{bmatrix}\end{gathered}=\sigma(z^{[1]}){% endkatex %}
    -   {% katex %}z^{[2]}=W^{[2]}\cdot a^{[1]}+b^{[2]}{% endkatex %} {% katex %}(1, 1),(1, 4),(4, 1),(1, 1){% endkatex %}
    -   {% katex %}a^{[2]}=\sigma(z^{[2]}){% endkatex %} {% katex %}(1,1),(1,1){% endkatex %}
    -   {% katex %}a^{[2](i)}{% endkatex %}: layer {% katex %}2{% endkatex %}; example {% katex %}i{% endkatex %}
-   for i=1 to m:
    -   {% katex %}z^{[1](i)}=W^{[1]}\cdot x(i)+b^{[1]}{% endkatex %}
    -   {% katex %}a^{[1](i)}=\sigma(z^{[1](i)}){% endkatex %}
    -   {% katex %}z^{[2](i)}=W^{[2]}\cdot a^{[1](i)}+b^{[2]}{% endkatex %}
    -   {% katex %}a^{[2](i)}=\sigma(z^{[2](i)}){% endkatex %}
-   Vectorizing of the above for loop
    -   {% katex %}X=\begin{gathered}\begin{bmatrix}| & | & | & | \\ x^{(1)}, &  x^{(2)}, & ..., & x^{(m)} \\ | & | & | & |\end{bmatrix}\end{gathered} (n_x,m)matrix{% endkatex %}    n is different hidden units
    -   {% katex %}Z^{[1]}=W^{[1]}\cdot X+b^{[1]}{% endkatex %}
    -   {% katex %}A^{[1]}=\sigma(Z^{[1]}){% endkatex %}
    -   {% katex %}Z^{[2]}=W^{[2]}\cdot A^{[1]}+b^{[2]}{% endkatex %}
    -   {% katex %}A^{[2]}=\sigma(Z^{[2]}){% endkatex %}
    -   hrizontally: training examples; vertically: hidden units

#### 1.3.2 Activation Functions

-   {% katex %}g^{[i]}{% endkatex %}: activation function of layer {% katex %}i{% endkatex %}
    -   Sigmoid:    {% katex %}a=\dfrac{1}{1+e^{[-z]}}{% endkatex %}
    -   Tanh:    {% katex %}a=\dfrac{e^z-e^{[-z]}}{e^z+e^{[-z]}}{% endkatex %}
    -   ReLU:    {% katex %}a=max(0,z){% endkatex %}
    -   Leaky ReLu:    {% katex %}a=max(0.01z, z){% endkatex %}
-   Rules to choose activation function
    1.   Output is between {0, 1}, choose sigmoid.
    2.   Default choose ReLu.
-   Why need non-liner activation function
    -   Use linear hidden layer will be useless to have multiple hidden layers. It will become {% katex %}a=w'x+b'{% endkatex %}.
    -   Linear may sometime use at output layer but with non-linear at hidden layers.

#### 1.3.3 Forward and Backward Propogation

-   Derivative of activation function
    -   Sigmoid: {% katex %}g'(z)=\dfrac{d}{dz}g(z)=\dfrac{1}{1+e^{[-z]}}(1-\dfrac{1}{1+e^{[-z]}})=g(z)(1-g(z))=a(1-a){% endkatex %}
    -   Tanh: {% katex %}g'(z)=\dfrac{d}{dz}g(z)=1-(tanh(z))^2{% endkatex %}
    -   ReLU: {% katex %}g'(z)=\left\{\begin{array}{lr}0&if \space z<0 \\1&if \space z\geq0\\\usepackage{undefined}&\usepackage{if \space z=0}\end{array}\right.{% endkatex %}
    -   Leaky ReLU: {% katex %}g'(z)=\left\{\begin{array}{lr}0.01&if \space z<0 \\1&if \space z\geq0\end{array}\right.{% endkatex %}
-   Gradient descent for neural networks
    -   Parameters: {% katex %}w^{[1]}(n^{[1]},n^{[2]}), b^{[1]}(n^{[2]},1),w^{[2]}(n^{[2]},n^{[1]}), b^{[2]}(n^{[2]},1){% endkatex %}
    -   {% katex %}n_x=n^{[0]},n^{[1]},n^{[2]}=1{% endkatex %}
    -   Cost function: {% katex %}J(w^{[1]}, b^{[1]},w^{[2]}, b^{[2]})=\dfrac{1}{m}\sum\limits_{i=1}^nL(\hat{y},y){% endkatex %}
-   Forward propagation:
    -   {% katex %}Z^{[1]}=W^{[1]}\cdot X+b^{[1]}{% endkatex %}
    -   {% katex %}A^{[1]}=g^{[1]}(Z^{[1]}){% endkatex %}
    -   {% katex %}Z^{[2]}=W^{[2]}\cdot A^{[1]}+b^{[2]}{% endkatex %}
    -   {% katex %}A^{[2]}=g^{[2]}(Z^{[2]})=\sigma(Z^{[2]}){% endkatex %}
-   Back Propogation:
    -   {% katex %}dZ^{[2]}=A^{[2]}-Y{% endkatex %}    {% katex %}Y=[y^{(1)},y^{(2)},...,y^{(m)}]{% endkatex %}
    -   {% katex %}dW^{[2]}=\dfrac{1}{m}dZ^{[2]}A^{[1]T}{% endkatex %}
    -   {% katex %}db^{[2]}=\dfrac{1}{m}np.sum(dZ^{[2]},axis=1,keepdims=True){% endkatex %}
    -   {% katex %}dZ^{[1]}=W^{[2]T}dZ^{[2]}*g'^{[1]}(Z^{1}){% endkatex %}
        -   {% katex %}(n^{[1]},m)->element-wise\space product->(n^{[1]},m){% endkatex %}
    -   {% katex %}dW^{[1]}=\dfrac{1}{m}dZ^{[1]}X^{T}{% endkatex %}
    -   {% katex %}db^{[1]}=\dfrac{1}{m}np.sum(dZ^{[1]},axis=1,keepdims=True){% endkatex %}
-   Random Initialization
    -   {% katex %}x_1,x_2->a_1^{[1]},a_2^{[1]}->a_1^{[2]}->\hat{y}{% endkatex %}
    -   {% katex %}w^{[1]}=np.random.randn((2,2))*0.01{% endkatex %}
    -   {% katex %}b^{[1]}=np.zeros((2,1)){% endkatex %}
    -   {% katex %}w^{[2]}=np.random.randn((1,2))*0.01{% endkatex %}
    -   {% katex %}b^{[2]}=0{% endkatex %}

### 1.4 Deep Neural Networks

#### 1.4.1 Deep L-Layer Neural Network

-   Deep neural network notation
    -   ![deep-learning-notes_1-4-1](https://s2.loli.net/2023/11/20/9w2GKxylSrjfoFq.jpg)
    -   {% katex %}L=4{% endkatex %} (#layers)
    -   {% katex %}n^{[l]}= \#\space units\space in\space layer\space l {% endkatex %}
        -   {% katex %}n^{[1]}=5,n^{[2]}=5,n^{[3]}=3,n^{[4]}=n^{[l]}=1{% endkatex %}
        -   {% katex %}n^{[0]}=n_x=3{% endkatex %}
    -   {% katex %}a^{[l]}=activations\space in\space layer\space l{% endkatex %}
    -   {% katex %}a^{[l]}=g^{[l]}(z^{[l]}),\space w^{[l]}=weights\space for\space z^{[l]},\space b^{[l]}=bias\space for\space z^{[l]}{% endkatex %}
    -   {% katex %}x=a^{[0]},\space \hat{y}=a^{l}{% endkatex %}

#### 1.4.2 Forward Propagation in a Deep Network

-   General: {% katex %}Z^{[l]}=w^{[l]}A^{[l-1]}+b^{[l]}, A^{[l]}=g^{[l]}(Z^{[l]}){% endkatex %}
    -   {% katex %}x: z^{[1]}=w^{[1]}a^{[0]}+b^{[1]}, a^{[1]}=g^{[1]}(z^{[1]}){% endkatex %}    {% katex %}a^{[0]}=X{% endkatex %}
    -   {% katex %}z^{[2]}=w^{[2]}a^{[1]}+b^{[2]}, a^{[1]}=g^{[2]}(z^{[2]}){% endkatex %}
    -   ...
    -    {% katex %}z^{[4]}=w^{[4]}a^{[3]}+b^{[4]}, a^{[4]}=g^{[4]}(z^{[4]})=\hat{y}{% endkatex %}
-   Vectorizing:
    -   {% katex %}Z^{[1]}=w^{[1]}A^{[0]}+b^{[1]}, A^{[1]}=g^{[1]}(Z^{[1]}){% endkatex %}    {% katex %}A^{[0]}=X{% endkatex %}
    -   {% katex %}Z^{[2]}=w^{[2]}A^{[1]}+b^{[2]}, A^{[2]}=g^{[2]}(Z^{[2]}){% endkatex %}
    -   {% katex %}\hat{Y}=g(Z^{[4]})=A^{[4]}{% endkatex %}
-   Matrix dimensions
    -   ![deep-learning-notes_1-4-2](https://s2.loli.net/2023/11/20/a6emOyncIbRlo8w.jpg)
    -   {% katex %}z^{[1]}=w^{[1]}\cdot x+b^{[1]}{% endkatex %}
    -   {% katex %}z^{[1]}=(3,1),w^{[1]}=(3,2),x=(2,1),b^{[1]}=(3,1){% endkatex %}
    -   {% katex %}z^{[1]}=(n^{[1]},1),w^{[1]}=(n^{[1]},n^{[0]}),x=(n^{[0]},1),b^{[1]}=(n^{[1]},1){% endkatex %}
    -   {% katex %}w^{[l]}/dw^{[l]}=(n^{[l]},n^{[l-1]}),b^{[l]}/db^{[l]}=(n^{[l]},1){% endkatex %}
    -   {% katex %}z^{[l]},a^{[l]}=(n^{[l]},1),Z^{[l]}/dZ^{[l]},A^{[l]}/dA^{[l]}=(n^{[l]},1){% endkatex %}    {% katex %}l=0, A^{[0]}=X=(n^{[0]},m){% endkatex %}
-   Why deep representation?
    -   Earier layers learn simple features; later deeper layers put together to detect more complex things.
    -   Circuit theory and deep learning: Informally: There are functions you can compute with a "small" L-layer deep neural network that shallower networks require exponentially more hidden units to compute.

#### 1.4.3 Building Blocks of Deep Neural Networks

-   Forward and backward functions
    -   ![deep-learning-notes_1-4-3](https://s2.loli.net/2023/11/20/PBfq6ISu2h8vKeV.jpg)
    -   Layer {% katex %}l:w^{[l]},b^{[l]}{% endkatex %}
    -   Forward: Input {% katex %}a^{[l-1]}{% endkatex %}, output {% katex %}a^{[l]}{% endkatex %}
        -   {% katex %}z^{[l]}:w^{[l]}a^{[l-1]}+b^{[l]}{% endkatex %}    {% katex %}cache\space z^{[l]}{% endkatex %}
        -   {% katex %}a^{[l]}:g^{[l]}(z^{[l]}){% endkatex %}
    -   Backward: Input {% katex %}da^{[l]}, cache(z^{[l]}){% endkatex %}, output {% katex %}da^{[l-1]},dw^{[l]},db^{[l]}{% endkatex %}
-   One iteration of gradient descent of neural network
    -   ![deep-learning-notes_1-4-3-2](https://s2.loli.net/2023/11/20/35UIkJnmlSHt82j.jpg)
-   How to implement?
    -   Forward propagation for layer {% katex %}l{% endkatex %}
        -    Input {% katex %}a^{[l-1]}{% endkatex %}, output {% katex %}a^{[l]},cache\space (z^{[l]}){% endkatex %}
            -   {% katex %}z^{[l]}=w^{[l]}a^{[l-1]}+b^{[l]}{% endkatex %}
            -   {% katex %}a^{[l]}=g^{[l]}(z^{[l]}){% endkatex %}
        -   Vectoried
            -   {% katex %}Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]}{% endkatex %}
            -   {% katex %}A^{[l]}=g^{[l]}(Z^{[l]}){% endkatex %}
    -   Backward propagation for layer {% katex %}l{% endkatex %}
        -   Input {% katex %}da^{[l]}, cache(z^{[l]}){% endkatex %}, output {% katex %}da^{[l-1]},dw^{[l]},db^{[l]}{% endkatex %}
            -   {% katex %}dz^{[l]}=da^{[l]}*g'^{[l]}(z^{[l]}){% endkatex %}
            -   {% katex %}dw^{[l]}=dz^{[l]}\cdot a^{[l-1]}{% endkatex %}
            -   {% katex %}db^{[l]}=dz^{[l]}{% endkatex %}
            -   {% katex %}da^{[l-1]}=w^{[l]T}\cdot dz^{[l]}{% endkatex %}
        -   Vectorized:
            -   {% katex %}dZ^{[l]}=dA^{[l]}*g'^{[l]}(Z^{[l]}){% endkatex %}
            -   {% katex %}dW^{[l]}=\dfrac{1}{m}dZ^{[l]}A^{[l-1]T}{% endkatex %}
            -   {% katex %}db^{[l]}=\dfrac{1}{m}np.sum(dZ^{[l]},axis=1,keepdims=True){% endkatex %}
            -   {% katex %}dA^{[l-1]}=W^{[l]T}\cdot dZ^{[l]}{% endkatex %}

#### 1.4.4 Parameters vs. Hyperparameters

-   Parameters: {% katex %}W^{[1]}, b^{[1]}, W^{[2]}, b^{[2]},...{% endkatex %}
-   Hyperparameters (will affect/control/determine parameters):
    -   learning rate {% katex %}\alpha{% endkatex %}
    -   \# iterations
    -   \# of hidden units {% katex %}n^{[1]},n^{[2]},...{% endkatex %}
    -   \# of hidden layers
    -   Choice of activation function
-   Later: momemtum, minibatch size, regularization parameters,...

## II. Improving Deep Neural Networks: Hyperparameter Tuning, Regularization and Optimization

### 2.1 Practical Aspects of Deep Learning

#### 2.1.1 Train / Dev / Test sets

-   Big data may need only 1% or even less dev/test sets.
-   Mismatched: Make sure dev/test come from same distribution
-   Not having a test set might be okay. (Only dev set.)

#### 2.1.2 Bias / Variance

![deep-learning-notes_2-1-2](https://s2.loli.net/2023/11/21/ROywuJQ3dNzfhBo.jpg)

![deep-learning-notes_2-1-2-2](https://s2.loli.net/2023/11/21/S4cZ3Aua8es7WfG.jpg)

-   Assume optimal (Bayes) error: {% katex %}\approx0\%{% endkatex %}
-   High bias (underfitting): The prediction cannot classify different elemets as we want.
    -   Training set error {% katex %}15\%{% endkatex %}, Dev set error {% katex %}16\%{% endkatex %}.
    -   Training set error {% katex %}15\%{% endkatex %}, Dev set error {% katex %}30\%{% endkatex %}.
-   "just right": The prediction perfectly classify different elemets as we want.
    -   Training set error {% katex %}0.5\%{% endkatex %}, Dev set error {% katex %}1\%{% endkatex %}.
-   High variance (overfitting): The prediction 100% classify different elemets.
    -   Training set error {% katex %}1\%{% endkatex %}, Dev set error {% katex %}11\%{% endkatex %}.
    -   Training set error {% katex %}15\%{% endkatex %}, Dev set error {% katex %}30\%{% endkatex %}.

#### 2.1.3 Basic Recipe for Machine Learning

##### 2.1.3.1 Basic Recipe

-   High bias(training data performance)
    -   Bigger network
    -   Train longer
    -   (NN architecture search)
-   High variance (dev set performance)
    -   More data
    -   Regulairzation
    -   (NN architecture search)

##### 2.1.3.2 Regularization

-   Logistic regression.  {% katex %}\min\limits_{w,b}J(w,b){% endkatex %}
    -   {% katex %}w\in\mathbb{R}^{n_x}, b\in\mathbb{R}{% endkatex %}
    -   {% katex %}\lambda=regularization\space parameter{% endkatex %}
    -   {% katex %}J(w,b)=\dfrac{1}{m}\sum\limits_{i=1}^mL(\hat{y}^{(i)},y^{(i)})+\dfrac{\lambda}{2m}||w^2||_2{% endkatex %}
    -   L2 regularization    {% katex %}||w^2||_2=\sum\limits_{j=1}^{n_x}w_j^2=w^Tw{% endkatex %}
    -   L1 regularization    {% katex %}\dfrac{\lambda}{2m}\sum\limits_{j=1}^{n_x}|w_j|=\dfrac{\lambda}{2m}||w||_1{% endkatex %}
        -   {% katex %}w{% endkatex %} will be spouse(for L1) (will have lots of 0 in it, only help a little bit)
-   Neural network
    -   {% katex %}J(w^{[1]},b^{[1]},...,w^{[l]},b^{[l]})=\dfrac{1}{m}\sum\limits_{i=1}^{m}L(\hat{y}^{(i)},y^{(i)})+\dfrac{\lambda}{2m}\sum\limits_{l=1}^{l}||w^2||_F{% endkatex %}
    -   {% katex %}||w^{[l]}||_F^2=\sum\limits_{i=1}^{n^{[l-1]}}\sum\limits_{j=1}^{n^{[l]}}(w_{ij}^{[l]})^2{% endkatex %}    {% katex %}w: (w^{[l]},w^{[l-1]}){% endkatex %}
        -   Frobenius norm: Square root of square sum of all elements in a matrix.
    -   {% katex %}dw^{[l]}=(from\space backprop)+\dfrac{\lambda}{m}w^{[l]}{% endkatex %}
        -   {% katex %}w^{[l]}:=w^{[l]}-\alpha dw^{[l]}{% endkatex %} (keep the same)
        -   Weight decay
            -   {% katex %}w^{[l]}:=w^{[l]}-\alpha[(from\space backprop)+\dfrac{\lambda}{m}w^{[l]}]{% endkatex %}
            -   ​        {% katex %}=w^{[l]}-\dfrac{\alpha\lambda}{m}w^{[l]}-\alpha(from\space backprop){% endkatex %}
            -   ​        {% katex %}=(1-\dfrac{\alpha\lambda}{m})w^{[l]}-\alpha(from\space backprop){% endkatex %}
-   How does regularization prevent overfitting: {% katex %}\lambda{% endkatex %} bigger {% katex %}w^{[l]}{% endkatex %} smaller {% katex %}z^{[l]}{% endkatex %} smaller, which will make the activation function nearly linear(take tanh as an example). This will cause the network really hard to draw boundary with curve.
-   Dropout regularization
    -   ![deep-learning-notes_2-1-3-2](https://s2.loli.net/2023/11/21/WTqeEg4MDPbtK12.jpg)
    -   Implementing dropout("Inverted dropout")
        -   Illustrate with layer {% katex %}l=3{% endkatex %} {% katex %}keep-prob=0.8{% endkatex %} (means 0.2 chance get dropout/be 0 out)
        -   {% katex %}d3 = np.random.rand(a3.shape[0],a3.shape[1]) < keep-prob{% endkatex %}    #This will set d3 to be a same shape matrix as a3 with True (1), False (0) value.
        -   {% katex %}a3 = np.multiply(a3, d3){% endkatex %}  #a3*=d3; This will let some neruons been dropout
        -   {% katex %}a3/=keep-prob{% endkatex %}    #inverted dropout, keep the total avtivation the same before and after dropout.
    -   Why work: Can't rely on any one feature, so have to spread out weights.(shrink weights)
    -   First make sure the J is decreasing during iteration, then turn on dropout.
-   Data augmentation
    -   Image: crop, flop, twist...
-   Early stopping
    -   Mid-size {% katex %}||w||_F^2{% endkatex %}
    -   May caused optimize cost function and not overfir at the same time.
-   Orthogonalization
    -   Only consider optimize cost function or consider not overfit at one time.

##### 2.1.3.3 Setting up your optimization problem

-   Normalizing training sets
    -   ![deep-learning-notes_2-1-3-3](https://s2.loli.net/2023/11/21/jtT9fC5nw2R7xqo.jpg)
    -   {% katex %}x=\begin{gathered}\begin{bmatrix}x_1 \\ x_2\end{bmatrix}\end{gathered}{% endkatex %}
    -   Subtract mean:
        -   {% katex %}\mu=\dfrac{1}{m}\sum\limits_{i=1}^{m}x^{(i)}{% endkatex %}
        -   {% katex %}x:=x-\mu{% endkatex %}
    -   Normalize variance:
        -   {% katex %}\sigma^2=\dfrac{1}{m}\sum\limits_{i=1}^{m}x^{(i)}**2{% endkatex %}   "**" element-wise
        -   {% katex %}x/=\sigma^2{% endkatex %}
    -   Use same {% katex %}\mu,\sigma^2{% endkatex %} to normalize test set.
    -   Why normalize inputs?
        -   When inputs in very different scales will help a lot for performance and gradient descent/learning rate.
        -   ![deep-learning-notes_2-1-3-3-2](https://s2.loli.net/2023/11/21/MW7wNCXahR3FZx9.jpg)
-   Vanishing/exploding gradients
    -   {% katex %}w^{[l]}>I{% endkatex %} Just slightly, will make the gradient increase really fast (exploding). 
    -   {% katex %}w^{[l]}<I{% endkatex %} Just slightly, will make the gradient decrease really slow (varnishing). 
-   Weight initalization (Single neuron)
    -   large {% katex %}n{% endkatex %} (number of input features) --> smaller {% katex %}w_i{% endkatex %}
    -   {% katex %}Variance(w:)=\dfrac{1}{n}{% endkatex %} (sigmoid/tanh)    ReLU: {% katex %}\dfrac{2}{n}{% endkatex %}  (variance can be a hyperparameter, DO NOT DO THAT)
    -   {% katex %}w^{[l]}=np.random.randn(shapeOfMatrix)*np.sqrt(\dfrac{1}{n^{[l-1]}}){% endkatex %}    ReLU: {% katex %}\dfrac{2}{n^{[l-1]}}{% endkatex %}
    -   Xavier initialization: {% katex %}\sqrt{\dfrac{1}{n^{[l-1]}})}{% endkatex %} Sometime {% katex %}\sqrt{\dfrac{2}{n^{[l-1]}+n^{[l]}})}{% endkatex %}
-   Numerical approximation of gradients
    -   {% katex %}\dfrac{f(\theta+\epsilon)-f(\theta-\epsilon)}{2\epsilon}{% endkatex %}
-   Gradient checking (Grad check)
    -   Take {% katex %}W^{[1]},b^{[1]},...,W^{[L]},b^{[L]}{% endkatex %} and reshape into a big vector {% katex %}\theta{% endkatex %}.
    -   Take {% katex %}dW^{[1]},db^{[1]},...,dW^{[L]},db^{[L]}{% endkatex %} and reshape into a big vector {% katex %}d\theta{% endkatex %}.
    -   for each i:
        -   {% katex %}d\theta_{approx}[i]=\dfrac{J(\theta_1,\theta_2,...,\theta_i+\epsilon,...)-J(\theta_1,\theta_2,...,\theta_i-\epsilon,...)}{2\epsilon}\approx d\theta[i]=\dfrac{\partial J}{\partial \theta_i}{% endkatex %}
        -   Check Euclidean distance {% katex %}\dfrac{||d\theta_{approx}-d\theta||_2}{||d\theta_{approx}||_2+||d\theta||_2}{% endkatex %}   ({% katex %}||.||_2{% endkatex %} is Euclidean norm, sqare root of the sum of all elements' power of 2)
        -   take {% katex %}\epsilon=10^{-7}{% endkatex %}, if above Euclidean distance is {% katex %}\approx10^{-7}{% endkatex %} or smaller, is great.
        -   If is {% katex %}10^{-5}{% endkatex %} or bigger may need to check.
        -   If is {% katex %}10^{-3}{% endkatex %} or bigger may need to worry, maybe a bug. Check which i approx is difference between the real value.
    -   notes:
        -   Don't use in training - only to debug.
        -   If algorithm fails grad check, look at components to try to identify bug.
        -   Remember regularization. (include the {% katex %}\dfrac{\lambda}{2m}{% endkatex %})
        -   Doesn't work with dropout. (since is random, implement without dropout)
        -   Run at random initialization; perhaps again after some training. (not work when {% katex %}w,b\approx0{% endkatex %})

### 2.2 Optimization Algorithms

#### 2.2.1 Mini-batch gradient descent

#### 2.2.2 Exponentially weighted averages

#### 2.2.3 RMSprop and Adam optimization

### 2.3 Hyperparameter Tuning, Batch Normalization, and Programming Frameworks

#### 2.3.1 Tuning process

#### 2.3.2 Using an appropriate scale to pick hyperparameters

#### 2.3.3Batch Normalization

#### 2.3.4 Multi-class classification

## III. Structuring Machine Learning Projects



## IV. Convolutional Neural Networks



## V. Sequence Models