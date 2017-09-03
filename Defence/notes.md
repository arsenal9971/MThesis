## Notes for thesis defence beamer.

- [Presentation of myself and thanks for the public].

### Slide 1: What is this thesis about?

- A sparsely sampled light field reconstruction methdo of a static scene.
- This method uses Universal Shearlets to perform and inpainting algorithm in the sparse Epipolar plane images (EPIs).
- The EPIs are images with linear structures obtained by tracking different feature points in a sequence of pictures of the scene. 
- The slope of the straight lines in the EPIs can be used to compute the depth of feature points in the scene and therefore the depth map that contains the 3D information of the scene. 
- The thesis presents all the steps in the reconstruction pipeline with theory, algorithms and code. 
- [Say that I will explain every concept in the next with a limit of time, so one can find a detailed explanation on the thesis]. 

### Slide 2: Involved concepts.

- Early Vision (biology)[study of how the visual cortex works in order to form the visual information of the world] and Light Field Theory (physics) [how the light as an electromagnetic wave propagates in the 3D space from a scene elements to the humen cortex].
- Computer Vision for point tracking and line detection ([which uses] basic concepts of linear algebra).
- Functional Analysis and Computational Harmonic Analysis ([concept of] sparsifying dictionaries [as wavelets and shearlets]).
- Compressed sensing techniques ([as] $\ell^1$ optimization algorithm).

[When I started to design this thesis I needed to learn light field theory in particular light field reconstruction methods from scratch so I ended up ordering the method on the thesis in the way that they were needed as steps of a pipeline, 

### Slide 3: Light Field Theory.

- In 1846 Michael Faraday proposed for the first time on his lecture "Thoughts on Ray Vibrations" that light could be inrepreted as a field [this based on his work about electromagnetic fields, but this idea was formalized bye Adelson and Bergen until 1991. 

- [They proposed that...]The propagation of light rays in the 3D space is completely described by a 7D continuous function $L(x,y,z,\theta,\phi,\lambda,\tau)$ called the plenoptic function [where $(x,y,z)$ is the location in the 3D space, $\theta$ and $\phi$ are the propagatin angles, $\lambda$ is the wavelength of the corresponding light wave, and $\tau$ the time. This function descibes the amound of light flowing in every direction through every point in space at any time, the magnitud of $L$ is know as the radiance]

- [By fixing $\lambda$ and $\theta$] THe plenoptic function can be simplified to a 4D function $L_4$, called 4D Light Field or simply Light Field, which quantifies the intensity of static and monochromatic light rays propagating in half space. 

- [This looks like an important reduction of information, but his contraint does not limit us in the accurate 3D description of a scene from where the light rays come from, The Light Field of a 3D scene (subspace) describes the 3D information like the depth of the points in the scene and can be recovered by taking multiple pictures (views) of the scene. The goal of this thesis is to explain a particular fast technique for this purpose). 

- [There are different ways to represent a 4D Light Field].
 
### Slide 4: 4D Light Field Representation.

- [From Left to right three different 4D Light Field represenations. Left: LF rays positions indexed by their Cartesian coordinates on a plane and the directional angles leaving each point. Center: LF rays positions are indexed by pairs of point on the surface of a sphere. Right: LF rays positions are indexed by their Cartesian coordinates on two parallel planes, also called two plane parametrization].

- [Due computational low complexity we used the "Two plane parametrization", how to understand it: Consider a camera with image plane coordinates $(u,v)$ and the focus $f$ moving along the $(s,t)$ plane].

- [Once we have clear what is the light field and Before analysing more deeply the method used to recover it I would like just to present some of the motivation that drive me to study this topic which includes, historical work and interesting applications]. 

### Slide 5: Motivation.

### Slide 6: Compression of High Resolution Light Field (Wetzsetein et al., 2013).

- [First time I heard about light field was when I found a paper made by MIT Media Lab -present the paper-, I personally find always very interesting all the work made by MIT Media Lab, due its very creative way to tackle fun problems; on this paper the "Camera Culture Group" leaded by Prof. Gordon Wetzstein proposed a method to compress high resolution light fields using masked acquisition -they insert a mask on the lens of a camera to simulate having and array of lenses that take different views of the scene- and learning an sparsifying dictionary called light field atoms, though the paper is very well explained, the approach seemed to me very complicated and it recquired also very complex and bulky hardware].

- [The most interesting features that I found in this paper was the possibility to perform a refocusing of a scene, when knowing the light field in terms of the depth map].

- [Show the refocusing program by python].

- [After this encounter with the Light Field photrography, I searched for a less bulky hardware that could be used to acquire light field and I found two companies that developed commercial light field cameras -also called plenoptic cameras-].

### Slide 6: Raytrix (Perwass and Wietzke, 2010).

- [The first commercialized plenoptic cameras were developed by the german computer scientist Christian Perwass and Lennart Wietzke, they created the company Raytrix (based on Kiel) that develops since then plenoptic cameras with array of lenses mostly focused on industrial applications, they have very high resolution and their cheapes camera costs 3500 euros].

### Slide 7: Lytro (Ng, 2012).

- [While in germany people was producing industrial Light Field cameras, a Stanford PhD Student in Computer Science and photography aficionado, Ren Ng was developing the first light field camera focused on general public. He created a company Lytro based on silicon valley and develope the Lytro cameras on 2012 that also use lenses arrays and that cost around 500 euros, which still too expensive for my budget].

- [At that moment I was developing a Julia version of the Shearlet Transform library developed by Professor Kutyniok Group, Shearlab so I was interested in the question, could we use Shearlets to recover a sparse sampled light field, in other words, can we compress the Light Field using Shearlets].

### Slide 8: Shearlet Representation of LF (Vagharshakya et al., 2015).

- [After this question I actually found a paper that did exactly that].
- [Why to do something that is already done?].
- [Mathematical curiousity: best way to learn how the things are done is actually do it your self].
- [The commercial cameras are very expensive.]
- [All the papers that I found on this topic, including the ones related to the Lytro and Raytrix cameras, are very obscure when presenting the technical parts; the mathematics behind the reconstruction methods are clear, but they do not give their data set, their code or the side steps to actually go from a raw sequence of pictures to a depth map representing the light field. They also use very slow-high level privative software for some computer vision tasks that can be done in a free and easier way. The reason for this black boxes is commercial interest].

### Slide 9: Freedom of knowledge.

- [Present Donoho and Buckheit quote and explain that this is the main philosophy followed in the thesis].
- [Now that we know the motivation and the philosophy behind this thesis we can proceed on the theory behind the method we are presenting].

### Slide 10: Stereo Vision and multiview Epipolar Geometry.

- The human brain generates the 3D depth perception by triangulating the points of a scene using the information coming from both eyes [that can be interpreted as cameras] [humans can actually percieve 3D with one eye, using the so called "pinhole effect", but this is more complex to explain and does not concern this thesis].
- Epipolar Geometry: Generalization of Stereo Vision with more than two views interpreted as [images taken by a camera that moves withing a trajectory], assuming the epipolar constraint.

- Epipolar Constraint: Supply  the separate analysis of both camera motion and object position by an unified treatment of parameters and concentrate solely in object position while knowing the camera followed trajectory. 
- [The Epipolar Constraint reduces the complexity of the feature point matching in different views from two dimensions to one dimension (Epipolar Line).]
- [The application of Epipolar Geometry to describe the threedimensional information of an static scene was introduced in 1987, he used for this task a dense sequence of images of a static scene -dense in the sens that it forms a solid block of data in which temproal continouity from image to image is equal to spatial continuity].

### Slide 11: EPIs on straight line trajectories.

- [Epipolar lines are the same in the multiple views when the camera trajectory describes a straight line]

- [Tracking the different feature points in the scene corresponding to each of one of this lines we can obtain an image with linear structures that describe the points trajectories, this are called epipolar plane images].

### Slide 12: Functional analysis of EPIs.



### Slide 13: Depth map estimation with EPIs.

### Slide 14: EPIs physical acquisition setup.

### Slide 15: EPIs computational acquisition pipeline. 

### Slide 16: Sparse representation and sampling rate.

### Slide 17: Reconstruction method with inpainting.

### Slide 18: Cone Adapted Shearlets.

### Slide 19: Universal Shearlets and $\alpha$-Shearlets.

### Slide 20: Shearlet-based inpaiting with iterative hard thresholding.

### Slide 21: Line detection and depth map estimation.

### Slide 22: Results and performance benchmarking.

### Slide 23: Conclusions and outlook.

### Slide 24: Thanks. 


