# **MATLAB Traps-Tips-Troubleshooting**

This document explains some traps, tips, trouble shootings for MATLAB for beginners.



### Section 1. How To Get a Graph with MATLAB

You better get the graph from command window. This is quite classical way but its more robust and flexible.



##### In Simulink:

At first, you have to send the data that you want to plot from Simulink to MATLAB workspace. You can achieve this through "to Workspace" block.

So, find out the block and place it to your Simulink field, and connect the arbitrary signal to it. And double click the block, you have to specify the name of signal.

If the signal is named like "v", you can set the name like "v\_data" for example. Additionally, you better change the saving form "Time series" to "Array". "Array" is easy to treat for beginners.

After you checked the name of the block has changed through the procedure, now you can execute the simulation.

When the simulation has done, you can move to the command window.



##### In Command Window:

In command window, you have to execute below commands one by one.



> {arbitrary signal name} = out.{arbitrary signal name you set in the Simulink};

> t = out.tout;



Do not worry about "tout". "tout" is made by MATLAB automatically. So you do not have to specify this signal data in Simulink.

And, in this time, we will use the below whole example for instance. This example is attempting to get the Friction Force and Velocity in the workspace and extract

the certain execution time.



> v = out.v\\\_data;

> F = out.F\\\_data;

> t = out.tout;

> idx = find(t > 0.8);

> plot(v(idx), F(idx));

> grid on;

> xlabel('Velocity /(m/s)');

> ylabel('Friction Force /N');



Now you got the plotted graph with a new window. So you can save that with arbitrary name.

And do not forget to execute below command. If you do not do that, you cannot execute the same command to save another figure again.



> close all



#### Section 2. Plot Several Curves in One Graph

This will introduce how to plot several curves in one graph to compare the condition. Most of the procedure is similar to Method 1, but we have to add some operation before plot a curve.



##### In Command Window:

At first, you have to operate at command window to let the system to remain previous plotted graph.



> close all	# clean your last time graph at first

> figure		# just show up the empty figure

> grid on

> hold on	# this will work to let the system to remain previous one



##### In Simulink Field:

In Simulink, execute the simulation and do not forget about add "to Workspace" block to send data to the workspace. The procedure to achieve it is explained in Method 1.

When you achieved simulation for the first condition, you can go back to command window and do some operations.



##### In Command Window:

In command window, you have to do the same thing as Method 1. This will plot the graph you simulated.



And now, you will go back to Simulink field and try another condition. Then, move on to the command window to plot them with hold previous curve.

When you tried all of conditions, you can save it with legends and other settings(e.g. axis labeling).



#### Section 3. Semi-Colon Trap

One of the traps that almost all MATLAB beginners struggle with is this, trap about semi-colon.



for example, if you forget to put semi-colon at the end of the sentence in MATLAB function, the result of that line will be printed to the command line numerous times, because MATLAB functions are called thousands of times in execution.



So you will get an numerous amount of meaningless result at the command window. To dodge this, simply put semi-colon.





##### Section 4. Base Workspace? Model Workspace? Is it yummy???

This trap is not so much difficult. Just a distinction for convenience, that means, if you use that variable only in one model, you can declare that in Simulink. And this will be unable to recognize in any other Simulink model, or even in MATLAB command window.

So, this will cause a problem. If you want to simulate automatically with MATLAB script(ends with .m), that is trying to simulate several conditions and plot those or something like that, you have to execute your Simulink model through your MATLAB command window. So that your script cannot recognize your variable in Simulink model. 

To dodge this, you should declare several variables that you want to change with scripts in base workspace.

This will solve the problem and much easy.



