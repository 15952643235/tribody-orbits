# tribody-orbits
homework
"""
Created on Tue Jun 12 23:21:32 2018

@author: Huang
"""

import numpy as np
import matplotlib.pylab as pl
import matplotlib.pyplot as plt
import matplotlib.animation as animation

''' 2  3   4 '''

M1=1.0
M2=1.0
M3=1.0
G=1.0
N=2000000
n=2000001
vx=(0.30689,0.39295,0.18428,0.46444,0.43917,0.40592,0.38344,0.08330,0.350112,0.08058,0.55906,0.51394,0.28270,0.41682,0.41734)
vy=(0.12551,0.09758,0.58719,0.39606,0.45297,0.23016,0.37736,0.12789,0.07934,0.58884,0.34919,0.30474,0.32721,0.33033,0.31310)
T=(6.2356,7.0039,63.5345,14.8939,28.6703,13.8658,25.8406,10.4668,79.4759,21.2710,55.5018,17.3284,10.9626,55.7898,54.2076)
x1=np.zeros(n)
y1=np.zeros(n)
x2=np.zeros(n)
y2=np.zeros(n)
x3=np.zeros(n)
y3=np.zeros(n)
vx1=np.zeros(n)
vy1=np.zeros(n)
vx2=np.zeros(n)
vy2=np.zeros(n)
vx3=np.zeros(n)
vy3=np.zeros(n)

def F(x1,x2,x3,y1,y2,y3,M1,M2,M3):
    return -G*M2*M1*(x1-x2[i])/(((x1-x2[i])**2+(y1[i]-y2[i])**2)**(3/2))\
    -G*M3*M1*(x1-x3[i])/(((x1-x3[i])**2+(y1[i]-y3[i])**2)**(3/2))
     
    
for j in range(3,15):
    print(j)
    vx1[0]=vx[j]
    vy1[0]=vy[j]


    x1[0]=-1.0
    y1[0]=0.0
    x2[0]=1.0
    y2[0]=0.0
    x3[0]=0.0
    y3[0]=0.0
    vx2[0]=vx1[0]
    vy2[0]=vy1[0]
    vx3[0]=-2.0*vx1[0]
    vy3[0]=-2.0*vy1[0]
    i=0
    dt=0.00001
    
   
    def Oular(x1,x2,x3,y1,y2,y3,v1,M1,M2,M3):
        v1[i+1]=v1[i]+F(x1[i],x2,x3,y1,y2,y3,M1,M2,M3)/M1*dt
        x1[i+1]=x1[i]+(v1[i]+v1[i+1])*dt/2.0
        
    for i in range(N):
        Oular(x1,x2,x3,y1,y2,y3,vx1,M1,M2,M3)
        Oular(y1,y2,y3,x1,x2,x3,vy1,M1,M2,M3)
        Oular(x2,x1,x3,y2,y1,y3,vx2,M2,M1,M3)
        Oular(y2,y1,y3,x2,x1,x3,vy2,M2,M1,M3)
        Oular(x3,x2,x1,y3,y2,y1,vx3,M3,M2,M1)
        Oular(y3,y2,y1,x3,x2,x1,vy3,M3,M2,M1)    
        print(i)
    print(j)
    
    fig1=pl.figure()
    plt.plot(x1,y1, 'r-',linewidth=1.0)
    plt.plot(x2,y2, 'c-',linewidth=1.0)
    plt.plot(x3,y3, 'y-',linewidth=1.0)
    d1, = pl.plot([], [], 'ro',markersize=5)
    d2, = pl.plot([], [], 'co',markersize=5)
    d3, = pl.plot([], [], 'yo',markersize=5)
    '''#dot1_ani = animation.FuncAnimation(fig1, update_line1, np.arange(1000),\
    #fargs=(x1,y1,d1,x2,y2,d2,x3,y3,d3),interval=2, blit=False)'''
    
    pl.show()
