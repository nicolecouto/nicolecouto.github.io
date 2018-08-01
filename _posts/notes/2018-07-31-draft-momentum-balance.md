---
layout: page-fullwidth
subheadline:  "31 July 2018"
title:  "Momentum balance"
teaser: ""
breadcrumb: true
tags:
    - notes format
categories:
    - notes
---
# Momentum balance in Bering Strait
### July 26-30, 2018


### To do list #1
- [x] 1.1 Recalculate $\tau_b$ from $\epsilon$ within the bottom boundary layer.  
- [x] 1.2 Plot $\tau_b$  from $\epsilon$ vs v to see if the value of $C_d$ makes sense.
- [x] 1.3 Plot "theoretical curve using this value of $C_d$"
- [x] 1.4 On top of theoretical curve, plot $\tau_b$ from velocity data and from $\epsilon$ data.


I did a lot of work to calculate the values of $u_*$ using the modified law of the wall approach and the ordinary law of the wall approach in the scripts:

```Matlab
calc_bottom_boundary_layer.m
pick_hd_by_RMS.m
wind_and_transport.m
```

Now use:
```Matlab
fig_addNewTau.m
```
to quickly process these new steps and compare to what I did before.

### 1.1 and 1.2
Plot $C_d = \frac{\tau_b}{\rho v^2}$ and compare to assumed value of $C_d = 1.225  \times 10^{-3}$

$\tau_b$ is calculated using $\epsilon$ measurements in the bottom boundary calc_bottom_boundary_layer.

```Matlab
for iProf=1:length(u_star)
    inBBL = zMat(:,iProf) <= zBBL(iProf);
    rho(iProf) = nanmean(data(2).pdens_smooth(inBBL,iProf));
    E = data(2).eps(inBBL,iProf);
    z = zMat(inBBL,iProf);
    tau_b_eps(iProf) = nanmean((E.*kappa.*z).^(1/3));  
    v_bot(iProf) = nanmean(data(2).v_smooth(inBBL,iProf));
end
```

![](./compare_to_Cd.png =500x)
<img src="./compare_to_Cd.png">

The value of $C_d$ that I get from $\tau_b$ calculated using $\epsilon$ values is much lower than the assumed value.

### 1.3 and 1.4
How does the "theoretical curve" change if I use this value of $C_d$?

Figure 3 in `wind_and_transport.m` shows the theoretical curves. Add that bit of code to `fig_andNewTau.m` and add the curve using the mean value of $C_d$.

![](./theoretical_curves_new.png =500x)

The dotted teal curve is the "theoretical" bottom stress using the average value of Cd shown above. It's closer to the values of \tau_b I get from the modified law of the wall approach.

The modified law of the wall approach is closer to this curve than the ordinary law of the wall approach.

![](./fit013.png =300x)
![](./fit024.png =300x)
![](./fit026.png =300x)

The red line seems problematic. I sum the bottom stress and wind stress to get what the pressure head should be. When northerly wind speed is greater than about 5 m/s, the pressure head becomes negative meaning that, on it's own, it would work to drive water southward through the strait. The pressure head is known to change, but not that much. In fact, Woodgate 2018 says there was
"a ~30% increase in the PH term from 2001 to 2011."

### To do list #2
- [x] 2.1 What value of $C_d$ should I be using?
  * Jen suggested recalculating based on a "synthetic $\epsilon$" (see handwritten notes from 7/26/18)
- [x] 2.2 Recalculate bottom stress from $\epsilon$
- [ ] 2.3 Remake the "theoretical values" plot with PGF held constant and $\tau_b$ = PGF - $\tau_w$


### 2.1 What value of $C_d$ should we be using?
```Matlab
calc_Cd.m
```
We know
$$u_* ^2 = C_d u_0 ^2$$
$$u_* = [C_d u_0^2]^{1/2} $$

 where $u_0$ is the velocity somewhere above the bottom boundary layer. We also know

$$\epsilon = \frac{u_* ^3}{\kappa z}$$

So we can write
$$\epsilon = \frac{[C_d u_0^2]^{3/2}}{\kappa z}$$

Compare both values of $\epsilon$ and find the value of $C_d$ for which they are the closest. Here are four examples. It probably makes sense to solve this in a least squares sense instead of guessing.

![](./calc_Cd_4choices.png =500x)

##### Find the best value of Cd in a least-squares sense.

```
b = A\y;
```
where
$$ y = \epsilon^{2/3} $$
$$ A = \left[ \frac{u_0}{(\kappa z)^{1/3}} \right]^2 $$

![](./calc_Cd_leastSquares.png =500x)

The best fit is when $C_d = 1.17 \times 10^{-3}$.

Plot sections of $\epsilon$ and synthetic $\epsilon$ near the bottom:

![](./compare_eps_inBBL.png =600x)


### 2.2 Recalculate bottom stress from $\epsilon$

Continue with
```Matlab
 calc_Cd.m
```

$$\tau_b = \rho u_*^2$$
$$u_* = \left(C_d u_0^2 \right)^{1/2} $$


where $u_0$ is the velocity just above the bottom boundary layer.

### 2.3 Remake the "theoretical values" plot with PGF held constant
The pressure head changes, but on seasonal, not synoptic time scales. So it makes more sense to show an average value. Also, the bottom stress calculated from the relationships between wind speed and transport/velocity have a lot of variability. I should at least show that on a trend line. Maybe it makes sense to plot them both ways with errors for both calculations.

- [x] Plot $\tau_b$ values from three different values of $u_*$:
* synthetic $\epsilon$ calculation
* modified law of the wall
* ordinary law of the wall

![](./theoretical_curves_new2.png =800x)

The green dots go really far out of the limits of this graph. Down to ~ -10  $N m^{-2}$

- [x] Bin average the different values of $\tau_b$ by wind speed so you can better see the curves.

![](./theoretical_curves_new2_binned.png =800x)

- [ ] Add uncertainty/standard deviation around curves
- [ ] Add theoretical bottom stress using calculated $C_d$.


## Other Post Formats
{: .t60 }
