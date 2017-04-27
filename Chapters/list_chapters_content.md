### <center> List of Chapters and Content for Master Thesis </center>

Tentative title: 3D Light Field Camera via the Shearlet Transform  
Title that I prefer: Fast Sparse Light Field Reconstruction with Shearlet Transform

1. Abstract, Zusammenfassung.  
2. Introduction.(explain chapters)  
3. Light Field Photography. 
  1. Light Field Cameras in the History.  
  2. Plenoptic Function.  
  3. 7D to 4D Approximation.  
  4. Epipolar Geometry, Stereo vision and Image rectification.    
  5. Sparse aquisition of Epipolarplane (using OpenCV with such algorithms), with sampling rate.  
4. Shearlets.  
  1. Frames.  
  2. Shearlets as Frames.  
  3. Generalization of Shearlets to Alpha Particles.  
  4. 1D Shearlets and its relation with ridgelets (proof that are parseval frames).  
  5. Epipolar Plane Representaion with 1D Shearlets. (0-particles)  
5. Inpainting Sparse Sampled Epipolar Plane.
  1. Using 1D Shearlets to inpaint it.  
  2. Iterative thresholding with constant velocity (Gitta and Wang-Q method).  
  3. Iterative thresholding with variable velocity (using paper), check the improvements.  
  4. Experiments with Shearlab.jl with GPU and without.  
6. Application of Geometric Structured Sparsity idea of Irina's thesis (tentative).  
