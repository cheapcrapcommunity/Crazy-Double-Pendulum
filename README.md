# Crazy-Double-Pendulum
Goal:

I want to create a Double Pendulum that not only relies on its physical characteristics but is also controlled by multiple settings, and these settings will cause some unexpected movement triggering certain behaviors when they meet some conditions and they cross over, sometimes like a seesaw, or sometimes like an object under an enchantment – which will change its own physical parameters instantly such as the mass and dumping value, without any external force. I applied 1st/2nd/3rd Markov chain and probabilities rules in this patch.

Several factors that impact the pendulum:
1.	Mouse clicks. Clicking anywhere inside the pendulum window will change the position unless it’s conflict with the current movement. 
2.	Rotation value and user input from the pink slider. The mouse clicks xPos and yPos are sent to a Markov chain to analyse, then the Markov1 and Markov2 receive the result from the former ones and keep producing new numbers. These numbers are sending to the posControl to change the current position, depending on the rotation value of the second hinge and comparing with the user input value from the pink slider.
3.	Dumping and mass control. Through analyzing the rotation value, and comparing with use input from the green sliders, it output decisions that affect either the dumping or the mass value. There’s also a blue slider inside the mass control and it decide when will finish feeding the Markov1 and Markov2.

Sound design:

1.	Layer1 creates a jumping spring sound according to the rotation value, position value received from markov and markov2.
2.	Layer2 uses the number from markov to produce frequency and modulate with the noise from layer4 to get more texture, so it sounds a bit frictional. The reverb plate is from Randy Jones, and I feed rotation value from the 1st and 2nd hinges into it.
3.	Layer3 receives osc2 from Layer2 and made a delay effect which using markov1 number as a parameter of its delay time signal to create a sharp and high pitch sound. It’s controlled by a gate which open when the rotation of the 2nd hinge value is smaller than 90.
4.	 Layer4 is a noise generator connecting with a resonant bandpass filter which is controlled by the filterParameters subpatch. The center frequency is controlled by markov2, and Q value is decided by the rotation degree.
5.	Layer5 is a last modification according to the current sound the double pendulum produced. The current whole sounds like the wheels of a crazy train, so I want to add a track that I recorded in train to resample. The markov3 use the Ypos of the 2nd hinge when it’s higher then 0, so when the 2nd is on the top, it keeps resampling with different starting point, and when it drops, it uses the last number from markov3 as the resample speed. However, after adding layer5, the high frequency is overlapping with the ones from layer3, so I set a specific probability weight for triggering each layer. 

<iframe title="vimeo-player" src="https://player.vimeo.com/video/666556872?h=08ac45f02f" width="640" height="360" frameborder="0" allowfullscreen></iframe>

Conclusion:

Overall, I like the sound of this piece, and the physical object brings a lot of dynamic elements to the music. I think randomness could be produced in complicated chaos, even each element in the chaos is almost certain. And the best thing is the sound won’t stop because the hinges stop moving, since there’re numbers stored in the Markov chains.


I learnt how to build the Double Pendulum through dude837's youtube tutorial: https://www.youtube.com/watch?v=GSYkr4ZSYzs&list=PLD45EDA6F67827497&index=75 and used the Plate reverb in the style of Griesinger from Randy Jones rej@2uptech.com in this patch. Thank you very much.
