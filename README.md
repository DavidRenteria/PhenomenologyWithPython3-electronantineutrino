# Particle physics phenomenology with Python 3: electron-antineutrino to electron-antineutrino scattering in the Fermi theory
These codes in Python 3 are used to calculate the scattering cross section of electron-antineutrino procces. The file 
`Montecarlo` is a pseudocode written in Python 3 to make the computation of the Cross Section by means of the Montecarlo method,
while, the file `Riemann sums` makes the calculation of the same Cross Section by means of the Riemann sums method. Meanwhile, the
file `Invariant amplitude` is a function, also written in Python 3, used by both methods and corresponds to the calculation of 
the square modulus of the invariant amplitude of scattering for the electron-antineutrino process. Finally, in the `Modules` 
folder, we find the pseudocodes `Differential cross section`, `RGE's` and `Invariant amplitude`  used to calculate and graph the 
dispersion of the cross section, solve the renormalization group equations and the invariant amplitude respectively. These last 
files are employed Montecarlo method  and Riemann sums.  

## Review
The general idea is resolve the equation (30) numerically  through create   random momentums in 
the  *x*, *y* and *z* components with a center of mass energy  lower than 1 TeV. This way, we build a set of random four vectors 
for the electron and antineutrino   with angles between 0 and 180 degrees. 
   
As well  know, the Fermi constant is depending of coupling constant, witch  we saw in equation (15),  this mean that the Fermi 
constant varies respect to energy of center mass system. For resolve the group renormalization equations (file `RGE's` ) the 
first pas is solve the differential equations (17),  in order to adjusted  *G_F* to process's energy. 
The method used to solve the system of differential equations in Phyton is Runge-Kutta 4. 

The next step is computing the `Invariant amplitude`  with help of equation (31). But to program the equation
(31), we have programmed the *gamma* matrices of equation (9) and *gamma_5* as shown in the 
table 2. 

Once the *gamma_i* and *gamma_5* matrices have been computed, we create a  function to calculate the invariant
amplitude average. Once we have obtained the invariant amplitude average, we calculate the cross section distribution 

In the corss secction distribution (file `Differential cross 
section`) we generate events for energy processes from 
0 GeV to 1000 GeV and adapt the Fermi constant *G_F* to the energy of the event.
The events have been conditioned so that their initial momentums are the same as their final momentums, to ensure energy 
conservation. The integral of equation (30) has not been calculated with Python 3, but we have been aided by equation 
(34).

## Montecarlo

Finally to obtain the distribution, we will have to make an adjustment with *curve_fit* on the enveloping 
points of the dispersion obtained and graph for energies less than 1000 GeV. To calculate the total effective section with 
Montecarlo method we have used the *curve_fit* adjustment and then we used the Montecarlo method to calculate the area of the curve fits the dispersion.


```disAleatoriaX=[]
disAleatoriaY=[] 
disBajoLaCurvaX=[]
disBajoLaCurvaY=[]
interaction = 50000
for i in range (interaction):
    x=180*random.random()
    y=max(SEpRegresion+0.01)*random.random()
    if y<=regresion(x):
        disBajoLaCurvaX.append(x)
        disBajoLaCurvaY.append(y)
    else:
        disAleatoriaX.append(x)
        disAleatoriaY.append(y)


areaMontecarlo=((len(disBajoLaCurvaY))/(len(disBajoLaCurvaY)+len(disAleatoriaY)))*(180*max(SEpRegresion+0.01))*(pi/180)
areaMontecarlo
```


## Riemman sums
While with Riemann sums, instead of making an adjustment  we have sum the areas generated by points of the envelope in 50 equal intervals. 

```areaBajoLaCurva=0
for i in range(len(nuevoAng)-1):
    areaBajoLaCurva=areaBajoLaCurva+(vecindad*pi/180)*nuevoSEp[i+1]
areaBajoLaCurva
```
