Reflection on PID project

* Tuning sequence: P first, then D, finally I. 
	* Proportional factor is the most important parameter that sets the basis of PID controller, which should be tuned first. 
	* I started as P=0.5, and D=0 and I=0. The car drives wobbly in zigzag route which means P is too big. P0.5.mov showed the case.
	* Reducing P to 0.1 resolved the problem and the car drives much smoother in straight route, but it cannot adjust fast enough to turns. Differential factor is the helper.
	* Setting P=0.1, D=0.3 can drive the car full loop as P0.1_D0.3.mov shows. 
	* I factor in this case doesn't help much once P and D are settled down, it can only be set to very small value, in my case 0.0003. Setting it to bigger values cause problems, say I=0.3 caused big turns (overshoots) on straight route in I0.3.mov.
* Slow down in (sharp) turns. 
	* One other lesson learned from experiment is to slow down in (sharp) turns, just as what we'll do in real life. Even steering controller provides correct commands, if too fast speed, the car didn't find chance to adjust itself back on track. 
	* To avoid slowing down too much, the brake is only applied when speed is larger than 20.0, and in a proportional way. A P-only controller on speed seems works well enough here. 
		         if((fabs(steer_value)>0.1) && (speed > 20.0))
		  	            throttle = -0.005*speed;