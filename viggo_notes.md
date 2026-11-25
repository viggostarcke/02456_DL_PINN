## Task 2.5
initialisation of weights and biases: all I could find was that it is 
standard to initialise biases as 0, and weights are initialised by drawing from a guassian
distribution with mean 0 and std$\sqrt{2/f}$ where $f$ is the fan-in, which is basically 
just a measure for what the weights multiply, as W1 multiplies the network input each hidden
unit gets one number, and W2 multiplies the hidden layer such that the output unit gets
M=64 numbers. Thus, W2 should be initialised with a std of $\sqrt{2/64}$ where W1 is
initialised with a std of $\sqrt{2/1}$. Note that we initialise b1 as the same as W1,
instead of 0. We tried 0, and find theres no reason in our case.\
We see that the results are not satisfying. Since the function we approximate is oscillating
quite much on the domain we reason that the weights need to grow a lot from their
initialisation to be able to catch this behaviour. To do so we try to see how our PINN learns
if we initialise every weight and bias with an increasing scale. We only do this for W1 and b1
since they are the ones acting directly on t. A std of 10 seems to be the best performer.
I think we get the best result if we settle for another $\lambda_{phys}$ with scale 10, but
I have not done this yet.

## Task 2.7
The network output is $\tilde{x}_\theta (t) = 1 + t^2 \cdot x_\theta (t)$, where $x_\theta$
is our network $y$. This gives us the initial position 
$\tilde{x}_\theta (0) = 1 + 0^2 \cdot x_\theta (0) = 1$. \
To show the time derivative also matches; $\frac{d}{dt} (1 + t^2 \cdot x_\theta(t))=
(\frac{d}{dt} t^2) \cdot x_\theta(t) + t^2 (\frac{d}{dt} x_\theta(t)) = 
2t \cdot x_\theta(t) + t^2 \frac{d}{dt} x_\theta(t)$. For $t=0$ this becomes;
$\frac{d}{dt} \tilde{x}_\theta (0) = 2(0) \cdot x_\theta (0) + (0)^2 \frac{d}{dt} x_\theta(0) = 0 + 0 = 0$.\
if $\tilde{x}_\theta (t) = 1 + t x_\theta (t)$ then 
$\frac{d}{dt} \tilde{x}_\theta (t) = x_\theta (t) + t \frac{d}{dt} x_\theta(t)$ such that 
$\frac{d}{dt} \tilde{x}_\theta (0) = x_\theta (0) + 0 \frac{d}{dt} x_\theta(0) = x_\theta (0)$
which we say is generally not true. It should hold for all weights, and it wouldnt for $t^2 \rightarrow t$.

