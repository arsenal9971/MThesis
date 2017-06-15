### <center> List of Chapters and Content for Master Thesis </center>

Tentative title: 3D Light Field Camera via the Shearlet Transform  
Title that I prefer: Fast Sparse Light Field Reconstruction with Shearlet-based Inpainting

1
0. Abstract, Zusammenfassung.  
1. Introduction.(explain chapters)  
2. Light Field Photography. 
  1. Light Field Photography in the History.  
  2. Light Field Acquisition Settings.
	3. Typical applications for the Light Field Theory.
  4. Geometrix proxy: Stereo Vision and multiview Epipolar Geometry.
		1. Epipolar constraint.
		2. Bolles feature tracking technique and experimental setup.
		4. Functional analysis approach to EPI.
		5. Geometrical approach to EPI.
  5. Physical and computational setup for sparse acquisition of epipolar plane
		1. Physical setup and sampling rate.
		2. Followed pipeline.
		3. Geometric construction of epipolar lines.
		4. Tracking points algorithms.
		5. Procedure for tracking and painting the EPIs.
3. Shearlets.
	  
  1. Continuous Shea.  
  2. Shearlets as Frames.  
  3. Universal Shearlets and Alpha Particles.  
  4. Linear Shearlets and its relation with ridgelets (proof that are parseval frames).
	5. Image inpainting using Shearlets.
  5. Epipolar Plane Representation :with linear Shearlets. (0-particles)  
4. Inpainting Sparse Sampled Epipolar-plane.
  1. Using linear Shearlets to inpain sparse sampled Epipolar-plane.
  2. Iterative thresholding with constant velocity (Gitta and Wang-Q method).  
  3. Iterative thresholding with variable velocity (using paper), check the improvements.  
  4. Experiments with Shearlab.jl with GPU and without.  
5. Application of Geometric Structured Sparsity idea of Irina's thesis (tentative). 

- Appendices::
1. Appendix A: Code for point tracking
