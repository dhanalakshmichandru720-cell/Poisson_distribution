Fitting Poisson distribution
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
 import numpy as np
import math
import scipy.stats
#Input
L = [int(i) for i in input("Enter data: ").split()]
N = len(L)
M = max(L)
X = []
f = []
#Frequency calculation
for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c += 1
    f.append(c)
    X.append(i)
sf = np.sum(f)
#Probability P(x)
p = []
for i in range(M + 1):
    p.append(f[i] / sf)
#Mean of Poisson distribution
mean = np.inner(X, p)
#Reset lists
p = []
E = []
xi = []
print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")
print("-----------------------------------")
#Poisson probability, expected frequency & Chi-square term
for x in range(M + 1):
    px = math.exp(-mean) * (mean ** x) / math.factorial(x)
    p.append(px)
   exp_f = px * sf
    E.append(exp_f)
   xi_val = ((f[x] - exp_f) ** 2) / exp_f if exp_f != 0 else 0
    xi.append(xi_val)
   print("%2d   %.3f   %4d   %.2f   %.3f" %
          (x, px, f[x], exp_f, xi_val))
print("-----------------------------------")
#Chi-square
cal_chi2 = np.sum(xi)
print("Calculated value of Chi-square = %.4f" % cal_chi2)
#Table value (1% LOS)
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print("Table value at 1%% LOS = %.4f" % table_chi2)
#Conclusion
if cal_chi2 < table_chi2:
    print("The given data CAN be fitted to Poisson Distribution at 1% LOS")
else:
    print("The given data CANNOT be fitted to Poisson Distribution at 1% LOS")
```
# Output : 
<img width="900" height="430" alt="image" src="https://github.com/user-attachments/assets/8cfed703-6b11-4016-ae08-8bd5e0073079" />



# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
