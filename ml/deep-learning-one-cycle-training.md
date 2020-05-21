Deep Learning One Cycle Training
================================

The fast.ai library has implemented something called 1cycle policy. It's pretty neat: the cycle progressively increases the LR while decreasing momentum, and then proceeds to do the exact opposite. This has been shown to lead to much faster convergence than training with a fixed learning rate. It does require picking an optimal learning rate with a LR finder (also easily accessible in the fast.ai library). This fast training phenomenon is called superconvergence.

I tried this myself on a transfer learning problem and got good results very quickly, much quicker than with my usual Keras approach with manual stepwise annealing in 2 or 3 steps.

Useful links:

- [fast.ai docs](https://docs.fast.ai/callbacks.one_cycle.html)
- [paper by Leslie Smith](https://arxiv.org/pdf/1803.09820.pdf)
- [blogpost](https://sgugger.github.io/the-1cycle-policy.html)
