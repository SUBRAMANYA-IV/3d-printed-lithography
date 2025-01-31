# Introcution

As stated in the intro section, this project aims to simulate, design and prototype a 3d printed maskless photolithography system. 

Components like the optical setup, stage and overall structure should be 3d printable using basic fillament, with other off-the-shelf components like lenses, servos and other electronics easily bought from amazon. 

The most "difficult" to source parts of this project will be
- the projector: not really 'hard', but you have to make sure its an older DLP based projector with a mercury lamp, as these kinds of lamps emmit the highest amount of UV-light, which is important in curing the photoresist
- the beam-splitter and hot mirror: im still doing research into the pass-bands of the beam splitter, but this *might* require you to buy them from an actual optics company like thorlabs, which can get pretty pricy. Same with the UV-pass hot mirror: you're gonna have to gut the projector and replace its usual UV-blocking hot filter with a UV-pass hot filter so that a) the wavelength of light you want gets passed and b) the rest of the projector doesnt get fried

## Sections

This project is still in progress, and I only expect results mid way through the fall-semester of 2025. However, the general road map comes in 3 parts

##### Simulation and Sourcing

This was surprisingly one of the most time consuming parts.

I never had experience in executing this kind of project before, so I didnt know where to even start. 

One of the biggest hurdles was knowing what I could "work with". it was a feedback loop of not knowing what components you had/could use, and hence not being able to accurately simulate the optical setup. 

Best way to get over this is to just hop onto amazon and search for the components within your budget, and that (roughly) accomplish what you need. The second part is important; **dont get hung up on the details**, design around these limitations, not the other way around. 


Next biggest hurdle was simulations; I spent a solid 3-4 days just trying to find a simulation software that would fit my needs, and was open source. It'd usually go something like 
- find software
- spend 3-4 hours managing/resolving dependencies
- learn how to use the software for 2-3 hours
- realise it isnt what I wanted/needed

I dont think you can really avoid this. I ended up settling on a program called "**Aether**", which was a ray-tracing/optical simulation software written in C++ by a group at University of technology, Troyes, France. It has an intuitive GUI and is overall simple to use. The real kicker is the amount of flexibility you have in terms of defining materials and devices, all the way from refractive indicies and the IRF of bodies/surfaces to defining their behavior/response to wavelengths, and allowing you simulate data collection from sensors. 

Though I'm still learning my way around this software, so far its been incredibly useful in simulating the beam convergance with rough estimations of the optical setup. I'm still working through designing the beam splitter and filters, and this will be important to make sure UV light isn't being passed into the eye piece (which is obviously very bad), as well as any optical abberations/interference that might occur that I didnt forsee. 

one hurdle i've faced so far is the simulation of an aluminum-based beam splitter, which is giving an unexpected amount of scattering for the passed beam. 

##### Testing using an optical bread board

before 3d printing the entire project to house all the optics and the projector, it'd be best to test out the system for any optical abberations, projected image quality and other parameters/factors. 
To do this I plan on 3d printing a few optical holders and using an optical breadboard to test the whole setup, with the most important factors being
- ability of the system to focus the light onto the sample, changing the power of the objective lens as well as testing if theres enough 'leeway' with the projectors built in focusing mechanism to account for any errors
- ability of the system to project a clear, sharp image onto the sample; needs to maintain sharp "lines" while changing the microscope objective, depending on how "large" the printed image needs to be
- ability to pass/block the respective wavelengths needed; needs to be able to pass UV light through the beam splitter, which is then funneled into the objective lens, while the reflected light needs to be in the visible range to be safely viewed by the imaging sensor/eye. 
- **the most difficult part**: account for any phase shifts/optical abberations that might occur. This might require the use of diffraction gratings or other optical components to select for specific wavelengths. 

##### prototyping and assembley of the optical setup

Finally, once all the problems with the optical breadboard setup are resolved, we can model and 3d print the final setup. Given that the focusing power of the lenses I have at hand are around 200-500 mm, or 
20-50 cm, I believe the setup will be somewhat "long" to accomodate the required focusing points of each lens. 



After getting all of this to work, I'll begin working on a moving stage using the OpenFlexure project, which will allow me to either create multiple samples on a larger wafer, OR to create larger circuits by
projecting and moving the stage. The latter seems more useful but also significantly more difficult, as the stage will have to have incredible precision, along with the optical setup being able to repeatedly
project the same image, with the same precision multiple times.



### Other software

other than the simulation, I've been using FreeCad to model components like the lens holders and mount for the projector. I'll go into detail as why this is a surprisingly important aspect of the project. 

Though im still in the early stages, i'm guessing i'll also have to work with python if I want to collect and process any data, as well as C++ if I want to work with hardware in the later stages of the project when I need to control the block stage to position the wafer. 

#### Knowledge

outside of basic physics, I had no real exposure to optics until now, hence this is probably tied for the most tedious/time consuming aspect of the project. 

I had a really hard time wrapping my head around beam convergance and image formation, stemming from my confusion between point sources on an object versus the actual object being imaged. 
Though my understanding of optics is still rudimentary, resources like Physics Libre text have provided a good foundation for knowldge in the field, as well as resources from companies like Edmund Optics. 

This gave a pretty solid base for understanding compound lens setups, focal lengths, real and virtual images, and image formation, but I havent dove into ideas like optical abberations. 
I'm half hoping that, because this project utilizes short-wavelength light instead of the entire visible spectrum, abberations should be kept to a minimum. 




